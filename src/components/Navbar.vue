<script>
export default {
    name: "Navbar",
    props: {userData: Object, userReposData: {type: Array, required:true, default: () => []}, userStarredData: {type: Array, required:true, default: () => []},gitt:String, pageViewing: Number, pageViewType: String},
    data: function(){
        return {
            url: "https://api.github.com/users/",
            inputExtract: "",
            isSearching: false
        }
    },
    methods: {
        changePageTrigger(pageView,pageType){
            this.$emit('changePage', pageView, pageType);
        },
        fetchDataFromGitApi(){
            if(this.inputExtract.trim() === "") return;
            const xhttp = new XMLHttpRequest();
            const self = this
            xhttp.onreadystatechange = function(){
                if(this.readyState == 4 && this.status == 200){
                    let data = JSON.parse(this.responseText);
                    //console.log(data);
                    self.isSearching = true;
                    self.$emit('passUserData', data);

                }
                else if(this.readyState == 4){
                    console.log("Error: " + this.status);
                }
            }
            xhttp.open("GET", this.url + this.inputExtract);
            //console.log(this.gitt);
            xhttp.setRequestHeader("Authorization", "Bearer " + self.gitt);
            xhttp.send();  
        }
    }
}
</script>


<template>
<header class="AppHeader">
    <div class="AppHeader-globalBar  js-global-bar">
        <div class="AppHeader-globalBar-start">
            <button class="Button Button--iconOnly Button--secondary"><i class="fa fa-bars" aria-hidden="true"></i></button>
            <img src="../assets/images/icon.svg" width="32px" height="32px" alt="" srcset="">
            <input placeholder="search user..." v-model="inputExtract" class="search-input" type="text">
            <button @click="fetchDataFromGitApi()" class="Button Button--secondary test">sumbit</button>
        </div>


        <!-- <div class="AppHeader-globalBar-end">
            <div class="AppHeader-search">
                <button>yo</button>
            </div>
        </div> -->
    </div>
    <div v-if="isSearching" class="AppHeader-localBar">
        <nav aria-label="User" data-view-component="true" class="js-sidenav-container-pjax js-responsive-underlinenav overflow-hidden UnderlineNav">
            <ul data-view-component="true" class="UnderlineNav-body list-style-none">
                <li data-view-component="true" class="d-inline-flex">
                    <a v-if="pageViewing === 0" id="overview-tab" href="/a-x-r-o-n" data-tab-item="i0overview-tab" aria-current="page" data-view-component="true" @click.prevent="changePageTrigger(0,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-book UnderlineNav-octicon">
                    <path
                      d="M0 1.75A.75.75 0 0 1 .75 1h4.253c1.227 0 2.317.59 3 1.501A3.743 3.743 0 0 1 11.006 1h4.245a.75.75 0 0 1 .75.75v10.5a.75.75 0 0 1-.75.75h-4.507a2.25 2.25 0 0 0-1.591.659l-.622.621a.75.75 0 0 1-1.06 0l-.622-.621A2.25 2.25 0 0 0 5.258 13H.75a.75.75 0 0 1-.75-.75Zm7.251 10.324.004-5.073-.002-2.253A2.25 2.25 0 0 0 5.003 2.5H1.5v9h3.757a3.75 3.75 0 0 1 1.994.574ZM8.755 4.75l-.004 7.322a3.752 3.752 0 0 1 1.992-.572H14.5v-9h-3.495a2.25 2.25 0 0 0-2.25 2.25Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Overview</span>
                  <span title="Not available" data-view-component="true" class="Counter"></span>
                    </a>
                    <a v-else id="overview-tab" href="/a-x-r-o-n" data-tab-item="i0overview-tab" data-view-component="true" @click.prevent="changePageTrigger(0,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-book UnderlineNav-octicon">
                    <path
                      d="M0 1.75A.75.75 0 0 1 .75 1h4.253c1.227 0 2.317.59 3 1.501A3.743 3.743 0 0 1 11.006 1h4.245a.75.75 0 0 1 .75.75v10.5a.75.75 0 0 1-.75.75h-4.507a2.25 2.25 0 0 0-1.591.659l-.622.621a.75.75 0 0 1-1.06 0l-.622-.621A2.25 2.25 0 0 0 5.258 13H.75a.75.75 0 0 1-.75-.75Zm7.251 10.324.004-5.073-.002-2.253A2.25 2.25 0 0 0 5.003 2.5H1.5v9h3.757a3.75 3.75 0 0 1 1.994.574ZM8.755 4.75l-.004 7.322a3.752 3.752 0 0 1 1.992-.572H14.5v-9h-3.495a2.25 2.25 0 0 0-2.25 2.25Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Overview</span>
                  <span title="Not available" data-view-component="true" class="Counter"></span>
                    </a>
                </li>
                <li data-view-component="true" class="d-inline-flex">
                    <a v-if="pageViewing === 1" id="repositories-tab" href="/a-x-r-o-n?tab=repositories" aria-current="page" @click.prevent="changePageTrigger(1,`search`)" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-repo UnderlineNav-octicon">
                    <path
                      d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8ZM5 12.25a.25.25 0 0 1 .25-.25h3.5a.25.25 0 0 1 .25.25v3.25a.25.25 0 0 1-.4.2l-1.45-1.087a.249.249 0 0 0-.3 0L5.4 15.7a.25.25 0 0 1-.4-.2Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Repositories</span>
                  <span v-if="userReposData.length ===0" hidden="hidden" :title="`Bro has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}</span>
                  <span v-else  :title="`Bro has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}</span>
                    </a>
                    <a v-else id="repositories-tab" href="/a-x-r-o-n?tab=repositories" @click.prevent="changePageTrigger(1,`search`)" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-repo UnderlineNav-octicon">
                    <path
                      d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8ZM5 12.25a.25.25 0 0 1 .25-.25h3.5a.25.25 0 0 1 .25.25v3.25a.25.25 0 0 1-.4.2l-1.45-1.087a.249.249 0 0 0-.3 0L5.4 15.7a.25.25 0 0 1-.4-.2Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Repositories</span>
                  <span v-if="userReposData.length ===0" hidden="hidden" :title="`Bro has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}</span>
                  <span v-else  :title="`Bro has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}</span>
                    </a>
                </li>
                <!-- <li data-view-component="true" class="d-inline-flex">
                    <a v-if="pageViewing === 2" aria-current="page" id="projects-tab" href="/a-x-r-o-n?tab=projects" @click.prevent="changePageTrigger(2,`search`)" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                    data-view-component="true" class="octicon octicon-table UnderlineNav-octicon">
                    <path
                      d="M0 1.75C0 .784.784 0 1.75 0h12.5C15.216 0 16 .784 16 1.75v12.5A1.75 1.75 0 0 1 14.25 16H1.75A1.75 1.75 0 0 1 0 14.25ZM6.5 6.5v8h7.75a.25.25 0 0 0 .25-.25V6.5Zm8-1.5V1.75a.25.25 0 0 0-.25-.25H6.5V5Zm-13 1.5v7.75c0 .138.112.25.25.25H5v-8ZM5 5V1.5H1.75a.25.25 0 0 0-.25.25V5Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Projects</span>
                  <span title="0" hidden="hidden" data-view-component="true" class="Counter">0</span>
                    </a>
                    <a v-else id="projects-tab" href="/a-x-r-o-n?tab=projects" @click.prevent="changePageTrigger(2,`search`)" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                    data-view-component="true" class="octicon octicon-table UnderlineNav-octicon">
                    <path
                      d="M0 1.75C0 .784.784 0 1.75 0h12.5C15.216 0 16 .784 16 1.75v12.5A1.75 1.75 0 0 1 14.25 16H1.75A1.75 1.75 0 0 1 0 14.25ZM6.5 6.5v8h7.75a.25.25 0 0 0 .25-.25V6.5Zm8-1.5V1.75a.25.25 0 0 0-.25-.25H6.5V5Zm-13 1.5v7.75c0 .138.112.25.25.25H5v-8ZM5 5V1.5H1.75a.25.25 0 0 0-.25.25V5Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Projects</span>
                  <span title="0" hidden="hidden" data-view-component="true" class="Counter">0</span>
                    </a>
                </li>
                <li data-view-component="true" class="d-inline-flex">
                <a v-if="pageViewing === 3" aria-current="page" id="packages-tab" href="/a-x-r-o-n?tab=packages" @click.prevent="changePageTrigger(3,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-package UnderlineNav-octicon">
                    <path
                      d="m8.878.392 5.25 3.045c.54.314.872.89.872 1.514v6.098a1.75 1.75 0 0 1-.872 1.514l-5.25 3.045a1.75 1.75 0 0 1-1.756 0l-5.25-3.045A1.75 1.75 0 0 1 1 11.049V4.951c0-.624.332-1.201.872-1.514L7.122.392a1.75 1.75 0 0 1 1.756 0ZM7.875 1.69l-4.63 2.685L8 7.133l4.755-2.758-4.63-2.685a.248.248 0 0 0-.25 0ZM2.5 5.677v5.372c0 .09.047.171.125.216l4.625 2.683V8.432Zm6.25 8.271 4.625-2.683a.25.25 0 0 0 .125-.216V5.677L8.75 8.432Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Packages</span>
                  <span title="0" hidden="hidden" data-view-component="true" class="Counter">0</span>
                </a>
                <a v-else id="packages-tab" href="/a-x-r-o-n?tab=packages" @click.prevent="changePageTrigger(3,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-package UnderlineNav-octicon">
                    <path
                      d="m8.878.392 5.25 3.045c.54.314.872.89.872 1.514v6.098a1.75 1.75 0 0 1-.872 1.514l-5.25 3.045a1.75 1.75 0 0 1-1.756 0l-5.25-3.045A1.75 1.75 0 0 1 1 11.049V4.951c0-.624.332-1.201.872-1.514L7.122.392a1.75 1.75 0 0 1 1.756 0ZM7.875 1.69l-4.63 2.685L8 7.133l4.755-2.758-4.63-2.685a.248.248 0 0 0-.25 0ZM2.5 5.677v5.372c0 .09.047.171.125.216l4.625 2.683V8.432Zm6.25 8.271 4.625-2.683a.25.25 0 0 0 .125-.216V5.677L8.75 8.432Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Packages</span>
                  <span title="0" hidden="hidden" data-view-component="true" class="Counter">0</span>
                </a>
              </li> -->
              <li data-view-component="true" class="d-inline-flex">
                <a v-if="pageViewing === 4" aria-current="page" id="stars-tab" href="/a-x-r-o-n?tab=stars" @click.prevent="changePageTrigger(4,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                    data-view-component="true" class="octicon octicon-star UnderlineNav-octicon">
                    <path
                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Stars</span>
                  <span v-if="userStarredData.length === 0" title="1" hidden="hidden" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}</span>
                  <span v-else title="1" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}</span>
                </a>
                <a v-else id="stars-tab" href="/a-x-r-o-n?tab=stars" @click.prevent="changePageTrigger(4,`search`)" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                    data-view-component="true" class="octicon octicon-star UnderlineNav-octicon">
                    <path
                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Stars</span>
                  <span v-if="userStarredData.length === 0" title="1" hidden="hidden" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}</span>
                  <span v-else title="1" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}</span>
                </a>
              </li>
            </ul>
        </nav>
    </div>
</header>
</template>


<style scoped>



.AppHeader {
    --AppHeader-bg: var(--bg-inner);
    color: var(--text);
    background: var(--AppHeader-bg);
    box-shadow: inset 0 calc(var(--borderWidth-thin, 1px)*-1) var(--borderColor-default)
}

.AppHeader .AppHeader-globalBar {
    display: flex;
    padding: var(--base-size-16, var(--base-size-16));
    gap: var(--base-size-12, 12px)
}

.AppHeader .AppHeader-globalBar.search-expanded .AppHeader-globalBar-start,
.AppHeader .AppHeader-globalBar.always-expanded .AppHeader-globalBar-start {
    flex: none
}

.AppHeader .AppHeader-globalBar .AppHeader-globalBar-start {
    flex: 1 1 auto;
    display: flex;
    gap: var(--base-size-8, 8px)
}


.AppHeader .AppHeader-globalBar.search-expanded .AppHeader-globalBar-end,
.AppHeader .AppHeader-globalBar.always-expanded .AppHeader-globalBar-end {
    flex: 1 1 auto
}

.AppHeader .AppHeader-globalBar .AppHeader-globalBar-end {
    flex: 0 1 auto;
    display: flex;
    justify-content: flex-end;
    gap: var(--controlStack-medium-gap-auto, 8px);
    max-height: calc(var(--base-size-32, 32px))
}

.Button {
    align-items: center;
    background-color: initial;
    border: var(--borderWidth-thin) solid;
    border-color: #0000;
    border-radius: var(--borderRadius-medium);
    color: var(--button-default-fgColor-rest);
    cursor: pointer;
    display: inline-flex;
    flex-direction: row;
    font-size: var(--text-body-size-medium);
    font-weight: var(--base-text-weight-medium);
    gap: var(--base-size-4);
    height: var(--control-medium-size);
    justify-content: space-between;
    min-width: max-content;
    padding: 0 var(--control-medium-paddingInline-normal);
    position: relative;
    text-align: center;
    transition: var(--duration-fast) var(--easing-easeInOut);
    transition-property: color, fill, background-color, border-color;
    -webkit-user-select: none;
    user-select: none
}

.Button.Button--iconOnly {
    color: var(--fgColor-muted)
}

.Button--secondary {
    color: var(--button-default-fgColor-rest);
    fill: var(--fgColor-muted);
    background-color: var(--button-default-bgColor);
    border-color: var(--button-default-borderColor-rest);
    box-shadow: var(--button-default-shadow-resting), var(--button-default-shadow-inset)
}

.Button--secondary:hover:not(:disabled,
.Button--inactive) {
    background-color: var(--button-default-bgColor-hover);
    border-color: var(--button-default-borderColor-hover)
}

.Button--secondary:active:not(:disabled) {
    background-color: var(--button-default-bgColor-active);
    border-color: var(--button-default-borderColor-active)
}

.Button--secondary[aria-pressed=true] {
    background-color: var(--button-default-bgColor-selected);
    box-shadow: var(--shadow-inset)
}

.Button--secondary:disabled,
.Button--secondary[aria-disabled=true] {
    color: var(--control-fgColor-disabled);
    fill: var(--control-fgColor-disabled);
    background-color: var(--button-default-bgColor-disabled);
    border-color: var(--button-default-borderColor-disabled)
}

.AppHeader .AppHeader-globalBar.second-row .AppHeader-search {
    display: block
}

.AppHeader .AppHeader-globalBar.search-expanded .AppHeader-search .AppHeader-search-whenRegular,
.AppHeader .AppHeader-globalBar.always-expanded .AppHeader-search .AppHeader-search-whenRegular {
    max-width: 100%
}

.AppHeader .AppHeader-globalBar .AppHeader-search {
    position: relative;
    display: flex;
    flex: 1 1 auto;
    justify-content: flex-end
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-whenRegular {
    min-width: 12rem;
    max-width: 24rem;
    flex: 1 1 auto
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-wrap {
    display: grid
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-wrap.AppHeader-search-wrap--hasTrailing input[type=search] {
    padding-inline-end: calc(var(--control-medium-paddingInline-condensed, 8px) + var(--base-size-16, 16px) + var(--control-medium-gap, 8px) - var(--borderWidth-thin, 1px))
}

.AppHeader .AppHeader-globalBar .AppHeader-search .search-input-container {
    height: auto
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-kbd {
    display: inline-grid;
    width: var(--base-size-16, 16px);
    height: var(--base-size-16, 16px);
    padding: 0;
    font-size: var(--text-caption-size, 12px);
    line-height: var(--text-caption-lineHeight, 1.3333333333);
    color: inherit;
    vertical-align: baseline;
    background: var(--bgColor-transparent);
    border: var(--borderWidth-thin) solid var(--fgColor-muted);
    border-radius: var(--borderRadius-small);
    box-shadow: none;
    align-items: center;
    justify-content: center
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-placeholder {
    display: block;
    width: 100%;
    overflow: hidden;
    font-weight: var(--base-text-weight-normal, 400);
    line-height: var(--text-body-lineHeight-medium, 20px);
    color: var(--fgColor-muted);
    text-overflow: ellipsis;
    white-space: nowrap;
    pointer-events: none;
    grid-area: 1/1;
    padding-block: var(--control-medium-paddingBlock, 6px);
    padding-inline: calc(var(--control-medium-paddingInline-condensed, 8px) + var(--base-size-16, 16px) + var(--control-medium-gap, 8px))
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-control {
    grid-area: 1/1;
    position: relative
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-control-overflow {
    overflow: hidden
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-visual--leading {
    position: absolute;
    top: var(--base-size-8, var(--base-size-8));
    left: var(--base-size-8, var(--base-size-8));
    display: block;
    width: var(--base-size-16, 16px);
    height: var(--base-size-16, 16px);
    color: var(--fgColor-muted);
    pointer-events: none
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-visual--leading svg {
    display: block !important
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-searchButton {
    background: transparent
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search],
.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-searchButton {
    width: 100%;
    border: solid var(--borderWidth-thin) var(--button-default-borderColor-rest);
    transition: none;
    padding-block: calc(var(--control-medium-paddingBlock, 6px) - var(--borderWidth-thin, 1px));
    padding-inline: calc(var(--control-medium-paddingInline-condensed, 8px) + var(--base-size-16, 16px) + var(--control-medium-gap, 8px) - var(--borderWidth-thin, 1px))
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:placeholder-shown {
    background: transparent
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:not(:placeholder-shown) {
    background: var(--bgColor-default)
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]::placeholder {
    color: transparent;
    opacity: 1
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:focus {
    background: var(--bgColor-default)
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:focus::placeholder {
    color: var(--fgColor-muted)
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:focus:placeholder {
    color: var(--fgColor-muted);
    opacity: 1
}

.AppHeader .AppHeader-globalBar .AppHeader-search input[type=search]:focus-visible {
    border-color: var(--focus-outlineColor)
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing {
    position: absolute;
    top: var(--base-size-4, var(--base-size-4));
    right: var(--base-size-4, var(--base-size-4));
    display: grid;
    width: var(--control-xsmall-size, 24px);
    height: var(--control-xsmall-size, 24px);
    padding: 0;
    color: var(--fgColor-muted);
    background: var(--bgColor-transparent);
    border: 0;
    border-radius: var(--borderRadius-small);
    align-items: center;
    justify-content: center
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing:hover {
    background: var(--control-transparent-bgColor-hover)
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing:active {
    background: var(--control-transparent-bgColor-active)
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing::before {
    position: absolute;
    top: calc((var(--control-xsmall-size, var(--base-size-24)) - var(--base-size-16, var(--base-size-16)))/2);
    left: calc(var(--base-size-4, var(--base-size-4))*-1);
    display: block;
    width: var(--borderWidth-thin, 1px);
    height: var(--base-size-16, 16px);
    content: "";
    background: var(--borderColor-default)
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing::after {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100%;
    height: 100%;
    min-height: var(--control-medium-size, 32px);
    content: "";
    transform: translateX(-50%) translateY(-50%);
    min-width: var(--control-medium-size, 32px)
}

@media(pointer: coarse) {
    .AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing::after {
        min-width: var(--control-minTarget-coarse, 44px);
        min-height: var(--control-minTarget-coarse, 44px)
    }
}

.AppHeader .AppHeader-globalBar .AppHeader-search .AppHeader-search-action--trailing svg {
    color: inherit
}
.AppHeader .AppHeader-localBar {
    padding: 0 var(--base-size-16, var(--base-size-16))
}

.search-input {
    width: 60%;
    border-radius: var(--borderRadius-medium);
    background-color: var(--bg-inner);
    border: var(--borderWidth-thin) solid var(--borderColor-default);
    padding: 0 10px;
    color: var(--text-muted);
}

.search-input:focus{
    border-color: var(--focus-outlineColor);
}
.test{
    color: var(--borderColor-default);
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: center;
}
.pinned-item-list-item .pinned-item-handle {
    color: var(--fgColor-muted, var(--color-fg-muted))
}

.pinned-item-list-item .pinned-item-handle:hover {
    cursor: grab
}

.pinned-item-list-item.is-dragging,
.pinned-item-list-item.is-dragging .pinned-item-handle {
    cursor: grabbing
}

.pinned-item-list-item.is-dragging {
    background-color: var(--bgColor-accent-muted, var(--color-accent-subtle))
}

.pinned-item-list-item.sortable-ghost {
    background-color: var(--bgColor-accent-muted, var(--color-accent-subtle));
    opacity: 0
}

.pinned-item-list-item.empty {
    border-style: dashed;
    border-width: var(--borderWidth-thin);
    align-items: center;
    justify-content: center
}

.pinned-item-list-item-content {
    display: flex;
    width: 100%;
    flex-direction: column
}

.pinned-item-desc {
    flex: 1 0 auto
}

.pinned-item-meta {
    display: inline-block
}

.pinned-item-meta+.pinned-item-meta {
    margin-left: var(--base-size-16)
}

.achievement-badge-sidebar {
    filter: drop-shadow(var(--shadow-floating-large, var(--color-shadow-large)))
}

.achievement-badge-card {
    width: 96px;
    margin: var(--base-size-4);
    filter: drop-shadow(var(--shadow-floating-large, var(--color-shadow-large)))
}

@media(min-width: 1012px) {
    .achievement-badge-card {
        width: 128px
    }
}

.achievement-tier-label {
    color: var(--fgColor-black, var(--color-scale-gray-9))
}

.achievement-tier-label--bronze {
    background-color: #f9bfa7;
    border-color: #f9bfa7
}

.achievement-tier-label--silver {
    background-color: #e1e4e4;
    border-color: #e1e4e4
}

.achievement-tier-label--gold {
    background-color: #fae57e;
    border-color: #fae57e
}

.achievement-card {
    box-shadow: var(--shadow-resting-medium, var(--color-shadow-medium));
    transition: .4s ease
}

.achievement-card:hover {
    box-shadow: var(--shadow-floating-large, var(--color-shadow-large))
}

.achievement-card-unseen {
    box-shadow: 0 3px 6px var(--borderColor-accent-muted, var(--color-accent-subtle))
}

.achievement-badges .tier-badge {
    padding: 0;
    border: 0
}

.achievement-badges-flip {
    position: relative;
    transform-style: preserve-3d;
    width: 140px;
    height: 140px
}

.achievement-badges-flip .tier-badge {
    position: absolute;
    top: 0;
    left: 0;
    backface-visibility: hidden;
    opacity: 0
}

.achievement-badges-flip .tier-badge--back {
    transform: rotateY(180deg)
}

.achievement-badges-flip .tier-badge:first-child,
.achievement-badges-flip .tier-badge:nth-child(2) {
    opacity: 1
}

.achievement-detail-close {
    width: var(--base-size-32);
    height: var(--base-size-32)
}

.achievement-history {
    margin-bottom: calc(var(--base-size-16)*-1)
}

.achievement-history .achievement-history-unlocked-at::before {
    top: var(--base-size-24)
}

.achievement-history .achievement-history-tier:last-child::before {
    bottom: var(--base-size-40)
}

.ContributionCalendar.days-selected .ContributionCalendar-day {
    opacity: .5
}

.ContributionCalendar.days-selected .ContributionCalendar-day.active {
    opacity: 1
}

.ContributionCalendar-grid {
    width: max-content;
    border-collapse: separate
}

.ContributionCalendar-label {
    padding: .125em .5em .125em 0;
    font-size: 12px;
    font-weight: var(--base-text-weight-normal, 400);
    color: var(--fgColor-default);
    text-align: left;
    fill: var(--fgColor-default)
}

.ContributionCalendar-day-private-profile {
    fill: var(--bgColor-muted);
    background-color: var(--bgColor-muted)
}

.ContributionCalendar-day,
.ContributionCalendar-day[data-level="0"] {
    fill: var(--contribution-default-bgColor-0);
    shape-rendering: geometricPrecision;
    background-color: var(--contribution-default-bgColor-0);
    border-radius: 2px;
    border: .5px solid var(--contribution-default-borderColor-0)
}

@media(forced-colors: active) {

    .ContributionCalendar-day,
    .ContributionCalendar-day[data-level="0"] {
        --color-calendar-graph-day-bg: Canvas;
        border: none;
        forced-color-adjust: none
    }
}

.ContributionCalendar-day[data-level]:focus {
    outline: 2px solid var(--focus-outlineColor);
    outline-offset: -1px
}

.ContributionCalendar-day[data-level="1"] {
    fill: var(--contribution-default-bgColor-1);
    background-color: var(--contribution-default-bgColor-1);
    border-color: var(--contribution-default-borderColor-1)
}

@media(forced-colors: active) {
    .ContributionCalendar-day[data-level="1"] {
        background: radial-gradient(ellipse at center, CanvasText 0%, CanvasText 15%, Canvas 15%, CanvasText 15%, Canvas 15%, Canvas 100%)
    }
}

.ContributionCalendar-day[data-level="2"] {
    fill: var(--contribution-default-bgColor-2);
    background-color: var(--contribution-default-bgColor-2);
    border-color: var(--contribution-default-borderColor-2)
}

@media(forced-colors: active) {
    .ContributionCalendar-day[data-level="2"] {
        background: radial-gradient(ellipse at center, CanvasText 0%, CanvasText 35%, Canvas 35%, CanvasText 35%, Canvas 35%, Canvas 100%)
    }
}

.ContributionCalendar-day[data-level="3"] {
    fill: var(--contribution-default-bgColor-3);
    background-color: var(--contribution-default-bgColor-3);
    border-color: var(--contribution-default-borderColor-3)
}

@media(forced-colors: active) {
    .ContributionCalendar-day[data-level="3"] {
        background: radial-gradient(ellipse at center, CanvasText 0%, CanvasText 55%, Canvas 55%, CanvasText 55%, Canvas 55%, Canvas 100%)
    }
}

.ContributionCalendar-day[data-level="4"] {
    fill: var(--contribution-default-bgColor-4);
    background-color: var(--contribution-default-bgColor-4);
    border-color: var(--contribution-default-borderColor-4)
}

@media(forced-colors: active) {
    .ContributionCalendar-day[data-level="4"] {
        background: radial-gradient(ellipse at center, CanvasText 0%, CanvasText 75%, Canvas 75%, CanvasText 75%, Canvas 75%, Canvas 100%)
    }
}

.ContributionCalendar[data-holiday=halloween] .ContributionCalendar-day[data-level="1"] {
    fill: var(--contribution-halloween-bgColor-1);
    background-color: var(--contribution-halloween-bgColor-1)
}

.ContributionCalendar[data-holiday=halloween] .ContributionCalendar-day[data-level="2"] {
    fill: var(--contribution-halloween-bgColor-2);
    background-color: var(--contribution-halloween-bgColor-2)
}

.ContributionCalendar[data-holiday=halloween] .ContributionCalendar-day[data-level="3"] {
    fill: var(--contribution-halloween-bgColor-3);
    background-color: var(--contribution-halloween-bgColor-3)
}

.ContributionCalendar[data-holiday=halloween] .ContributionCalendar-day[data-level="4"] {
    fill: var(--contribution-halloween-bgColor-4);
    background-color: var(--contribution-halloween-bgColor-4)
}

.ContributionCalendar[data-holiday=winter] .ContributionCalendar-day[data-level="1"] {
    fill: var(--contribution-winter-bgColor-1);
    background-color: var(--contribution-winter-bgColor-1)
}

.ContributionCalendar[data-holiday=winter] .ContributionCalendar-day[data-level="2"] {
    fill: var(--contribution-winter-bgColor-2);
    background-color: var(--contribution-winter-bgColor-2)
}

.ContributionCalendar[data-holiday=winter] .ContributionCalendar-day[data-level="3"] {
    fill: var(--contribution-winter-bgColor-3);
    background-color: var(--contribution-winter-bgColor-3)
}

.ContributionCalendar[data-holiday=winter] .ContributionCalendar-day[data-level="4"] {
    fill: var(--contribution-winter-bgColor-4);
    background-color: var(--contribution-winter-bgColor-4)
}

.graph-before-activity-overview {
    border-top-left-radius: var(--borderRadius-medium);
    border-top-right-radius: var(--borderRadius-medium)
}

.activity-overview-box {
    border-top-left-radius: 0;
    border-top-right-radius: 0
}

.contribution-activity .select-menu-button {
    position: relative;
    top: -4px
}

.contribution-activity.loading .contribution-activity-listing {
    display: none
}

.contribution-activity.loading .contribution-activity-show-more {
    display: none
}

.contribution-activity.loading .contribution-activity-spinner {
    display: block
}

.contribution-activity-spinner {
    display: none
}

li.contribution {
    padding: var(--base-size-8) 0;
    list-style: none
}

li.contribution h3 {
    display: inline-block;
    margin: 0;
    font-size: 14px
}

li.contribution .cmeta {
    display: block;
    font-size: 12px
}

li.contribution .d {
    color: var(--fgColor-default)
}

li.contribution .a {
    color: var(--fgColor-default)
}

li.contribution .num {
    color: var(--fgColor-muted)
}

.user-profile-sticky-bar::after {
    height: 48px
}

.user-profile-sticky-bar {
    position: fixed;
    top: 0;
    z-index: 90;
    width: 233px;
    word-break: break-all;
    pointer-events: none;
    opacity: 0;
    transition: .2s
}

.user-profile-sticky-bar.is-stuck {
    pointer-events: auto;
    opacity: 1
}

.user-profile-nav .UnderlineNav-item {
    margin-right: 0 !important;
    line-height: 30px;
    white-space: nowrap
}

.user-profile-nav {
    background-color: var(--bgColor-default, var(--color-canvas-default));
    border-bottom: var(--borderWidth-thin) solid var(--borderColor-default, var(--color-border-default));
    box-shadow: none
}

.user-profile-nav.is-stuck {
    z-index: 90
}

.user-profile-mini-vcard {
    position: relative;
    top: 1px;
    z-index: 110;
    height: 48px
}

.user-profile-mini-avatar {
    width: 32px
}

.page-profile .news {
    float: none;
    width: auto
}

.mini-follow-button {
    padding: 0 var(--base-size-8);
    line-height: 1.5;
    opacity: 0;
    transition: opacity .2s
}

.is-follow-stuck .mini-follow-button {
    opacity: 1
}

.user-status-circle-badge-container {
    position: absolute;
    bottom: 0;
    left: 100%;
    z-index: 2;
    width: 38px;
    height: 38px;
    margin-bottom: var(--base-size-32);
    margin-left: calc(var(--base-size-40)*-1)
}

.user-status-circle-badge-container .user-status-emoji-container {
    width: 20px;
    height: 20px;
    margin-right: 0 !important
}

.user-status-circle-badge-container .user-status-message-wrapper {
    width: 0;
    padding-top: 0 !important;
    overflow: hidden;
    line-height: 20px;
    opacity: 0;
    transition: .1s ease
}

.user-status-circle-badge-container .user-status-busy {
    background-color: var(--bgColor-default, var(--color-canvas-default)) !important;
    background-image: linear-gradient(var(--bgColor-attention-muted, var(--bgColor-attention-muted, var(--color-attention-subtle))), var(--color-attention-subtle))
}

.user-status-circle-badge-container.user-status-editable:focus-within,
.user-status-circle-badge-container.user-status-has-content:focus-within,
.user-status-circle-badge-container.user-status-editable:hover,
.user-status-circle-badge-container.user-status-has-content:hover {
    width: max-content;
    max-width: 544px
}

.user-status-circle-badge-container.user-status-editable:focus-within .user-status-emoji-container,
.user-status-circle-badge-container.user-status-has-content:focus-within .user-status-emoji-container,
.user-status-circle-badge-container.user-status-editable:hover .user-status-emoji-container,
.user-status-circle-badge-container.user-status-has-content:hover .user-status-emoji-container {
    margin-right: var(--base-size-8) !important
}

.user-status-circle-badge-container.user-status-editable:focus-within .user-status-message-wrapper,
.user-status-circle-badge-container.user-status-has-content:focus-within .user-status-message-wrapper,
.user-status-circle-badge-container.user-status-editable:hover .user-status-message-wrapper,
.user-status-circle-badge-container.user-status-has-content:hover .user-status-message-wrapper {
    width: 100%;
    opacity: 1
}

.user-status-circle-badge-container.user-status-editable:focus-within .user-status-circle-badge,
.user-status-circle-badge-container.user-status-has-content:focus-within .user-status-circle-badge,
.user-status-circle-badge-container.user-status-editable:hover .user-status-circle-badge,
.user-status-circle-badge-container.user-status-has-content:hover .user-status-circle-badge {
    box-shadow: var(--shadow-resting-medium, var(--color-shadow-medium))
}

.user-status-circle-badge-container .user-status-message-wrapper .team-mention,
.user-status-circle-badge-container .user-status-message-wrapper .user-mention {
    white-space: nowrap
}

.vcard-names-container {
    position: sticky;
    top: 0
}

.vcard-names-container.is-stuck {
    pointer-events: none
}

.vcard-names-container.is-stuck .vcard-names {
    opacity: 0
}

.vcard-names-container.is-stuck::after {
    opacity: 1
}

.vcard-names {
    line-height: 1
}

.vcard-details {
    display: flex;
    list-style: none;
    flex-direction: column;
    gap: var(--base-size-4)
}

.vcard-detail {
    display: flex;
    align-items: flex-start;
    gap: var(--base-size-8);
    font-size: 14px
}

.vcard-detail .octicon {
    width: 16px;
    color: var(--fgColor-muted, var(--color-fg-muted));
    text-align: center;
    transform: translateY(3px)
}

.user-profile-bio {
    overflow: hidden;
    font-size: 14px
}

</style>