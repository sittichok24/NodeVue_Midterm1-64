<template>
  <div>
    <h1>Bus Lines</h1>
    <div v-if="users.length">
      <h4>จำนวนสายรถเมล์ {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            สร้างสายรถเมล์
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
       <p>ชื่อสายรถเมล์ : {{user.name}}</p>
        <p>หมายเลขทะเบียนรถ : {{user.lastname}}</p>
        <p>ชื่อผู้ขับ : {{user.email}}</p>
        <p>เบอร์ติดต่อ : {{user.password}}</p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูลผู้ใช้
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูล
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูล
          </button>
       <p> </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>