<template>
    <div class="container text-center  mt-5 mb-5">
        <div class="table-responsive my-5">

            <!-- The table component -->
            <Table :defaultAll="true" :fields='fields' :studentData="studentData"></Table>

        </div>
        <Edit v-if="popupTriggers.buttonTrigger" :TogglePopup="() => TogglePopup('buttonTrigger')" :fields='fields' :studentData="studentData" :test='test'>


        </Edit>
    </div>
</template>

<script>
    // Importing the table component
    import Table from '@/components/Table.vue';
    import Edit from '@/components/Edit.vue';
    import { ref } from 'vue';
    //importing bootstrap 
    import "bootstrap/dist/css/bootstrap.min.css";
    export default {
        name: 'App',
        methods: {
            edit(studentData) {
                const _id = document.getElementById("id").value;
                const _name = document.getElementById("name").value;
                const _school = document.getElementById("school").value;
                for (const obj of studentData) {
                    if (obj.ID == _id) {
                        obj.Name = _name;
                        obj.School = _school;
                        break;
                    }
                }
                return studentData;
            }
        },
        components: {
            Table,
            Edit
        },
        setup() {
            const popupTriggers = ref({
                buttonTrigger: false
            });
            const TogglePopup = (trigger) => {
                popupTriggers.value[trigger] = !popupTriggers.value[trigger]
            };
            const studentData = [
                { ID: 1, Naam: "Bar", School: "Fontys Hogescholen" },
                { ID: 2, Naam: "Bob Ross", School: "Avans Hogeschool" },
                { ID: 3, Naam: "John Doe", School: "Technische Universiteit Eindhoven" },
                { ID: 4, Naam: "Qux Baz", School: "Hogeschool Zuyd" },
                { ID: 5, Naam: "Foo", School: "Expivi University" },
                { ID: 6, Naam: "Lorem", School: "Hogeschool Ipsum" }
            ]
            const fields = [
                'ID', 'Naam', 'School'
            ]
         
            return { studentData, fields, popupTriggers, TogglePopup }
        },
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    
    label {
        display: inline-block;
        width: 200px;
        margin-right: 10px;
        text-align: right;
    }

    input {
    }

    fieldset {
        border: none;
        width: 500px;
        margin: 0px auto;
    }
</style>