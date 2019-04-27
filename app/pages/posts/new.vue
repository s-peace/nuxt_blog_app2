<template>
  <section class="container posts-page">
    <div slot="header" class="clearfix">
      <b-form-input placeholder="type title" v-model="formData.title"></b-form-input>
    </div>
    <div>
      <b-form-input placeholder="type text"
                    type="textarea" rows="15"
                    b-model="formData.body"></b-form-input>
    </div>
    <div class="text-right"
          style="margin-top: 16px">
      <b-button variant="primary" @click="publish">
        <span>publish</span>
      </b-button>
    </div>
  </section>
</template>

<script>
import {mapGetters,mapActions} from 'vuex'

export default {
  asyncData({redirect,store}){
    if(!store.getters['user']){
      redirect('/')
    }
    return {
      formData: {
        title: '',
        body: '',
      }
    }
  },
  computed:{
    ...mapGetters(['user'])
  },
  methods: {
    publish(){
      
    }
  }
}
</script>

