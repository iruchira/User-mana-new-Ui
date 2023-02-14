<script>
    import { createEventDispatcher } from "svelte";
    import SvelteTooltip from 'svelte-tooltip';
    import { onMount } from "svelte";
    import toast from "svelte-french-toast";
    const dispatch = createEventDispatcher();
    export let getData;
    export let userArray;
    console.log(getData());
    onMount(()=>{
        getData()
    });

    const handleDelete = (id) => {
        dispatch("delete", id);
    };
    const handleUpdate = (updateData) => {
        dispatch("update", updateData);
    };
//     (document).ready(function(){
// 	('[data-toggle="tooltip"]').tooltip();
// });
</script>

<div class="container">
    <div class="row">
        <div class="col-md-12">
            <div class="card">
                </div>
                <div class="table-responsive">
                    <table
                    class= "table table-striped table-hover"
                        style="vertical-align: baseline"
                    >
                        <thead class="table_headings">
                            <tr>
                                <!-- <th scope="col" class="border-0 text-uppercase font-medium pl-4">#</th> -->
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Name</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Email</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Address</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Gender</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Date of Birth</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Contact No</th
                                >
                                <th
                                    scope="col"
                                    class="border-0 text-SentenceCase font-medium"
                                    >Action</th
                                >
                            </tr>
                        </thead>

                        <tbody>
                            {#each userArray as user}
                                <tr class="tr">
                                    <!-- <td class="pl-4">{userArray.length}</td> -->
                                    <td>
                                        <h5 class="font-medium mb-0">
                                            {user.firstName +
                                                " " +
                                                user.lastName}
                                        </h5>
                                    </td>
                                    <td>
                                        <span class="text-muted"
                                            >{user.email}</span
                                        ><br />
                                    </td>
                                    <td>
                                        <span class="text-muted"
                                            >{user.address}</span
                                        ><br />
                                    </td>
                                    <td>
                                        <span class="text-muted"
                                            >{user.gender}</span
                                        ><br />
                                    </td>
                                    <td>
                                        <span class="text-muted"
                                            >{user.date_of_birth}</span
                                        ><br />
                                    </td>
                                    <td>
                                        <span class="text-muted"
                                            >{user.contactNo}</span
                                        ><br />
                                    </td>

                                    <td>
                                        <SvelteTooltip tip="Edit" top  color="#ffc107" >
                                        <a href="#" class="settings" title="Settings" on:click={handleUpdate(user)}><i class="material-icons">&#xE8B8;</i></a>
                                        </SvelteTooltip>

                                        <SvelteTooltip tip="Delete" top color="crimson">
                                        <a href="#" class="delete" title="Delete" on:click={handleDelete(user.id)}><i class="material-icons" >&#xE5C9;</i></a>
                                        </SvelteTooltip>                                        
                                        <!-- <button type="button" class="btn btn-outline-info btn-circle btn-lg btn-circle ml-2"><i class="fa fa-upload"></i> </button> -->
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
        <nav aria-label="Page navigation example">
            <ul class="pagination justify-content-end">
              <li class="page-item disabled">
                <a class="page-link" href="#" tabindex="-1">Previous</a>
              </li>
              <li class="page-item"><a class="page-link" href="#">1</a></li>
              <li class="page-item"><a class="page-link" href="#">2</a></li>
              <li class="page-item"><a class="page-link" href="#">3</a></li>
              <li class="page-item">
                <a class="page-link" href="#">Next</a>
              </li>
            </ul>
          </nav>
    </div>
<!-- </div> -->

<style>
    body {
        background: #edf1f5;
        margin-top: 20px;
    }
    .card {
        position: relative;
        display: flex;
        flex-direction: column;
        min-width: 0;
        word-wrap: break-word;
        background-color: #fff;
        background-clip: border-box;
        border: 0 solid transparent;
        border-radius: 0;
    }
    .btn-circle.btn-lg,
    .btn-group-lg > .btn-circle.btn {
        width: 50px;
        height: 50px;
        padding: 14px 15px;
        font-size: 18px;
        line-height: 23px;
    }
    .text-muted {
        color: #8898aa !important;
    }
    [type="button"]:not(:disabled),
    [type="reset"]:not(:disabled),
    [type="submit"]:not(:disabled),
    button:not(:disabled) {
        cursor: pointer;
    }
    .btn-circle {
        border-radius: 100%;
        width: 40px;
        height: 40px;
        padding: 10px;
    }
    .user-table tbody tr .category-select {
        max-width: 150px;
        border-radius: 20px;
    }
    .container {
        margin-left: 5px;
        margin-right: 0px;
        padding-left: 5px;
        padding-right: 5px;
        max-width: none;
    
    }
    .table_headings{
        display: table-header-group;
        margin-bottom: 3px;
        border-bottom: 2px solid lightgray;
        font-size: 14px;
    }
    .h5, h5{
        font-size: 16px;
    }
    table.table td a:hover {
    color: #2196F3;
}
.table-title .btn:hover, .table-title .btn:focus {
    color: #566787;
    background: #f2f2f2;
}
table.table td a.settings {
    color: #2196F3;
}
table.table td a.delete {
    color: #F44336;
}
.table-striped>tbody>tr:nth-of-type(odd) {
     --bs-table-accent-bg: #f8f9fa;
     color: var(--bs-table-striped-color); 
}

table.table-striped.table-hover tbody tr:hover{
    background: #f5f5f5;
}
tbody >.tr{
   height: 70px;
}


</style>
