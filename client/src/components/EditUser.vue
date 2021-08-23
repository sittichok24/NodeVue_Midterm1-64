<template>
<div>
    <h1>Edit Bus Lines</h1>
    <form v-on:submit.prevent = "editUser">
        <p>ชื่อสายรถเมล์ : <input type="text" v-model="user.name"></p>
        <p>หมายเลขทะเบียนรถ : <input type="text" v-model="user.lastname"></p>
        <p>ชื่อผู้ขับ : <input type="text" v-model="user.email"></p>
        <p>เบอร์ติดต่อ : <input type="text" v-model="user.password"></p>
        <p><button type="submit">แก้ไขสายรถเมล์</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อสายรถเมล์ : {{user.name}}</p>
        <p>หมายเลขทะเบียนรถ : {{user.lastname}}</p>
        <p>ชื่อผู้ขับ : {{user.email}}</p>
        <p>เบอร์ติดต่อ : {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>