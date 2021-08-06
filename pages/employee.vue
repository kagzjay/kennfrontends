<template>
    <div>
        <NavBar />
        <EditEmployeeModal :employee="selectedEmployee" />
        <DeleteEmployeeModal :employee="selectedEmployee" @onDeleted="getAll" />

        <div class="container">
            <h1>
                List of Employee
            </h1>
            
            <EmployeeEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Age</th>
                        <th>Address</th>
                        <th>Contact</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="employee in employees" :key="employee.id">
                        <td>{{employee.name}}</td>
                        <td>{{employee.age}}</td>
                        <td>{{employee.address}}</td>
                        <td>{{employee.contact}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(employee)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(employee)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
           employee: [],
            selectedEmployee: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/employees')
            .then((res)=>{
                if (res.status==200) {
                    this.employees = res.data
                };
            })
        },
        onEdit(selectedEmployee) {
            this.selectedEmployee = selectedEmployee
            this.$bvModal.show('editEmployeeModal')
        },
        onDelete(selectedEmployee) {
            this.selectedEmployee = selectedEmployee
            this.$bvModal.show('deleteEmployeeModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>