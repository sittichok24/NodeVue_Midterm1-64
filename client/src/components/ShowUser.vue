<template>
  <div>
    <h1>ข้อมูลสายรถเมล์</h1>
    <p>id: {{ userId }}</p>
    <p>ชื่อสายรถเมล์ :  {{ user.name }} </p>
    <p>หมายเลขทะเบียนรถ :  {{ user.lastname }} </p>
    <p>ชื่อผู้ขับ : {{ user.email }}</p>
    <p>เบอร์ติดต่อ : {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>