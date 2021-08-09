<template>
  <div style="width: 100%; height: 100vh; overflow: hidden"> <!--  :style="bg" 加背景图片-->
    <div style="width: 400px; margin: 100px auto">
      <div style="font-size: 30px; text-align: center; padding: 30px 0">欢迎登录</div>
          <button style="width: 100%" @click="login">登 录</button>
      <a href="/"><span id="sp">自动点击</span></a>
    </div>
  </div>
</template>

<script>

  // @ is an alias to /src
import request from "@/utils/request";

export default {
  name: "Login",
  data() {
    return {
      form: {role: 2, username: 'zhang', password: '123'},
      rules: {
        username: [
          {required: true, message: '请输入', trigger: 'blur'},
        ],
        password: [
          {required: true, message: '请输入', trigger: 'blur'},
        ],
      },
      // 加背景图片
      // bg: {
      //   backgroundImage: "url(" + require("@/assets/bg.jpg") + ")",
      //   backgroundRepeat: "no-repeat",
      //   backgroundSize: "100% 100%"
      // }
    }
  },
  created() {
    sessionStorage.removeItem("user")
  },
  methods: {
    login() {
      $(function(){ //跳转到主页，该方法能避免主页组件失效
        $("#sp").trigger("click");
      });
          request.post("/user/login", this.form).then(res => {
            if (res.code === '0') {
              sessionStorage.setItem("user", JSON.stringify(res.data))  // 缓存用户信息
              this.$router.push("/")  //登录成功之后进行页面的跳转，跳转到主页
              console.log('success')
            } else {
              console.log('error')
            }
          })
    }
  }
}
</script>

<style scoped>

</style>
