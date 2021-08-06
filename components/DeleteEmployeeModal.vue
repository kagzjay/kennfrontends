<template>
    <div>
        <b-modal id="deleteEmployeeModal" title="Delete Employee" ok-title="Delete Employee" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this employee? <br><br>
            Name: {{employee.name}} <br>
            Age: {{employee.age}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        employee: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/employees/' + this.employee.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>