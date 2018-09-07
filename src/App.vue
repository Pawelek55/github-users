<template>
   <div>
        <h1>Please enter the name of the github user</h1>
        <input type="text" placeholder="Name of user" v-model="user.login">
        <button @click="serch">Serch</button>
        <hr>
        <h2>Serch result:</h2>
        <ul>
            <li v-for="u in users">{{u.login}}</li>
            <li v-for="u in users"><img :src="u.avatar_url" alt=""></li>
            <li v-for="u in users">{{u.repos_url}}</li>
        </ul>
   </div>
</template>

<script>
export default {
  data () {
    return {
        user: {
         login: ''   
        },
        users: []
    }
  },
    methods: {
        serch() {
            console.log(this.user.login)
            this.$http.get('https://api.github.com/users/' + this.user.login)
                .then(response => {
                    console.log(response)
                    return response.json()
                })
                .then(data => {
//                    console.log(data.repos_url)
//                    let respository = data.repos_url;
//                respository.json()
//                console.log(respository)
                    let usersArray = [];
                    usersArray.push(data)
                this.users = usersArray
                });
//            this.$http.get('https://api.github.com/users/'+ this.user.login +'/repos')
        }
    }
}
</script>

<style>
    div{
        text-align: center;
    }
    li{
        list-style: none;
    }
</style>
