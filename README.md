# POS (projectpos)

A Quasar Framework app

## Install the dependencies
```bash
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```

## Axios initialization
Axios instance is initialized in `/src/boot/axios.js`. This file executes on app's boot up. Axios' `$api` instance is made to be globally available in Vue components and is available using `this.$api`.

### Making requests
Inside the created() hook of index page /src/pages/Index.vue, a GET request is first made to `/sanctum/csrf-cookie` endpoint. And after recieving a response, a POST request is made to the  `/api/website/event/all` 

```
created(){
    this.$api.get('/sanctum/csrf-cookie').then(response => {
        console.log(document.cookie);
        this.$api.post('/api/website/event/all', {}, {withCredentials: true}).then(response => {
            this.$store.commit('setAllEvents', response.data.data);
        }).catch(error => {
            console.log(error);
        })
    }).catch(error => {
        console.log(error);
    })
  }
```
