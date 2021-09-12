<template>
  <q-page class="flex flex-center">
    {{ title }}
  </q-page>
</template>

<script>

export default {
  name: 'PageIndex',
  data(){
    return {
      title: "API Troubleshoot"
    }
  },
  created(){
    this.$api.get('/sanctum/csrf-cookie').then(response => {
        console.log(document.cookie);
        // console.log( response.headers['set-cookie'] );
        this.$api.post('/api/website/event/all', {}, {withCredentials: true}).then(response => {
            this.$store.commit('setAllEvents', response.data.data);
        }).catch(error => {
            console.log(error);
        })
    }).catch(error => {
        console.log(error);
    })
  }
}
</script>
