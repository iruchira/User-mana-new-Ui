<script>
    import { createEventDispatcher } from "svelte";
    //new instance of createEventDispatcher is created//
    const dispatch = createEventDispatcher();
    export let objToUpdate;
    let data = "";
    console.log("objToUpdate");
    if (objToUpdate === undefined) {
        data = {
            firstName: "",
            lastName: "",
            email: "",
            password: "",
            confirmPassword: "",
            address: "",
            gender: "",
            date_of_birth: "",
            contactNo: "",
        };
    } else {
        data = {
            id: objToUpdate.id,
            firstName: objToUpdate.firstName,
            lastName: objToUpdate.lastName,
            email: objToUpdate.email,
            password: objToUpdate.password,
            address: objToUpdate.address,
            gender: objToUpdate.gender,
            date_of_birth: objToUpdate.date_of_birth,
            contactNo: objToUpdate.contactNo,
        };
    }
    function formInfo() {
        dispatch("createInfo", data);
    }
    function handleUpdate() {
        dispatch("update", data);
    }
    //Form validation//
    let NameError = "";
    let lastNameError = "";
    let emailError = "";
    let passwordError = "";
    let conPassError = "";
    let contactNoError = "";
    let submitError= "";
    function nameValidation() {
        var name = data.firstName;
         if (name.length == 0 || name.trim() === "") {
            NameError = " * name cannot be empty";
            return false;
        }if (!name.match(/^[A-Za-z\s]*$/)) {
            NameError = "alphabets only";
            return false;
        } NameError ='';
            return true;
    }
    function lastNameValidation() {
        var lname = data.lastName;
        if (lname.length == 0 || lname.trim() === "") {
            lastNameError = "* name cannot be empty";
            return false;
        }if (!lname.match(/^[A-Za-z\s]*$/)) {
            lastNameError = "alphabets only";
            return false;
        }lastNameError = "";
            return true;

    }
    function emailValidation() {
        var emailId = data.email;
        if (emailId.length == 0 || emailId.trim() === "") {
            emailError = "* Required";
            return false;
        }if (!emailId.match(/^[a-zA-Z0-9+_.-]+@[a-zA-Z0-9.-]+$/)) {
            emailError = "invalid email"
            return false;
        }emailError = "";
            return true;


    }
    function passwordValidation() {
        var pass = data.password;
        var passwordStr = pass.match(
            /^(?=.{10,}$)(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*\W).*$/
        );
        var confpass = data.confirmPassword;
         
        if (pass.length !== 10 && (pass !== passwordStr)) {
            passwordError =
            "*Required 1 char, 1 Uppercase, 1 lowercase, 1 special character and 1 number";
            return false;
        }
        if ( confpass !== pass) {
            conPassError = "Passwords do not match";
            return false;

        }passwordError = "";
        conPassError = "";
            return true;

    }
    function contactNoValidation() {
        var cont = data.contactNo;
        if (cont.length == 0 || cont.trim() == "") {
            contactNoError = "*Require field";
            return false;
        }if (cont !== cont.match(/^(\+)([1-9]{2})(\s)(\d{10})$/g)) {
            contactNoError = "Enter 10 digit mobile no";
            return false;
        }contactNoError = "";
            return true;
    }

    function handleSubmit(){
        if(! nameValidation() || ! lastNameValidation() || ! emailValidation() || ! passwordValidation() || ! passwordValidation()){
            submitError = "* Please fill out required fields ";
        }
            submitError ="";
    }
   
</script>

<section>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>The Easiest Way to Add Input Masks to Your Forms</title>
</section>

<div class="registration-form">
    <form>
        <div class="form-icon">
            <span><i class="icon icon-user"/></span>
        </div>
        <div class="form-group">
            <input
                type="text"
                class="form-control item"
                id="firstName"
                placeholder="Firstname"
                on:keyup={nameValidation}
                bind:value={data.firstName}
            />
            <span
            class="errorDiv"
            contenteditable="false"
            bind:innerHTML={NameError}
        >
            {NameError}
        </span>
        </div>
        <div class="form-group">
            <input
                type="text"
                class="form-control item"
                id="lastName"
                placeholder="Lastname"
                on:keyup={lastNameValidation}
                bind:value={data.lastName}
            />
            <span
                class="errorDiv"
                contenteditable="false"
                bind:innerHTML={lastNameError}
            >
                {lastNameError}
            </span>
        </div>
        <div class="form-group">
            <input
                type="email"
                class="form-control item"
                id="email"
                placeholder="Email"
                on:keyup={emailValidation}
                bind:value={data.email}
            />
            <span
                class="errorDiv"
                contenteditable="false"
                bind:innerHTML={emailError}
            >
                {emailError}
            </span>
        </div>
        <div class="form-group">
            <input
                type="password"
                class="form-control item"
                id="password"
                placeholder="Password"
                on:keyup={passwordValidation}
                bind:value={data.password}
            />
            <span
                class="errorDiv"
                contenteditable="false"
                bind:innerHTML={passwordError}
            >
                {passwordError}
            </span>
        </div>
        <div class="form-group">
            <input
                type="password"
                class="form-control item"
                id="Confpassword"
                placeholder="Confirm Password"
                on:keyup={passwordValidation}
                bind:value={data.confirmPassword}
            />
            <span
                class="errorDiv"
                contenteditable="false"
                bind:innerHTML={conPassError}
            >
                {conPassError}
            </span>
        </div>
        <div class="form-group">
            <input
                type="text"
                class="form-control item"
                id="address"
                placeholder="Address"
                bind:value={data.address}
            />
            <span class="errorDiv"></span>
        </div>
        <div class="form-group">
            <select type="select"
            class="form-control item"
            id="gender"
            placeholder="Gender"
            bind:value={data.gender}
            ><option value="" disabled selected>Select Gender</option>
            <option value="male">Male</option>
            <option value="Female">Female</option>
            <option value="other">Other</option>
        </select>
            <span class="errorDiv"></span>
        </div>
        <div class="form-group">
            <input
                type="date"
                class="form-control item"
                id="dateOfBirth"
                placeholder="D.O.B : dd-mm-yy"
                bind:value={data.date_of_birth}
            />
            <span class="errorDiv"></span>
        </div>
        <div class="form-group">
            <input
                type="text"
                id="contactNo"
                class="form-control item"
                placeholder="Contact No"
                on:keyup={contactNoValidation}
                bind:value={data.contactNo}
            />
            <span
                class="errorDiv"
                contenteditable="false"
                bind:innerHTML={contactNoError}
            >
                {contactNoError}
            </span>
        </div>
        <div class="form-group">
            <button
                type="button"
                class="btn btn-block create-account"
                id="submitButton"
                on:click={() => {
                    if (objToUpdate === undefined) {
                        formInfo();
                    } else {
                        handleUpdate();
                    }
                }}>Create Account</button
            >
        </div>
    </form>
</div>

<style>
    body {
        background-color: #dee9ff;
    }

    .registration-form {
        padding: 50px 0;
        width: 600px;
    }

    .registration-form form {
        background-color: #fff;
        max-width: 600px;
        margin: auto;
        padding: 50px 70px;
        border-top-left-radius: 30px;
        border-top-right-radius: 30px;
        box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.075);
        border-bottom-left-radius: 30px;
        border-bottom-right-radius: 30px;
        color: #9fadca;
        /* border-top: 1px solid #dee9ff; */
        box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.075);
    }

    .registration-form .form-icon {
        text-align: center;
        background-color: #5891ff;
        border-radius: 50%;
        font-size: 40px;
        color: white;
        width: 100px;
        height: 100px;
        margin: auto;
        margin-bottom: 50px;
        line-height: 100px;
    }

    .registration-form .item {
        border-radius: 20px;
        margin-bottom: 0px;
        padding: 10px 20px;
    }

    .registration-form .create-account {
        border-radius: 30px;
        padding: 10px 20px;
        font-size: 18px;
        font-weight: bold;
        background-color: #5791ff;
        border: none;
        color: white;
        margin-top: 20px;
    }
    .registration-form .social-icons {
        margin-top: 30px;
        margin-bottom: 16px;
    }

    .registration-form .social-icons a {
        font-size: 23px;
        margin: 0 3px;
        color: #5691ff;
        border: 1px solid;
        border-radius: 50%;
        width: 45px;
        display: inline-block;
        height: 45px;
        text-align: center;
        background-color: #fff;
        line-height: 45px;
    }
   
    .errorDiv {
        /* margin-left:0 px; */
        padding-left: 20px;
        display:inline-block;
        color :red;
        margin-bottom: 3px;
        margin-top: 0px;
        font-size:12px;
    }
    
    .registration-form .social-icons a:hover {
        text-decoration: none;
        opacity: 0.6;
    }
    .valid{
    border-color : 2px solid green;
   }
   .invalid{
    border-color:red;
   }

    @media (max-width: 576px) {
        .registration-form form {
            padding: 50px 20px;
        }
        .registration-form .form-icon {
            width: 70px;
            height: 70px;
            font-size: 30px;
            line-height: 70px;
        }
    }

</style>
