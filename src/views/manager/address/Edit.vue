<template>
    <briup-fulllayout title="添加地址">
    <div>
      {{form}}
      <van-cell-group>
      <van-field v-model="form.telephone" placeholder="请输入手机号" />
      </van-cell-group>
      <van-cell-group>
      <van-field v-model="form.province" placeholder="省" />
      </van-cell-group>
      <van-cell-group>
      <van-field v-model="form.city" placeholder="市" />
      </van-cell-group>
      <van-cell-group>
      <van-field v-model="form.area" placeholder="区" />
      </van-cell-group>
      <van-cell-group>
      <van-field v-model="form.address" placeholder="详细地址" />
      </van-cell-group>
      <van-button block @click="submitHandler" type="primary">保存</van-button>
  </div>
    </briup-fulllayout>
</template>
<script>
import {post,response}  from '../../../http/axios'
import {mapState} from 'vuex'
export default {
  data(){
    return{
     form:{}
       }
  },
    computed:{
      //将状态机中的user对象中的info对象取到
      ...mapState("user",["info"])
    },
  methods:{
    submitHandler(){
      let url="/address/saveOrUpdate";
      this.form.customerId=this.info.id;
      post(url,this.form).then((response)=>{
        
        this.$router.go(-1);
        this.$toast.success("添加成功");
      })
    },
    
  }
}
</script>