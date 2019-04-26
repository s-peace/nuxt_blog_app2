<template>
  <section class="container">
    <div class="cleafix">
      <span>login</span>
    </div>
    <b-form>
      <b-form-group>
        <span>user Id:</span>
        <b-form-input
          placeholder=""
          v-model="formData.id"
        >
        </b-form-input>
        <b-form-checkbox
          v-model="isCreateMode"
        >
          regist new account
        </b-form-checkbox>
        <b-button
          variant="primary"
          @click="handleClickSubmit"
        >
          {{buttonText}}
        </b-button>
      </b-form-group>
    </b-form>
    {{testMsg}}
    <!-- <b-table :items="items"></b-table> -->
  </section>
</template>

<script>
import {mapGetters,mapActions} from 'vuex'
import Cookies from 'universal-cookie'

export default {
  asyncData({redirect,store}){
    if(store.getters['user']){
      redirect('/posts/')
    }
    return {
      isCreateMode: false,
      formData: {
        id: ''
      },
      testMsg: {
        id:'',
        msg: '',
        user : '',
      }
    }
  },
  computed: {
    buttonText(){
      return this.isCreateMode? 'regist' : 'login'
    },
    ...mapGetters(['user'])
  },
  methods: {
    async handleClickSubmit(){
      const cookies = new Cookies()
      if(this.isCreateMode){
        try {
          await this.register({...this.formData})
          this.testMsg = {
            id:this.formData.id,
            msg: `registerd ${this.formData.id}`,
            }
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
          return this.testMsg
        } catch(e){
          this.testMsg = {
            id:`${this.formData.id}`,
            msg: 'failed regist',
            user: this.$store.getters['user'],
            }
          return this.testMsg 
        }
      } else {
        try {
          await this.login({...this.formData})
          this.testMsg = {
            id:this.formData.id,
            msg: `logined ${this.formData.id}`,
            }
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
          return this.testMsg
        } catch(e){
          this.testMsg = {
            id:'',
            msg: 'failed login',
            user: this.user,
            }
          return this.testMsg 
        }
      }
    },
    ...mapActions(['login','register'])
  }
}
</script>

<style>
.form-content{
  margin: 16px;
}
</style>
