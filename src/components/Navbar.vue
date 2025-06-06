<script>
export default {
    name: "Navbar",
    props: {userData: Object, userReposData: {type: Array, required:true, default: () => []}, userStarredData: {type: Array, required:true, default: () => []}},
    data: function(){
        return {
            url: "https://api.github.com/users/",
            inputExtract: "",
            isSearching: false
        }
    },
    methods: {
        
        fetchDataFromGitApi(){
            if(this.inputExtract.trim() === "") return;
            const xhttp = new XMLHttpRequest();
            const self = this
            xhttp.onreadystatechange = function(){
                if(this.readyState == 4 && this.status == 200){
                    let data = JSON.parse(this.responseText);
                    console.log(data);
                    self.isSearching = true;
                    self.$emit('passUserData', data);

                }
                else if(this.readyState == 4){
                    console.log("Error: " + this.status);
                }
            }
            xhttp.open("GET", this.url + this.inputExtract);
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
                    <a id="overview-tab" href="/soniyav20" data-tab-item="i0overview-tab" aria-current="page" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
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
                    <a id="repositories-tab" href="/soniyav20?tab=repositories" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                        <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-repo UnderlineNav-octicon">
                    <path
                      d="M2 2.5A2.5 2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0 1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 1v6.708A2.486 2.486 0 0 1 4.5 9h8ZM5 12.25a.25.25 0 0 1 .25-.25h3.5a.25.25 0 0 1 .25.25v3.25a.25.25 0 0 1-.4.2l-1.45-1.087a.249.249 0 0 0-.3 0L5.4 15.7a.25.25 0 0 1-.4-.2Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Repositories</span>
                  <span v-if="userReposData.length ===0" hidden="hidden" :title="`MF has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}</span>
                  <span v-else  :title="`MF has ${userReposData?userReposData.length:0} repositories`" data-view-component="true" class="Counter">{{ userReposData?userReposData.length:0 }}{{ console.log("log at Navbar.vue: \n",userReposData) }}</span>
                    </a>
                </li>
                <li data-view-component="true" class="d-inline-flex">
                    <a id="projects-tab" href="/soniyav20?tab=projects" data-view-component="true" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
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
                <a id="packages-tab" href="/soniyav20?tab=packages" class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-package UnderlineNav-octicon">
                    <path
                      d="m8.878.392 5.25 3.045c.54.314.872.89.872 1.514v6.098a1.75 1.75 0 0 1-.872 1.514l-5.25 3.045a1.75 1.75 0 0 1-1.756 0l-5.25-3.045A1.75 1.75 0 0 1 1 11.049V4.951c0-.624.332-1.201.872-1.514L7.122.392a1.75 1.75 0 0 1 1.756 0ZM7.875 1.69l-4.63 2.685L8 7.133l4.755-2.758-4.63-2.685a.248.248 0 0 0-.25 0ZM2.5 5.677v5.372c0 .09.047.171.125.216l4.625 2.683V8.432Zm6.25 8.271 4.625-2.683a.25.25 0 0 0 .125-.216V5.677L8.75 8.432Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Packages</span>
                  <span title="0" hidden="hidden" data-view-component="true" class="Counter">0</span>
                </a>
              </li>
              <li data-view-component="true" class="d-inline-flex">
                <a id="stars-tab" href="/soniyav20?tab=stars"class="UnderlineNav-item no-wrap js-responsive-underlinenav-item js-selected-navigation-item">
                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                    data-view-component="true" class="octicon octicon-star UnderlineNav-octicon">
                    <path
                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                    </path>
                  </svg>
                  <span data-view-component="true">Stars</span>
                  <span v-if="userStarredData.length === 0" title="1" hidden="hidden" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}{{ console.log("log at Navbar.vue: \n",userStarredData) }}</span>
                  <span v-else title="1" data-view-component="true" class="Counter">{{ userStarredData?userStarredData.length:0 }}{{ console.log("log at Navbar.vue: \n",userStarredData) }}</span>
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
}
</style>