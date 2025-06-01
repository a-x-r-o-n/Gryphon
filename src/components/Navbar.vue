<script>
export default {
    name: "Navbar",
    data: function(){
        return {
            url: "https://api.github.com/users/",
            inputExtract: ""
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
            <img src="../assets/images/image.png" width="32px" height="32px" alt="" srcset="">
            <input placeholder="search user..." v-model="inputExtract" class="search-input" type="text">
            <button @click="fetchDataFromGitApi()" class="Button Button--secondary test">sumbit</button>
        </div>


        <!-- <div class="AppHeader-globalBar-end">
            <div class="AppHeader-search">
                <button>yo</button>
            </div>
        </div> -->
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