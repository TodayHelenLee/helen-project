<template>
  <div>
    <h1>{{$route.query.app}}:result</h1>
    <button>消失bar</button>
    <router-link :to="`/acc/child?id=${id}`">跳轉</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
mounted:function(){

    console.log(this.$route.query.app)
}
,
data:function(){
return{
    id:'/',
    result:this.$route.query.app
}

}
}
</script>

<style>

</style>