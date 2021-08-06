<template>
    <div>
        <b-button v-b-modal.EmployeeEntryModal variant="primary">Add Employee</b-button>

        <b-modal id="EmployeeEntryModal" title="Employee Entry" ok-title="Save Employee" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="employee.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Age" label-for="age">
                <b-form-input id="age" v-model="employee.age" trim></b-form-input>
                </b-form-group>
                

                <b-form-group label="Address" label-for="address">
                <b-form-input id="address" v-model="employee.address" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Contact" label-for="contact">
                <b-form-select v-model="employee.contact" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            employee: {},
            options: [
                {value: 'email', text: 'email'},
                {value: 'mobile number', text: 'mobile number'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('/api/employees', this.employee)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added an employee')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>