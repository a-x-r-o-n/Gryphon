<script>

import Navbar from "./components/Navbar.vue";
import SearchDisplayer from "./components/SearchDisplayer.vue";

export default {
  name: "App",
  data: function(){
    return {
      userData: null,
      userUrl: `https://api.github.com/users/${this.userData?this.userData:''}`,
      userRepos: this.userData?(this.userUrl+'/repos'):'',
    }
  },
  methods: {
    bindUserData(data){
      console.log("Method Ativated");
      this.userData = data;
    }
  },
  components: {
    Navbar,SearchDisplayer
  },
};
</script>


<template>
  <Navbar @passUserData="bindUserData"/>
  <SearchDisplayer :userData="this.userData"/>
  
</template>