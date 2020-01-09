<template>
  <briup-fulllayout title="常用地址">
  <van-list >
    <van-cell
      v-for="item in addresses"
      :key="item.id"
      :title="item.province+''+item.city+''+item.area+''+item.address"
    />
</van-list>
<br>
<van-button block type="primary"  @click="toAddressEditHandler">添加</van-button>
<van-button block >修改</van-button>
  </briup-fulllayout>
</template>
<script>
import {get,post} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
 computed:{  //计算属性
    //将状态机中的user对象中的info对象获取到
    ...mapState("user",["info"])
  },
  data(){
    return{
      addresses:[]
       }
  },
  created(){
        this.loadAddress()
    },
    
  methods:{
    loadAddress(){
       let id = this.info.id;
       let url = "/address/findByCustomerId?id="+id;
       get(url).then((response)=>{
        //将查询结果。数组中的前6个元素获取到
        this.addresses = response.data;
      })
    },
     toAddressEditHandler(){
        //编程跳转
        this.$router.push("/manager/address_edit")
    },
    
  }
}
</script>