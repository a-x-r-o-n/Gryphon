<script>

import Navbar from "./components/Navbar.vue";
import SearchDisplayer from "./components/SearchDisplayer.vue";

export default {
  name: "App",
  data: function(){
    return {
      gitt: "",
      userData: null,
      userUrl: `https://api.github.com/users/${this.userData?this.userData["Login"]:''}`,
      userRepos: this.userData?(this.userUrl+'/repos'):'',
      userStarred: this.userData?(this.userUrl+'/starred'):'',
      userReposData: null,
      tempPlaceholder: null,
      recentCreatedRepo: [],
      recentCreatedRepoWithLanguage: {}
    }
  },
  methods: {
    bindUserData(data){
      //console.log("Method Ativated");
      this.userData = data;
      this.fetchUserRepos();
      this.fetchUserStarred();
      this.fetchUserRecentCreatedRepo();
    },
    fetchUserRepos(){
      if(this.userData["login"]){
        const xhttp = new XMLHttpRequest();
        let self = this;
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            self.userReposData = JSON.parse(this.responseText);
            //console.log("log at App.vue:\n",this.userReposData);
          }
        };
        xhttp.open("GET", `${this.userData["repos_url"]}`, true);
        xhttp.setRequestHeader("Authorization", "Bearer " + self.api);
        xhttp.send();
      }
    },
    fetchUserStarred(){
      if(this.userData["login"]){
        const xhttp = new XMLHttpRequest();
        let self = this;
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            self.userStarred = JSON.parse(this.responseText);
            // //console.log("log at App.vue:\n",this.userReposData);
          }
        };
        xhttp.open("GET", `https://api.github.com/users/${this.userData["login"]}/starred`, true);
        xhttp.setRequestHeader("Authorization", "Bearer " + self.api);
        xhttp.send();
      }
    },
    fetchTopLanguageUsedInRepo(repoName){
      const xhttp = new XMLHttpRequest();
      let self = this;
      xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
          self.tempPlaceholder = JSON.parse(this.responseText);
          self.recentCreatedRepoWithLanguage[`${repoName}`]=Object.keys(self.tempPlaceholder)[0];

          //console.log("log at App.vue:\n",this.tempPlaceholder);
        }
      }
      xhttp.open("GET", `https://api.github.com/repos/${this.userData["login"]}/${repoName}/languages`, true);
      xhttp.setRequestHeader("Authorization", "Bearer " + self.api);
      xhttp.send();

      
      // this.recentCreatedRepoWithLanguage[`${repoName}`]=Object.keys(this.tempPlaceholder)[0];
    },
    fetchUserRecentCreatedRepo(){

      if(this.userData["login"]){
        const xhttp = new XMLHttpRequest();
        let self = this;
        xhttp.onreadystatechange = function() {
          if (this.readyState == 4 && this.status == 200) {
            self.recentCreatedRepo = JSON.parse(this.responseText);
            // //console.log("log at App.vue:\n",this.userReposData);
            self.recentCreatedRepo.forEach( repo => {
              console.log(`sending ${repo["name"]} for fetching Top language`);
            self.fetchTopLanguageUsedInRepo(repo["name"]);
        });
        console.log(self.recentCreatedRepoWithLanguage);
          }
        };
        xhttp.open("GET", `https://api.github.com/users/${this.userData["login"]}/repos?sort=created&direction=desc&per_page=6`, true);
        xhttp.setRequestHeader("Authorization", "Bearer " + self.api);
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
  <Navbar @passUserData="bindUserData" :userData = this.userData :userReposData = this.userReposData?this.userReposData:[] :userStarredData = this.userStarred?this.userStarred:[] :gitt = "this.gitt" />
  <SearchDisplayer :userData="this.userData" :recentCreatedRepo="this.recentCreatedRepo?this.recentCreatedRepo:[]" :recentCreatedRepoWithLanguage="this.recentCreatedRepoWithLanguage?this.recentCreatedRepoWithLanguage:{}" :api = "this.api" />
  
</template>