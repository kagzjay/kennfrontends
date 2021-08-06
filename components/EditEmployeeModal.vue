<template>
    <div>
        <b-modal id="editEmployeeModal" title="Edit Employee" ok-title="Save Employee" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="employee.name" trim></b-form-input>
                </b-form-group>employee

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
    props: {
        employee: {}
    },
    data() {
        return {
            options: [
                {value: 'programmer', text: 'programmer'},
                {value: 'designer', text: 'designer'},
               
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/employees/' + this.employee.id, this.employee)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>