<template>
    <div class="popup">
        <div class="popup-inner">
            <slot />
            <label for="editTitle"></label><h1 id="editTitle" name="editTitle">Edit</h1>
            <label for="students">Verander de gevevens</label>
            <br />
            <label for="id">Id</label>
            <input type="number" name="id" id="id" readonly>
            <br>
            <label for="naam">Naam</label>
            <input type="text" name="naam" id="naam">
            <br>
            <label for="school">School</label>
            <input type="text" name="school" id="school">
            <br>
            <div>
                <button class="closeButton" @click='TogglePopup(); '>Close</button>

                <button class="editButton" @click='edit(studentData); TogglePopup(); '>Edit</button>
            </div>

        </div>
    </div>
</template>
<script>
    //importing bootstrap 
    import "bootstrap/dist/css/bootstrap.min.css";
    export default {
        name: 'App',
        mounted() {
            this.SetPlaceholder(this.currentRow);
        },
        methods: {
            edit(studentData) {
                const _id = document.getElementById("id").value;
                const _naam = document.getElementById("naam").value;
                const _school = document.getElementById("school").value;
                for (const obj of studentData) {
                    if (obj.ID == _id) {
                        obj.Naam = _naam;
                        obj.School = _school;
                        break;
                    }
                }
                return studentData;
            },
            SetPlaceholder(currentRow) {
                //alert(currentRow[0]);

                //Set Placeholders
                document.getElementById("id").value = currentRow[0];
                document.getElementById("naam").placeholder = currentRow[1];
                document.getElementById("school").placeholder = currentRow[2];
            }
        },
        props:{
            studentData: {
                type: Array,
            },
            fields: {
                type: Array,
            },
            TogglePopup: {

            },
            currentRow: {
                type: Array,
            }

        }
    }
    

</script>
<style>
    .popup{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index:99;
        background-color: rgba(0,0,0,0.2);
        display: flex;
        align-items:center;
        justify-content: center;
    }
    .popup-inner{
        background: #FFF;
        padding: 32px;
    }
    .closeButton {
        border-color: #ff0000;
        padding: 5px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin-left: 20px;
    }
    .editButton {
        border-color: #cfd017 ;
        padding: 5px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin-top: 5px;
        margin-left: 20px;
    }
</style>