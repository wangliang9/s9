<template>
    <div>
      <h1>{{msg}}</h1>
      <ul v-for="row in courseList">
        <li><router-link to="/detail">{{row.title}}</router-link></li>

      </ul>
    </div>
</template>

<script>
    export default {
        name: "course",
        data(){
          return{
            msg:'课程列表',
            courseList:[

            ]
          }
        },
        mounted:function() {
          // vue页面刚加载时自动执行
          this.initCourse()
        },
        methods:{
            initCourse() {
              var that = this
              this.$axios.request({
                url:'http://127.0.0.1:8000/api/v1/course/',
                method:"GET"
              }).then(function (ret) {
                //ajax请求成功后，获取的响应内容
                if(ret.data.code === 1000){
                  console.log(ret.data)
                  that.courseList = ret.data.data
                }else{
                  alert('获取数据失败')
                }
              }).catch(function (ret) {
                //ajax请求失败之后，获取响应的内容
              })
            }
        }
    }
</script>

<style scoped>

</style>
