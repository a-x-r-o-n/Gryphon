<script>

import Navbar from "./components/Navbar.vue";
import SearchDisplayer from "./components/SearchDisplayer.vue";

export default {
  name: "App",
  data: function(){
    return {
      userData: null,
      userUrl: `https://api.github.com/users/${this.userData?this.userData["Login"]:''}`,
      userRepos: this.userData?(this.userUrl+'/repos'):'',
      userReposData: null,
    }
  },
  methods: {
    bindUserData(data){
      console.log("Method Ativated");
      this.userData = data;
      this.fetchUserRepos();
    },
    fetchUserRepos(){
      if(this.userData["login"]){
        const xhttp = new XMLHttpRequest();
        let self = this;
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            self.userReposData = JSON.parse(this.responseText);
            console.log("log at App.vue:\n",this.userReposData);
          }
        };
        xhttp.open("GET", `${this.userData["repos_url"]}`, true);
        xhttp.send();
      }
    }
  },
  components: {
    Navbar,SearchDisplayer
  },
};
</script>


<template>
  <Navbar @passUserData="bindUserData" :userData = this.userData :userReposData = this.userReposData?this.userReposData:[] />
  <SearchDisplayer :userData="this.userData"/>
  
</template>