<template>
  <section class="container">
    <div class="cleafix">
      <span>login</span>
    </div>
    <b-form>
      <b-form-group>
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
    <b-table :items="items"></b-table>
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
      items: []
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
          this.items = [{
            id:this.formData.id,
            msg: `registerd ${this.formData.id}`,
            }]
          return this.items 
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch(e){
          this.items = [{
            id:'',
            msg: 'failed regist',
            }]
          return this.items 
        }
      } else {
        try {
          await this.login({...this.formData})
          this.items = [{
            id:this.formData.id,
            msg: `logined ${this.formData.id}`,
            }]
          return this.items
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch(e){
          this.items = [{
            id:'',
            msg: 'failed login',
            }]
          return this.items 
        }
      }
    }
  },
  ...mapActions(['login','register'])
}
</script>

<style>
.form-content{
  margin: 16px;
}
</style>
