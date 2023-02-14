<script>
    import Icon from "@iconify/svelte";
    import DisplayUser from "./displayUser.svelte";
    import AdminPanel from "./adminPanel.svelte";
    import UserForm from "./userForm.svelte";
    //for toast msg//
    import toast, { Toaster } from "svelte-french-toast";

    let objToUpdate = "";
    let userArray = [];
    let counter = "displayUserList";
    
    const getData = async () => {
        try {
            const response = await fetch("http://localhost:3000/user/");
            userArray = await response.json();
            console.log(userArray);
        } catch (error) {
            console.log("error....");
        }
    };

    let postData = async (event) => {
        let data = event.detail;
        if (
            data.firstName.trim() === "" ||
            data.lastName.trim() === "" ||
            data.password.trim() === "" ||
            data.gender.trim() === "" ||
            data.address.trim() === "" ||
            data.date_of_birth.trim() === "" ||
            data.contactNo.trim() === ""
        ) {
            console.log("data invalid");
            toast.error("Please enter valid data..");
        }else {
            try {
                const res = await fetch("http://localhost:3000/user/", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },

                    body: JSON.stringify({
                        firstName: data.firstName,
                        lastName: data.lastName,
                        email: data.email,
                        password: data.password,
                        gender: data.gender,
                        address: data.address,
                        date_of_birth: data.date_of_birth,
                        contactNo: data.contactNo,
                    }),
                });
                const response = await res.text();
                //  const data = await response.text();
                console.log(response);
                // isFormEnable = true
                counter = "displayUserList";
                toast.success("user added...");
            } catch (error) {
                console.log("error in writing file...." + error);
            }
        }
    };

    const deleteUserData = async (e) => {
        console.log(e.detail);
        const res = await fetch("http://localhost:3000/user/" + e.detail, {
            method: "DELETE",
        });
        const response = await res.text();
        console.log(response);
        var findingId = "";
        for (let i = 0; i < userArray.length; i++) {
            if (userArray[i].id === e.detail) {
                findingId = i;
            }
        }
        userArray.splice(findingId, 1);
        userArray = userArray;
    };

    const updateUser = async (event) => {
        try {
            objToUpdate = event.detail;
            console.log(objToUpdate);
            counter = "updateUserList";
        } catch (error) {
            console.log("error updating obj....");
        }
    };

    const updatedList = async (e) => {
        try {
            //getting the object which we want to update//
            let updatedData = e.detail;
            console.log(e.detail);
            const response = await fetch(
                "http://localhost:3000/user/" + updatedData.id,
                {
                    method: "PATCH",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        firstName: updatedData.firstName,
                        lastName: updatedData.lastName,
                        gender: updatedData.gender,
                        address: updatedData.address,
                        date_of_birth: updatedData.date_of_birth,
                        email: updatedData.email,
                        password: updatedData.password,
                        contactNo: updatedData.contactNo,
                    }),
                }
            );
            const res = response.text();
            console.log(res);
            counter = "displayUserList";
            toast.success("user updated sucessfully...");

        } catch (error) {
            console.log("error while displaying user list");
        }
    };
</script>
<Toaster/>
<main>
    <!-- <section class= "s0"> -->
        <div class="row">
          <div class="col-sm-5"><h2>User  <b>Managment</b></h2></div>
          <div class="col-sm-7">
            <button class="btn btn-secondary" on:click={() => {
                counter = "displayUserList";
            }}><Icon icon="material-symbols:home" inline={true} />
                <span>Home</span></button>
            <button class="btn btn-secondary" on:click={() => {
                counter = "addUser";
            }}><Icon icon="material-symbols:add-circle" inline={true} />
                <span>Add New User</span></button>     
        </div>
        </div>
    <!-- <section class="s1"> -->
        <!-- <div class="s10"><AdminPanel /></div> -->
        <div class="s11">
            {#if counter === "displayUserList"}
                <DisplayUser
                    {userArray}
                    {getData}
                    on:delete={deleteUserData}
                    on:update={updateUser}
                />
            {:else if counter === "addUser"}
                <UserForm on:createInfo={postData} />
            {:else if counter === "updateUserList"}
                <UserForm {objToUpdate} on:update={updatedList} />
            {/if}
        </div>
    <!-- </section> -->
</main>

<style>
    * {
        margin: 0px;
        padding-top: 0px;
        padding-right: 0px;
        padding-left: 0px;
        padding-bottom: 0px;
    }
.row{
    box-sizing: border-box;
    font-family: 'Varela Round', sans-serif;
    font-size: 13px;
    background-color: #007bff;
    color: white;
    height: 70px;
    align-items: center;
    padding-left: 22px;
}
.col-sm-7{
    justify-content: flex-end; 
    display: flex; 
}
.btn {
    height: 35px;
    padding: 5px;
    border: none;
    outline: none;
    color: #566787;
    background: white;
    margin-right: 20px;
    border-radius: 3%;
    font-weight: 400;
    margin-right: 15px;

   
}
.btn-secondary{
    border-radius: 2px;
    padding: 7px;
    /* margin-right: 5px; */
    margin-left: 6px;
    text-align: center;
    line-height: 1.5;
}
.btn-secondary :hover{
    color: #566787;
    background: #f2f2f2;
}
 .btn:not(:disabled):not(.disabled):hover {
     cursor: pointer; 
     background-color: #f8f9fa;
}
    #addButton {
        margin-right: 10px;
        background: black;
        box-shadow: 0.5px lightgrey;
    }
    .s1 {
        display: flex;
        flex-direction: row;
        align-items: stretch;
        height: 1000px;
        background: white;
    }
    .s10 {
        /* flex-grow:0.5; */
        padding: 2px;
        /* border:1px solid black; */
        border-radius: 2px;
    }
    .s11 {
        display: flex; 
        justify-content: center;
        flex-grow: 5;
        padding: 2px;
        /* border:1px solid black; */
        border-radius: 2px;
    }
</style>
