<script>
import "../assets/main.css";
export default {
    name: "SearchDisplayer",
    props: {userData:Object,userReposData:{type:Array,default: () => {}},recentCreatedRepo:{type:Array,default: () => {}},recentCreatedRepoWithLanguage:{type:Object,default: () => {}}, gitt:String, pageViewing:Number, pageViewType:String}, 
    data: function () {
        return {
            languageFrameworkColors : {
                "javascript": "#f1e05a",
                "nix":"#7e7eff",
                "lean":"#000",
                "python": "#3572A5",
                "java": "#b07219",
                "c++": "#f34b7d",
                "c": "#555555",
                "c#": "#178600",
                "go": "#00ADD8",
                "ruby": "#701516",
                "php": "#4F5D95",
                "typescript": "#3178c6",
                "swift": "#ffac45",
                "kotlin": "#A97BFF",
                "objective-c": "#438eff",
                "shell": "#89e051",
                "html": "#e34c26",
                "css": "#563d7c",
                "dart": "#00B4AB",
                "rust": "#dea584",
                "scala": "#c22d40",
                "perl": "#0298c3",
                "haskell": "#5e5086",
                "r": "#198CE7",
                "clojure": "#db5855",
                "elixir": "#6e4a7e",
                "lua": "#000080",
                "assembly": "#6E4C13",
                "matlab": "#e16737",
                "powershell": "#012456",
                "dockerfile": "#384d54",
                "makefile": "#427819",
                // Frameworks
                "vue": "#41B883",
                "react": "#61DAFB",
                "angular": "#DD0031",
                "django": "#092E20",
                "flask": "#000000",
                "laravel": "#FF2D20",
                "spring": "#6DB33F",
                "express": "#000000",
                "ruby on rails": "#CC0000",
                "asp.net": "#512BD4"
            }

        }
    },
    methods: {
        getImageUrl(path) {
            return new URL(path, import.meta.url).href;
        },
        displayDescriptionTOPinnedRepos(description="",numChars=220){
            if(description.length>220){
                let des = "";
                for(let iterator = 0;iterator<=numChars;iterator++){
                    if(description.length === iterator+1) break;
                    des+=description[iterator];
                }
                des+= "...";
                return des;
            }
            else{
                return description;
            }
        },
        formatDate(dateString) {
  const date = new Date(dateString);
  const options = { month: 'short', day: 'numeric', year: 'numeric' };
  const formatted = date.toLocaleDateString('en-US', options);
  
  const [monthDay, year] = formatted.split(', ');
  return `${monthDay},\n${year}`;
}

    }
}
</script>

<template>
    <div class="application-main ">
        <main>
            <div class="container-xl px-3 px-md-4 px-lg-5 mt-2">
                <div v-if="this.userData"
                    class="Layout Layout--flowRow-until-md Layout--sidebarPosition-start Layout--sidebarPosition-flowRow-start">
                    <div class="Layout-sidebar">
                        <div class="h-card mt-5">
                            <div class="js-profile-editable-replace">
                                <div class="clearfix d-flex d-md-block flex-items-center mb-4 mb-md-0">
                                    <div class="position-relative d-inline-block col-2 col-md-12 mr-3 mr-md-0 flex-shrink-0"
                                        style="z-index:4;">
                                        <a :href="this.userData?getImageUrl(this.userData['avatar_url']): getImageUrl('https://avatars.githubusercontent.com/u/88935039?v=4')">
                                            <img style="height:auto;" alt="View a-x-r-o-n&#39;s full-sized avatar"
                                                :src="this.userData?getImageUrl(this.userData['avatar_url']): getImageUrl('https://avatars.githubusercontent.com/u/88935039?v=4')" width="260"
                                                height="260"
                                                class="avatar avatar-user width-full border color-bg-default" />
                                        </a>

                                    </div>
                                    <div class="vcard-names-container float-left js-profile-editable-names col-12 py-3">
                                        <h1 class="vcard-names ">
                                            <span class="p-name vcard-fullname d-block overflow-hidden" itemprop="name">

                                            </span>
                                            <span class="p-nickname vcard-username d-block" itemprop="additionalName">
                                                {{userData?userData["login"]:"Search Name"}}

                                            </span>
                                        </h1>

                                    </div>
                                </div>
                                <div class="d-flex flex-column">
                                    <div class="flex-order-1 flex-md-order-none">
                                        <div class="d-flex flex-lg-row flex-md-column">
                                            <div class="flex-1 mb-3 mb-md-3">
                                                <div class="js-sticky js-user-profile-follow-button pb-1 mb-n1">
                                                </div>

                                                <span class="user-following-container js-form-toggle-container">

                                                    <form class="js-form-toggle-target"
                                                        data-sr-feedback="You are following a-x-r-o-n"
                                                        data-turbo="false" action="/users/follow?target=a-x-r-o-n"
                                                        accept-charset="UTF-8" method="post"><input type="hidden"
                                                            name="authenticity_token"
                                                            value="lDenOhM6oQaZdYh4_5wJ8rj0YIiP-v1cU4o6feIYQlIF3zKazAPhAvXEjltyLSkjqLQAQcMeLwC5-P2pqY41Og" />
                                                        <input type="submit" name="commit" value="Follow"
                                                            class="btn btn-block" title="Follow a-x-r-o-n"
                                                            aria-label="Follow a-x-r-o-n"
                                                            data-hydro-click="{&quot;event_type&quot;:&quot;user_profile.click&quot;,&quot;payload&quot;:{&quot;profile_user_id&quot;:88935039,&quot;target&quot;:&quot;FOLLOW_BUTTON&quot;,&quot;user_id&quot;:121759085,&quot;originating_url&quot;:&quot;https://github.com/a-x-r-o-n&quot;}}"
                                                            data-hydro-click-hmac="038c29990b24aef83ff643f4d42eb9b4c2d0f25b3cfb651f1a3d2cd99214100a"
                                                            data-disable-with="Follow" />
                                                    </form>

                                                    <form class="js-form-toggle-target" hidden="hidden"
                                                        data-sr-feedback="You are unfollowing a-x-r-o-n"
                                                        data-turbo="false" action="/users/unfollow?target=a-x-r-o-n"
                                                        accept-charset="UTF-8" method="post"><input type="hidden"
                                                            name="authenticity_token"
                                                            value="5X4pGiqJfma2aJPND_GEcu5WnMb313AcmqQpg9k1kf2xMK0WdPLp7C1UqSK8b2aZvba_OCX15rS1U7r2FiwS2A" />
                                                        <input type="submit" name="commit" value="Unfollow"
                                                            class="btn btn-block" data-disable-with="Unfollow"
                                                            title="Unfollow a-x-r-o-n"
                                                            aria-label="Unfollow a-x-r-o-n" />
                                                    </form>
                                                </span>

                                            </div>
                                        </div>


                                    </div>


                                    <div class="js-profile-editable-area d-flex flex-column d-md-block">
                                        <div class="p-note user-profile-bio mb-3 js-user-profile-bio f4"
                                            data-bio-text="" hidden></div>
                                            


                                        <div class="flex-order-1 flex-md-order-none mt-2 mt-md-0">
                                            <div class="mb-3">
                                                <a class="Link--secondary no-underline no-wrap"
                                                    href="https://github.com/a-x-r-o-n?tab=followers">
                                                    <svg style="margin-right: var(--base-size-4, 4px);" text="muted" aria-hidden="true" height="16"
                                                        viewBox="0 0 16 16" version="1.1" width="16"
                                                        data-view-component="true" class="octicon octicon-people">
                                                        <path
                                                            d="M2 5.5a3.5 3.5 0 1 1 5.898 2.549 5.508 5.508 0 0 1 3.034 4.084.75.75 0 1 1-1.482.235 4 4 0 0 0-7.9 0 .75.75 0 0 1-1.482-.236A5.507 5.507 0 0 1 3.102 8.05 3.493 3.493 0 0 1 2 5.5ZM11 4a3.001 3.001 0 0 1 2.22 5.018 5.01 5.01 0 0 1 2.56 3.012.749.749 0 0 1-.885.954.752.752 0 0 1-.549-.514 3.507 3.507 0 0 0-2.522-2.372.75.75 0 0 1-.574-.73v-.352a.75.75 0 0 1 .416-.672A1.5 1.5 0 0 0 11 5.5.75.75 0 0 1 11 4Zm-5.5-.5a2 2 0 1 0-.001 3.999A2 2 0 0 0 5.5 3.5Z">
                                                        </path>
                                                    </svg>
                                                    <span class="text-bold color-fg-default">{{ userData?userData["followers"]:0 }}</span>
                                                    followers
                                                </a> &middot; <a class="Link--secondary no-underline no-wrap"
                                                    href="https://github.com/a-x-r-o-n?tab=following">
                                                    <span class="text-bold color-fg-default">{{ userData?userData["following"]:0 }}</span>
                                                    following
                                                </a>
                                            </div>
                                        </div>

                                        <ul class="vcard-details">







                                        </ul>
                                        <div>
                                            <p>{{ userData?userData["bio"]:"" }}</p>
                                        </div>
                                    </div>

                                </div>

                                <div class="border-top color-border-muted pt-3 mt-3 d-none d-md-block">
                                    <h2 class="h4 mb-2"><a href="/a-x-r-o-n?tab=achievements"
                                        class="Link--primary mb-2">Links</a></h2>
                                    <div class="d-flex flex-wrap" style="gap: 5px;"><a v-if="userData?userData['blog']:null" target="_blank" :href="userData?userData['blog']:null"
                                        class="position-relative"><img
                                        src="../assets/images/website-svg.svg"
                                        data-hovercard-type="achievement"
                                        data-hovercard-url="/users/a-x-r-o-n/achievements/pull-shark/detail?hovercard=1" width="64"
                                        alt="Achievement: Pull Shark" data-view-component="true"
                                        class="achievement-badge-sidebar" /></a>
                                        <a v-if="userData?userData['twitter_username']:null" target="_blank" :href="`https://www.x.com/${userData?userData['twitter_username']:null}`" class="position-relative"><img
                                        src="https://github.githubassets.com/assets/quickdraw-default-39c6aec8ff89.png"
                                        data-hovercard-type="achievement"
                                        data-hovercard-url="/users/a-x-r-o-n/achievements/quickdraw/detail?hovercard=1" width="64"
                                        alt="Achievement: Quickdraw" data-view-component="true"
                                        class="achievement-badge-sidebar" /></a>
                                    </div>
                                </div>


                                <div class="border-top color-border-muted pt-3 mt-3 d-none d-md-block">
                                    <h2 class="h4 mb-2">Highlights</h2>
                                    <ul class="list-style-none">
                                    <li class="mt-2">
                                        <svg style="margin-right: var(--base-size-4, 4px);" aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                                        data-view-component="true" class="octicon octicon-star color-fg-muted">
                                        <path
                                            d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                        </path>
                                        </svg>
                                        <span title="Label: Pro" data-view-component="true" class="Label Label--purple text-uppercase">
                                        Pro
                                        </span>
                                    </li>
                                    </ul>
                                </div>
                                <button id="dialog-show-dialog-6ce5fa53-b6d0-40f4-b757-2c8e8f3c51e0"
                                    data-show-dialog-id="dialog-6ce5fa53-b6d0-40f4-b757-2c8e8f3c51e0" type="button"
                                    data-view-component="true" class="Button--link Button--medium Button color-fg-muted"> <span
                                    class="Button-content">
                                    <span class="Button-label text-bold" style="color: var(--text-muted);">Block or Report</span>
                                    </span>
                                </button>

                            </div>

                        </div>
                    </div>

                    <div v-if="this.pageViewing === 0" data-view-component="true" class="Layout-main">
                        <div class="Box mt-4 ">
                            <div class="Box-body p-4">
                                <div class="d-flex flex-justify-between">
                                    <div class="text-mono text-small mb-3">
                                        <a href="/a-x-r-o-n/a-x-r-o-n" class="no-underline Link--primary">{{userData?userData["login"]:'a'}}</a><span
                            class="color-fg-muted d-inline-block" style="padding:0px 2px;">/</span>STATS<span
                            class="color-fg-muted">.md</span>
                                    </div>
                                </div>

                                <article class="markdown-body entry-content container-lg f5" itemprop="text">

                                    <div class="markdown-heading" dir="auto">
                                        <h1 class="heading-element" dir="auto">📊 GitHub Stats:</h1><a id="user-content--github-stats"
                                            class="anchor" aria-label="Permalink: 📊 GitHub Stats:" href="#-github-stats"><svg
                                            class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16"
                                            aria-hidden="true">
                                            <path
                                                d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z">
                                            </path>
                                            </svg></a>
                                    </div>
                                    <p style="display: flex; justify-content: space-evenly;" dir="auto"><a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/60af0bb8646fa8afb66b6bf20fc246d0cc5e223c639b92efe15ea664797ffe8c/68747470733a2f2f6769746875622d726561646d652d73747265616b2d73746174732e6865726f6b756170702e636f6d2f3f757365723d736f6e697961763230267468656d653d6461726b26686964655f626f726465723d66616c7365"><img
                                        :src="`https://github-readme-streak-stats.herokuapp.com/?user=${userData?userData['login']:'a'}&theme=transparent&hide_border=true`"
                                        alt=""
                                        data-canonical-src="https://github-readme-streak-stats.herokuapp.com/?user=a-x-r-o-n&amp;theme=transparent&amp;hide_border=false"
                                        style="max-width: 100%;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/dd64b5d220a8bf4445005a129d1bf452c9cc671429974d0bc971e2d2221a0088/68747470733a2f2f6769746875622d726561646d652d73746174732e76657263656c2e6170702f6170693f757365726e616d653d736f6e697961763230267468656d653d6461726b26686964655f626f726465723d66616c736526696e636c7564655f616c6c5f636f6d6d6974733d7472756526636f756e745f707269766174653d74727565"><img
                                        :src="`https://github-readme-stats.vercel.app/api?username=${userData?userData['login']:'a'}&theme=transparent&hide_border=true`"
                                        alt=""
                                        data-canonical-src="https://github-readme-stats.vercel.app/api?username=a-x-r-o-n&amp;theme=transparent&amp;hide_border=false&amp;include_all_commits=true&amp;count_private=true"
                                        style="max-width: 100%;"></a>
                                    </p>
                                    <!-- <p>
                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/af6d93cce46283b585fffba7f1ff9d55fb329eef0013975ca8a316705a3a0ded/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f6d6f73742d636f6d6d69742d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=a-x-r-o-n&amp;theme=transparent"
                                        style="display: block; margin: 0px auto;max-width: 100%;"></a>


                                    </p> -->
                                    <p dir="auto" style="display: flex; justify-content: space-evenly;">
                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/ab960ba950334e2f3f537e77c2bd1aa515b9bb7df044a06074edaab906692524/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f7265706f732d7065722d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=a-x-r-o-n&amp;theme=transparent"
                                        style="max-width: auto;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/af6d93cce46283b585fffba7f1ff9d55fb329eef0013975ca8a316705a3a0ded/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f6d6f73742d636f6d6d69742d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`https://github-readme-stats.vercel.app/api/top-langs/?username=${userData?userData['login']:'a'}&theme=transparent&hide_border=true`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=a-x-r-o-n&amp;theme=transparent"
                                        style="max-width: 100%;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/af6d93cce46283b585fffba7f1ff9d55fb329eef0013975ca8a316705a3a0ded/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f6d6f73742d636f6d6d69742d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=a-x-r-o-n&amp;theme=transparent"
                                        style="max-width: 100%;"></a>
                                        
                                    </p>

                                    <!-- <p dir="auto" style="display: flex; justify-content: space-evenly;">
                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/ab960ba950334e2f3f537e77c2bd1aa515b9bb7df044a06074edaab906692524/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f7265706f732d7065722d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`https://github-readme-stats.vercel.app/api/wakatime?username=${userData?userData['login']:''}&theme=transparent&hide_border=true`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=a-x-r-o-n&amp;theme=transparent"
                                        style="max-width: auto;"></a>
                                    </p> -->
                                    
                                    <!-- <div class="markdown-heading" dir="auto">
                                        <h2 class="heading-element" dir="auto">🌐 Socials:</h2><a id="user-content--socials"
                                            class="anchor" aria-label="Permalink: 🌐 Socials:" href="#-socials"><svg
                                            class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16"
                                            aria-hidden="true">
                                            <path
                                                d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z">
                                            </path>
                                            </svg></a>
                                    </div>
                                    <p dir="auto">
                                        <a href="https://linkedin.com/in/soniyavijay" rel="nofollow"><img src="https://custom-icon-badges.demolab.com/badge/LinkedIn-0A66C2?logo=linkedin-white&logoColor=fff" alt="LinkedIn" data-canonical-src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white" style="height: 25px;"></a>
                                    </p> -->
                                    <div class="markdown-heading" dir="auto">
                                        <h1 class="heading-element" dir="auto">🏆 GitHub Trophies</h1><a
                                            id="user-content--github-trophies" class="anchor" aria-label="Permalink: 🏆 GitHub Trophies"
                                            href="#-github-trophies"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1"
                                            width="16" height="16" aria-hidden="true">
                                            <path
                                                d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z">
                                            </path>
                                            </svg></a>
                                    </div>
                                    <p dir="auto"><a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/38df3110343df49889e447f4e3529f4d8c45a178123d4fc4ccf1e79f9ae56e40/68747470733a2f2f6769746875622d70726f66696c652d74726f7068792e76657263656c2e6170702f3f757365726e616d653d736f6e697961763230267468656d653d7261646963616c266e6f2d6672616d653d66616c7365266e6f2d62673d66616c7365266d617267696e2d773d34"><img
                                        :src="`https://github-profile-trophy.vercel.app/?username=${userData?userData['login']:'a'}&theme=darkhub`"
                                        alt=""
                                        data-canonical-src="https://github-profile-trophy.vercel.app/?username=a-x-r-o-n&amp;theme=radical&amp;no-frame=false&amp;no-bg=false&amp;margin-w=4"
                                        style="max-width: 100%;"></a>
                                    </p>
                                    <!-- <img src="https://raw.githubusercontent.com/a-x-r-o-n//output/snake.svg" alt="Snake animation" /> -->
                                </article>



                            </div>
                        </div>
                        <!--  -->
                  <div class="mt-4">
                    <div class="js-pinned-items-reorder-container">
                      <h2 class="f4 mb-2 text-normal">
                        Recent repositories
                        <span data-view-component="true">
                          <svg style="box-sizing: content-box; color: var(--color-icon-primary);" width="16" height="16"
                            viewBox="0 0 16 16" fill="none" aria-hidden="true" data-view-component="true"
                            class="spinner pinned-items-spinner js-pinned-items-spinner v-align-text-bottom ml-1 anim-rotate">
                            <circle cx="8" cy="8" r="7" stroke="currentColor" stroke-opacity="0.25" stroke-width="2"
                              vector-effect="non-scaling-stroke" fill="none" />
                            <path d="M15 8a7.002 7.002 0 00-7-7" stroke="currentColor" stroke-width="2"
                              stroke-linecap="round" vector-effect="non-scaling-stroke" />
                          </svg> <span class="sr-only">Loading</span>
                        </span>
                        <span class="ml-2 color-fg-muted f6 js-pinned-items-reorder-message" role="status"
                          aria-live="polite" data-error-text="Something went wrong."
                          data-success-text="Order updated."></span>
                      </h2>

                        <ol class="d-flex flex-wrap list-style-none gutter-condensed mb-4">

                        <li v-for="repo in recentCreatedRepo" class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="410462296"
                                    href="/a-x-r-o-n/name_generator" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo"> {{ repo["name"] }} </span></a></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">
                                {{ repo["description"] ? displayDescriptionTOPinnedRepos(repo["description"]) : "" }}
                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span v-if="recentCreatedRepoWithLanguage[`${repo[`name`]}`]" class="d-inline-block mr-3">
                                  <span class="repo-language-color" :style="`background-color: ${recentCreatedRepoWithLanguage[`${repo[`name`]}`]?languageFrameworkColors[recentCreatedRepoWithLanguage[`${repo[`name`]}`].toLowerCase()]:null}`"></span>
                                  <span class="ml-1" itemprop="programmingLanguage">{{ recentCreatedRepoWithLanguage[`${repo["name"]}`] }}</span>
                                </span>

                                <a href="/a-x-r-o-n/name_generator/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  {{ userData?repo["stargazers_count"]:12 }}
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        
                      </ol>

                      <!-- <ol class="d-flex flex-wrap list-style-none gutter-condensed mb-4">

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="410462296"
                                    href="/a-x-r-o-n/name_generator" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      name_generator
                                    </span></a> <tool-tip id="tooltip-289f3c85-a78c-45d6-ad9f-297774bba047"
                                    for="410462296" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">name_generator</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #00B4AB"></span>
                                  <span class="ml-1" itemprop="programmingLanguage">Dart</span>
                                </span>

                                <a href="/a-x-r-o-n/name_generator/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="417581251"
                                    href="/a-x-r-o-n/login_app" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      login_app
                                    </span></a> <tool-tip id="tooltip-915bd2d8-87b2-40e6-a7ba-6285e40ff598"
                                    for="417581251" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">login_app</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #00B4AB"></span>
                                  <span itemprop="programmingLanguage">Dart</span>
                                </span>

                                <a href="/a-x-r-o-n/login_app/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="419948209"
                                    href="/a-x-r-o-n/voice_to_text" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      voice_to_text
                                    </span></a> <tool-tip id="tooltip-6838335f-ff06-49bd-a841-2cc2e43a9784"
                                    for="419948209" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">voice_to_text</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #00B4AB"></span>
                                  <span itemprop="programmingLanguage">Dart</span>
                                </span>

                                <a href="/a-x-r-o-n/voice_to_text/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="758605303"
                                    href="/a-x-r-o-n/ml_image_classification" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      ml_image_classification
                                    </span></a> <tool-tip id="tooltip-7386cf8e-c186-448f-af3d-5d2941a88623"
                                    for="758605303" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">ml_image_classification</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #00B4AB"></span>
                                  <span itemprop="programmingLanguage">Dart</span>
                                </span>

                                <a href="/a-x-r-o-n/ml_image_classification/stargazers"
                                  class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="845836211"
                                    href="/a-x-r-o-n/sih_isl" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      sih_isl
                                    </span></a> <tool-tip id="tooltip-19b5d061-e493-4284-bc0a-e351ed9ca42d"
                                    for="845836211" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">sih_isl</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #00B4AB"></span>
                                  <span itemprop="programmingLanguage">Dart</span>
                                </span>

                                <a href="/a-x-r-o-n/sih_isl/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="891553129"
                                    href="/a-x-r-o-n/dlc_lab_exps" data-view-component="true"
                                    class="min-width-0 Link text-bold flex-auto wb-break-all"><span class="repo">
                                      dlc_lab_exps
                                    </span></a> <tool-tip id="tooltip-e21b415f-4bad-4f78-8072-e63c62bac1e9"
                                    for="891553129" popover="manual" data-direction="s" data-type="description"
                                    data-view-component="true"
                                    class="sr-only position-absolute">dlc_lab_exps</tool-tip></span> <span
                                  class="flex-auto text-right">
                                  <span></span><span class="Label Label--secondary v-align-middle ">Public</span>
                                </span>
                              </div>


                              <p class="pinned-item-desc color-fg-muted text-small d-block mt-2 mb-3">

                              </p>

                              <p class="mb-0 f6 color-fg-muted">
                                <span class="d-inline-block mr-3">
                                  <span class="repo-language-color" style="background-color: #DA5B0B"></span>
                                  <span itemprop="programmingLanguage">Jupyter Notebook</span>
                                </span>

                                <a href="/a-x-r-o-n/dlc_lab_exps/stargazers" class="pinned-item-meta Link--muted">
                                  <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1"
                                    width="16" data-view-component="true" class="octicon octicon-star">
                                    <path
                                      d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                    </path>
                                  </svg>
                                  1
                                </a>
                              </p>
                            </div>
                          </div>
                        </li>
                      </ol> -->

                    </div>

                  </div>
                        <!--  -->
            </div>
            <div v-else-if="this.pageViewing === 1" data-view-component="true" class="Layout-main">
                <div class="pl-5" id="user-repositories-list" data-hpc>
                    <ul data-filterable-for="your-repos-filter" data-filterable-type="substring">
                        <li class="col-12 d-flex flex-justify-between width-full py-4 border-bottom color-border-muted public source"></li>
                        <li v-for="repo in userReposData" class="col-12 d-flex flex-justify-between width-full py-4 border-bottom color-border-muted public source" >
                            <div class="col-10 col-lg-9 d-inline-block">
                                <div class="d-inline-block mb-1">
                                    <h3 class="wb-break-all">
                                        <a href="/A/client-rest-framework" >
                                            {{ repo["name"] }}</a>
                                        <span></span><span class="Label Label--secondary v-align-middle ml-1 mb-1">{{ repo["visibility"]==="public"?"Public":"Private" }}</span>
                                    </h3>
                                </div>
                                <div>
                                    <p v-if="repo[`description`]" class="col-9 d-inline-block color-fg-muted mb-2 pr-4">
                                    {{repo["description"] ? displayDescriptionTOPinnedRepos(repo["description"],240) : ""}}
                                    </p>
                                </div>
                                <div v-if="repo[`topics`]" class="topics-row-container d-inline-flex flex-wrap flex-items-center f6 my-1">
                                    <a v-for="topic in repo[`topics`]" data-ga-click="Topic, repository list" data-octo-click="topic_click"
                                    data-octo-dimensions="topic:frontend,repository_id:605965430,repository_nwo:A/client-rest-framework,repository_public:true,repository_is_fork:false"
                                    :href="`https://github.com/topics/${topic}`" title="Topic: frontend" data-view-component="true"
                                    class="topic-tag topic-tag-link f6 my-1">
                                    {{ topic }}
                                    </a>
                                </div>

                                <div class="f6 color-fg-muted mt-2">

                            <span v-if="repo[`language`]" class="ml-0 mr-3">
                              <span class="repo-language-color" :style="`background-color: ${languageFrameworkColors[repo[`language`].toLowerCase()]}`"></span>
                              <span itemprop="programmingLanguage" class="ml-1">{{repo["language"]}}</span>
                            </span>

                            <a class="Link--muted mr-3" href="/A/client-rest-framework/stargazers">
                              <svg aria-label="star" role="img" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                                data-view-component="true" class="octicon octicon-star">
                                <path
                                  d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.751.751 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25Zm0 2.445L6.615 5.5a.75.75 0 0 1-.564.41l-3.097.45 2.24 2.184a.75.75 0 0 1 .216.664l-.528 3.084 2.769-1.456a.75.75 0 0 1 .698 0l2.77 1.456-.53-3.084a.75.75 0 0 1 .216-.664l2.24-2.183-3.096-.45a.75.75 0 0 1-.564-.41L8 2.694Z">
                                </path>
                              </svg>
                              {{ repo["stargazers_count"] }}
                            </a>

                            <span class="mr-3">
                              <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                                data-view-component="true" class="octicon octicon-law mr-1">
                                <path
                                  d="M8.75.75V2h.985c.304 0 .603.08.867.231l1.29.736c.038.022.08.033.124.033h2.234a.75.75 0 0 1 0 1.5h-.427l2.111 4.692a.75.75 0 0 1-.154.838l-.53-.53.529.531-.001.002-.002.002-.006.006-.006.005-.01.01-.045.04c-.21.176-.441.327-.686.45C14.556 10.78 13.88 11 13 11a4.498 4.498 0 0 1-2.023-.454 3.544 3.544 0 0 1-.686-.45l-.045-.04-.016-.015-.006-.006-.004-.004v-.001a.75.75 0 0 1-.154-.838L12.178 4.5h-.162c-.305 0-.604-.079-.868-.231l-1.29-.736a.245.245 0 0 0-.124-.033H8.75V13h2.5a.75.75 0 0 1 0 1.5h-6.5a.75.75 0 0 1 0-1.5h2.5V3.5h-.984a.245.245 0 0 0-.124.033l-1.289.737c-.265.15-.564.23-.869.23h-.162l2.112 4.692a.75.75 0 0 1-.154.838l-.53-.53.529.531-.001.002-.002.002-.006.006-.016.015-.045.04c-.21.176-.441.327-.686.45C4.556 10.78 3.88 11 3 11a4.498 4.498 0 0 1-2.023-.454 3.544 3.544 0 0 1-.686-.45l-.045-.04-.016-.015-.006-.006-.004-.004v-.001a.75.75 0 0 1-.154-.838L2.178 4.5H1.75a.75.75 0 0 1 0-1.5h2.234a.249.249 0 0 0 .125-.033l1.288-.737c.265-.15.564-.23.869-.23h.984V.75a.75.75 0 0 1 1.5 0Zm2.945 8.477c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L13 6.327Zm-10 0c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L3 6.327Z">
                                </path>
                              </svg>MIT License
                            </span>


                            Updated <relative-time datetime="2025-06-05T15:15:42Z" class="no-wrap">{{ formatDate(repo['updated_at']) }}</relative-time>
                          </div>



                            </div>
                        </li>
                    </ul>
                    <div class="paginate-container">
                        <div role="navigation" aria-label="Pagination" class="d-flex d-md-inline-block pagination">
                            <span class="previous_page disabled" aria-label="Previous page">Previous</span> 
                            <a class="next_page" aria-label="Next page" rel="next" href="/A?page=2&amp;tab=repositories">Next</a>
                        </div>
                    </div>
                </div>
            </div>
            <div v-else-if="this.pageViewing === 2">
                <!-- <div data-view-component="true" class="Layout-main">

                    <div id="memexes-results" data-hpc="true" data-view-component="true" class="border rounded-2">
                      <h2 class="sr-only">Search results</h2>
                      <span hidden="hidden" id="projects-search-results-text" data-view-component="true">
                        0 open and 0 closed projects found.
                      </span>
                      <div data-view-component="true"
                        class="Box border-top-0 border-left-0 border-right-0 border-bottom-0">
                        <div id="header-8bbfeb98-3e8a-4baa-a01a-77f8a90160f3" data-view-component="true"
                          class="Box-header border-bottom-0">

                          <div data-view-component="true" class="d-flex flex-auto flex-items-center">
                            <div data-view-component="true" class="d-flex flex-auto flex-shrink-0">
                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen" data-view-component="true"
                                class="Link--primary Link text-bold p-0"><svg aria-hidden="true" height="16"
                                  viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true"
                                  class="octicon octicon-table">
                                  <path
                                    d="M0 1.75C0 .784.784 0 1.75 0h12.5C15.216 0 16 .784 16 1.75v12.5A1.75 1.75 0 0 1 14.25 16H1.75A1.75 1.75 0 0 1 0 14.25ZM6.5 6.5v8h7.75a.25.25 0 0 0 .25-.25V6.5Zm8-1.5V1.75a.25.25 0 0 0-.25-.25H6.5V5Zm-13 1.5v7.75c0 .138.112.25.25.25H5v-8ZM5 5V1.5H1.75a.25.25 0 0 0-.25.25V5Z">
                                  </path>
                                </svg>
                                0 Open</a> <a href="/users/A/projects?is_search=true&amp;query=is%3Aclosed"
                                data-view-component="true"
                                class="Link--primary Link Link--muted text-normal p-0 ml-3"><svg aria-hidden="true"
                                  height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true"
                                  class="octicon octicon-archive">
                                  <path
                                    d="M0 2.75C0 1.784.784 1 1.75 1h12.5c.966 0 1.75.784 1.75 1.75v1.5A1.75 1.75 0 0 1 14.25 6H1.75A1.75 1.75 0 0 1 0 4.25ZM1.75 7a.75.75 0 0 1 .75.75v5.5c0 .138.112.25.25.25h10.5a.25.25 0 0 0 .25-.25v-5.5a.75.75 0 0 1 1.5 0v5.5A1.75 1.75 0 0 1 13.25 15H2.75A1.75 1.75 0 0 1 1 13.25v-5.5A.75.75 0 0 1 1.75 7Zm0-4.5a.25.25 0 0 0-.25.25v1.5c0 .138.112.25.25.25h12.5a.25.25 0 0 0 .25-.25v-1.5a.25.25 0 0 0-.25-.25ZM6.25 8h3.5a.75.75 0 0 1 0 1.5h-3.5a.75.75 0 0 1 0-1.5Z">
                                  </path>
                                </svg>
                                0 Closed</a>
                            </div>
                            <action-menu data-select-variant="single" data-view-component="true">
                              <focus-group direction="vertical" mnemonics retain>
                                <button id="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-button"
                                  popovertarget="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-overlay"
                                  aria-controls="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-list"
                                  aria-haspopup="true" type="button" data-view-component="true"
                                  class="Button--invisible Button--medium Button p-0"> <span class="Button-content">
                                    <span class="Button-label">Sort</span>
                                  </span>
                                  <span class="Button-visual Button-trailingAction">
                                    <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16"
                                      data-view-component="true" class="octicon octicon-triangle-down">
                                      <path
                                        d="m4.427 7.427 3.396 3.396a.25.25 0 0 0 .354 0l3.396-3.396A.25.25 0 0 0 11.396 7H4.604a.25.25 0 0 0-.177.427Z">
                                      </path>
                                    </svg>
                                  </span>
                                </button>


                                <anchored-position data-target="action-menu.overlay"
                                  id="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-overlay"
                                  anchor="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-button" align="end"
                                  side="outside-bottom" anchor-offset="normal" popover="auto"
                                  data-view-component="true">
                                  <div data-view-component="true" class="Overlay Overlay--size-auto">

                                    <div data-view-component="true" class="Overlay-body Overlay-body--paddingNone">
                                      <action-list>
                                        <div data-view-component="true">
                                          <ul aria-labelledby="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-button"
                                            id="action-menu-707ad61c-e198-4e32-9f7d-7a62ea768ff9-list" role="menu"
                                            data-view-component="true" class="ActionListWrap--inset ActionListWrap">
                                            <li data-targets="action-list.items" role="none" data-view-component="true"
                                              class="ActionListItem">


                                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen?type=new&amp;query=is:open sort:updated-desc"
                                                tabindex="-1" id="item-e1735d61-5cef-49f2-b196-eb491f4bd7bf"
                                                role="menuitemradio" aria-checked="true" data-view-component="true"
                                                class="ActionListContent">
                                                <span class="ActionListItem-visual ActionListItem-action--leading">
                                                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
                                                    width="16" data-view-component="true"
                                                    class="octicon octicon-check ActionListItem-singleSelectCheckmark">
                                                    <path
                                                      d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z">
                                                    </path>
                                                  </svg>
                                                </span>

                                                <span data-view-component="true" class="ActionListItem-label">
                                                  <div class="select-menu-item-text">Recently updated</div>

                                                </span>
                                              </a>

                                            </li>
                                            <li data-targets="action-list.items" role="none" data-view-component="true"
                                              class="ActionListItem">


                                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen?type=new&amp;query=is:open sort:created-desc"
                                                tabindex="-1" id="item-2cbee5eb-2cef-4477-b7db-f64b6fb1ab3c"
                                                role="menuitemradio" aria-checked="false" data-view-component="true"
                                                class="ActionListContent">
                                                <span class="ActionListItem-visual ActionListItem-action--leading">
                                                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
                                                    width="16" data-view-component="true"
                                                    class="octicon octicon-check ActionListItem-singleSelectCheckmark">
                                                    <path
                                                      d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z">
                                                    </path>
                                                  </svg>
                                                </span>

                                                <span data-view-component="true" class="ActionListItem-label">
                                                  <div class="select-menu-item-text">Newest</div>

                                                </span>
                                              </a>

                                            </li>
                                            <li data-targets="action-list.items" role="none" data-view-component="true"
                                              class="ActionListItem">


                                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen?type=new&amp;query=is:open sort:created-asc"
                                                tabindex="-1" id="item-f16ef7de-5b1f-478e-a2b8-f213dcbe3867"
                                                role="menuitemradio" aria-checked="false" data-view-component="true"
                                                class="ActionListContent">
                                                <span class="ActionListItem-visual ActionListItem-action--leading">
                                                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
                                                    width="16" data-view-component="true"
                                                    class="octicon octicon-check ActionListItem-singleSelectCheckmark">
                                                    <path
                                                      d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z">
                                                    </path>
                                                  </svg>
                                                </span>

                                                <span data-view-component="true" class="ActionListItem-label">
                                                  <div class="select-menu-item-text">Oldest</div>

                                                </span>
                                              </a>

                                            </li>
                                            <li data-targets="action-list.items" role="none" data-view-component="true"
                                              class="ActionListItem">


                                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen?type=new&amp;query=is:open sort:updated-asc"
                                                tabindex="-1" id="item-05f85e31-e36c-4bb7-852c-56f581958ab5"
                                                role="menuitemradio" aria-checked="false" data-view-component="true"
                                                class="ActionListContent">
                                                <span class="ActionListItem-visual ActionListItem-action--leading">
                                                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
                                                    width="16" data-view-component="true"
                                                    class="octicon octicon-check ActionListItem-singleSelectCheckmark">
                                                    <path
                                                      d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z">
                                                    </path>
                                                  </svg>
                                                </span>

                                                <span data-view-component="true" class="ActionListItem-label">
                                                  <div class="select-menu-item-text">Least recently updated</div>

                                                </span>
                                              </a>

                                            </li>
                                            <li data-targets="action-list.items" role="none" data-view-component="true"
                                              class="ActionListItem">


                                              <a href="/users/A/projects?is_search=true&amp;query=is%3Aopen?type=new&amp;query=is:open sort:title-asc"
                                                tabindex="-1" id="item-8ff3315f-190c-43ae-aca8-51a48e86948a"
                                                role="menuitemradio" aria-checked="false" data-view-component="true"
                                                class="ActionListContent">
                                                <span class="ActionListItem-visual ActionListItem-action--leading">
                                                  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
                                                    width="16" data-view-component="true"
                                                    class="octicon octicon-check ActionListItem-singleSelectCheckmark">
                                                    <path
                                                      d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z">
                                                    </path>
                                                  </svg>
                                                </span>

                                                <span data-view-component="true" class="ActionListItem-label">
                                                  <div class="select-menu-item-text">Name</div>

                                                </span>
                                              </a>

                                            </li>
                                          </ul>
                                        </div>
                                      </action-list>


                                    </div>

                                  </div>
                                </anchored-position> </focus-group>
                            </action-menu>
                          </div>

                        </div>

                        <ul aria-labelledby="header-8bbfeb98-3e8a-4baa-a01a-77f8a90160f3" data-view-component="true">
                          <li data-view-component="true" class="Box-row border-top">
                            <div class="blankslate-container">
                              <div data-view-component="true" class="blankslate">
                                <svg aria-hidden="true" height="24" viewBox="0 0 24 24" version="1.1" width="24"
                                  data-view-component="true" class="octicon octicon-table blankslate-icon">
                                  <path
                                    d="M2 3.75C2 2.784 2.784 2 3.75 2h16.5c.966 0 1.75.784 1.75 1.75v16.5A1.75 1.75 0 0 1 20.25 22H3.75A1.75 1.75 0 0 1 2 20.25ZM9 9v11.5h11.25a.25.25 0 0 0 .25-.25V9Zm11.5-1.5V3.75a.25.25 0 0 0-.25-.25H9v4ZM3.5 9v11.25c0 .138.112.25.25.25H7.5V9Zm4-1.5v-4H3.75a.25.25 0 0 0-.25.25V7.5Z">
                                  </path>
                                </svg>

                                <h2 data-view-component="true" class="blankslate-heading"> No open projects
                                </h2>
                                <p data-view-component="true"></p>

                              </div>
                            </div>


                          </li>
                        </ul>
                      </div>
                    </div>
                </div> -->
            </div>
            <div v-else-if="this.pageViewing === 3"></div>
            <div v-else-if="this.pageViewing === 4"></div>



                </div>
                <div v-else>
                    <div style="display: block;height: 70vh;width: 100%;"></div>
                </div>
            </div>
        </main>
    </div>

        <footer class="footer pt-8 pb-6 f6 color-fg-muted p-responsive" role="contentinfo">
      <h2 class='sr-only'>Footer</h2>




      <div
        class="d-flex flex-justify-center flex-items-center flex-column-reverse flex-lg-row flex-wrap flex-lg-nowrap">
        <div class="d-flex flex-items-center flex-shrink-0 mx-2">
          <a aria-label="GitHub Homepage" class="footer-octicon mr-2" href="/">
            <svg aria-hidden="true" height="24" viewBox="0 0 24 24" version="1.1" width="24" data-view-component="true"
              class="octicon octicon-mark-github">
                <path d="M12 0C18.6274 0 24 5.37258 24 12C24 18.6274 18.6274 24 12 24C5.37258 24 0 18.6274 0 12C0 5.37258 5.37258 0 12 0ZM7.375 5.72656C5.09963 6.87365 4.92403 6.97417 4.5918 7.3252C4.10277 7.82676 3.95262 8.29712 3.99023 9.21875C4.00904 9.77658 4.03353 9.90843 4.20898 10.2656C4.31555 10.4913 4.4416 10.7292 4.49805 10.792C4.58579 10.9111 4.5916 10.8926 4.68555 10.5732C4.82975 10.0905 5.02472 9.82065 5.36328 9.65137C5.63892 9.51357 5.70227 9.51383 7.0498 9.52637L8.4541 9.54492L7.66992 9.9834C6.78603 10.4849 6.39108 10.8362 5.8457 11.626C5.65135 11.9144 5.50715 12.1465 5.53223 12.1465C5.61396 12.1463 6.72965 11.4821 7.59473 10.918L8.49121 10.335L8.50391 13.0996L8.52246 15.8711L9.05566 15.3691L9.58887 14.874L9.60742 15.1494C9.63877 15.5444 9.54495 15.7142 9.0498 16.1592L8.60449 16.5537L8.29688 16.2471L7.99023 15.9463V15.2998C7.99022 14.88 7.96477 14.6543 7.9209 14.6543C7.88322 14.6544 7.62582 14.8735 7.34375 15.1367C7.05537 15.4063 6.62286 15.8139 6.37207 16.0459C6.12756 16.2779 5.9209 16.5105 5.9209 16.5732C5.92102 16.8368 6.07795 17.4756 6.14062 17.4756C6.17885 17.4748 6.36022 17.3185 6.54785 17.1309C6.73577 16.9429 6.91121 16.7864 6.93652 16.7861C6.9616 16.7861 6.98633 17.1437 6.98633 17.5889V18.3916L7.42578 18.8232C7.66371 19.0612 7.8768 19.2374 7.90234 19.2129C7.92742 19.1941 7.95816 18.899 7.9707 18.5605L8.00195 17.9463L8.24707 17.6953L8.49121 17.4443V19.7578L8.82422 20.0586L9.14941 20.3662L9.16895 19.6572C9.18774 18.9932 9.19399 18.9432 9.35059 18.7803C9.44463 18.68 9.53881 18.6045 9.55762 18.6045C9.58264 18.6075 9.61409 18.926 9.63281 19.3066C9.67045 20.1028 9.83365 20.6737 10.1973 21.2881C10.4176 21.665 11.7204 23.0557 11.8457 23.0557C11.9837 23.0556 13.2819 21.6511 13.5264 21.2373C13.658 21.0116 13.8207 20.648 13.8896 20.4287C14.0276 19.971 14.1463 18.9677 14.0898 18.7295C14.0586 18.5793 14.0651 18.5798 14.2656 18.7803C14.4786 18.9808 14.4794 18.9873 14.5107 19.6768L14.542 20.3789L14.874 20.0654L15.2002 19.7578V17.4502L15.4824 17.7266L15.7646 18.002V19.3252L16.2529 18.8359L16.7363 18.3535L16.7549 17.5381C16.7674 17.0875 16.7923 16.7247 16.8174 16.7236C16.8425 16.7236 17.031 16.8986 17.2441 17.1055L17.6387 17.4941L17.6768 17.25C17.7018 17.1183 17.745 16.9111 17.7764 16.792C17.8014 16.6729 17.8014 16.5355 17.7764 16.4854C17.745 16.4289 17.2874 15.9831 16.7607 15.4941L15.7959 14.6045L15.7646 15.2441L15.7324 15.8828L15.4189 16.2402L15.1123 16.6045L14.1279 15.6201L14.1465 15.2754L14.165 14.9365L14.667 15.4004L15.1689 15.8711L15.1875 13.2246C15.1938 11.7514 15.2255 10.5791 15.2568 10.5791C15.2925 10.5815 15.7921 10.8374 16.3662 11.1494C17.8521 11.9457 20.0585 13.0114 20.0146 12.9111C20.0057 12.8755 19.6687 12.3131 19.2754 11.6514L18.5537 10.4541L17.9268 10.209C17.5813 10.0708 16.3407 9.60756 15.1689 9.16895C13.9978 8.73056 13.0016 8.34167 12.9619 8.30957C12.8741 8.2406 12.8492 7.75781 12.9307 7.75781C13.0577 7.76083 17.6208 9.4326 18.9238 9.94629C19.1932 10.0591 19.4315 10.1339 19.4443 10.1152C19.4631 10.0964 19.1433 9.53859 18.7295 8.87402L17.9834 7.66406L16.7363 7.62598C15.8214 7.60091 15.3947 7.56344 15.1689 7.48828C14.9997 7.43186 14.3348 7.30652 13.6953 7.21875C13.0576 7.12496 12.5261 7.04315 12.5107 7.03027C12.4982 7.01773 12.5671 6.89281 12.6611 6.75488C12.7739 6.5983 12.88 6.50403 12.9678 6.50391C13.1933 6.50391 15.2216 6.86671 15.4189 6.94238C15.5255 6.98627 16.1841 7.03099 16.9238 7.0498C18.6605 7.09996 18.774 7.06856 19.4824 6.37891L19.9961 5.88281L16.6289 5.87695C14.7733 5.87695 13.2568 5.85808 13.2568 5.83301C13.257 5.80769 13.3313 5.68224 13.4189 5.55078L13.5889 5.3125H16.2725L16.8359 4.91797L17.4004 4.5293L15.2881 4.50977L13.1689 4.49805L12.9238 4.72949C12.7859 4.86119 12.3915 5.4067 12.0342 5.93945C11.3508 6.98021 11.043 7.31295 10.5352 7.54492C9.38805 8.0714 8.59787 7.93989 7.80176 7.09375L7.41895 6.67969L7.75195 6.5166C8.05899 6.36623 8.14721 6.35392 8.97461 6.34766H9.87109L9.93945 6.00195C10.0773 5.31268 10.0091 5.375 10.5732 5.375C11.0619 5.375 11.087 5.36893 11.4941 5.09961C11.7195 4.94935 11.9767 4.7491 12.0586 4.66113L12.209 4.49805H9.80176L7.375 5.72656ZM14.0586 16.5791L14.0781 17.125L12.9932 18.209C12.3976 18.8046 11.8829 19.2939 11.8516 19.2939C11.8219 19.2893 11.3037 18.8018 10.7109 18.209L9.62012 17.1309V16.0713L9.82715 16.2529C9.93377 16.3533 10.435 16.8426 10.9365 17.3379L11.8516 18.2344L12.9424 17.1309L14.04 16.0273L14.0586 16.5791ZM9.76465 13.3691C9.84071 13.4389 10.3417 13.9216 10.874 14.4414L11.8457 15.3945L12.9424 14.3281L14.04 13.2627L14.0586 13.8145L14.0781 14.3662L12.9619 15.4824L11.8457 16.5977L10.7363 15.4824L9.62012 14.3662V13.2559L9.76465 13.3691ZM15.7646 13.7705L16.4346 14.3535C16.8044 14.6732 17.5131 15.2936 18.0146 15.7324L18.9307 16.5293L18.9678 15.9209C19.0429 14.7871 19.0305 13.3091 18.9492 13.2002C18.9053 13.1438 18.5102 12.9117 18.0713 12.6797L17.2686 12.2598V13.1875L17.6133 13.4824C17.9957 13.821 18.0401 13.9397 18.0088 14.623L17.9902 15.0557L17.3818 14.4727L16.7676 13.8896V12.1338L16.5859 11.9707C16.4856 11.8767 16.2595 11.72 16.084 11.626L15.7646 11.4502V13.7705ZM7.94629 11.4004C7.91495 11.4004 7.70146 11.5382 7.45703 11.7012L7.01855 12.002L6.98633 12.9492L6.95508 13.9023L6.5166 14.3477C6.27846 14.5921 6.0023 14.8421 5.9082 14.9111L5.73242 15.0371V13.9023L6.10938 13.5381L6.48535 13.1689V12.7549C6.48535 12.5229 6.46607 12.335 6.44727 12.335C6.42494 12.3371 6.04441 12.5496 5.60156 12.8115L4.79199 13.2881V14.8799C4.79199 15.7576 4.81127 16.4727 4.83008 16.4727C4.8499 16.4717 5.23772 16.1394 5.68848 15.7324C6.14605 15.325 6.81713 14.7362 7.19336 14.4102C7.56319 14.0905 7.8953 13.7767 7.92676 13.7139C8.00188 13.5761 8.01492 11.4005 7.94629 11.4004ZM10.1406 11.1807C10.4228 11.4565 10.9117 11.9334 11.2314 12.2344C11.5449 12.5353 11.8271 12.7797 11.8584 12.7734C11.8857 12.7713 12.3989 12.2954 12.9932 11.7324L14.0713 10.6924V11.5508L12.9746 12.6484L11.8838 13.7393L10.9863 12.874C9.54447 11.476 9.62012 11.5759 9.62012 11.0869V10.6729L10.1406 11.1807ZM13.4941 9.4502C13.5192 9.4502 13.6706 9.5508 13.8398 9.66992C14.0022 9.79485 14.1329 9.91384 14.1338 9.93945C14.1338 9.96453 13.8517 10.2655 13.5068 10.6104L12.8799 11.2373V10.8359C12.8799 10.4414 12.8866 10.435 13.1621 10.1846C13.4004 9.96513 13.4443 9.89537 13.4443 9.68848C13.4444 9.55763 13.4631 9.45118 13.4941 9.4502ZM10.3477 10.002L10.8115 10.4229V10.792C10.8115 11.1304 10.8052 11.1493 10.7051 11.0742C10.4172 10.8615 9.6232 10.0432 9.62012 9.95898C9.62012 9.90883 9.68299 9.8018 9.75195 9.72656L9.88965 9.58203L10.3477 10.002ZM11.4072 8.19629C11.4463 8.19737 11.7084 8.35427 12.002 8.54785C12.2964 8.74204 12.5476 8.91102 12.5605 8.92383C12.5982 8.95518 11.9205 9.70117 11.8516 9.70117C11.8125 9.69964 11.5567 9.48088 11.2881 9.20605C10.7364 8.65433 10.7173 8.56067 11.1123 8.33496C11.2377 8.25973 11.3759 8.19629 11.4072 8.19629ZM6.73633 7.00586C6.75759 7.00844 6.96944 7.2015 7.20605 7.44434L7.63867 7.88281H5.85156L5.88965 7.73926C5.97115 7.47593 6.10922 7.31942 6.41016 7.16895C6.57317 7.08117 6.71752 7.01213 6.73633 7.00586ZM16.6416 1.04297C16.6349 0.94921 12.019 0.974094 11.752 1.07422C11.6328 1.1181 10.6983 1.70124 9.68262 2.37207C8.20981 3.34976 7.75814 3.68231 7.46973 4.00195C7.11863 4.3844 6.6358 5.23121 6.67969 5.36914C6.69253 5.40031 7.30067 5.09939 8.02148 4.69824L9.33789 3.96484L13.6328 3.93359C17.7001 3.90226 17.9396 3.89594 18.1465 3.7832C18.3785 3.65781 19.2129 2.88604 19.2129 2.79199C19.2033 2.76695 17.3822 2.73575 15.1562 2.72949L11.0996 2.71094L11.4629 2.45996L11.8271 2.20898L13.501 2.17773L15.1689 2.14648L15.5195 1.9707C15.8644 1.79513 16.6416 1.15582 16.6416 1.04297Z" fill="var(--text-muted)"/>
            </svg>
          </a>
          <span>
            &copy; 2025 Gryphon,&nbsp;Inc.
          </span>
        </div>

        <nav aria-label="Footer">
          <h3 class="sr-only" id="sr-footer-heading">Footer navigation</h3>

          <ul class="list-style-none d-flex  flex-justify-center flex-wrap mb-lg-0"
            aria-labelledby="sr-footer-heading">

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to Terms&quot;,&quot;label&quot;:&quot;text:terms&quot;}"
                href="https://docs.github.com/site-policy/github-terms/github-terms-of-service"
                data-view-component="true" class="Link--secondary Link">Terms</a>
            </li>

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to privacy&quot;,&quot;label&quot;:&quot;text:privacy&quot;}"
                href="https://docs.github.com/site-policy/privacy-policies/github-privacy-statement"
                data-view-component="true" class="Link--secondary Link">Privacy</a>
            </li>

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to security&quot;,&quot;label&quot;:&quot;text:security&quot;}"
                href="https://github.com/security" data-view-component="true" class="Link--secondary Link">Security</a>
            </li>

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to status&quot;,&quot;label&quot;:&quot;text:status&quot;}"
                href="https://www.githubstatus.com/" data-view-component="true" class="Link--secondary Link">Status</a>
            </li>

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to docs&quot;,&quot;label&quot;:&quot;text:docs&quot;}"
                href="https://docs.github.com/" data-view-component="true" class="Link--secondary Link">Docs</a>
            </li>

            <li class="mx-2">
              <a data-analytics-event="{&quot;category&quot;:&quot;Footer&quot;,&quot;action&quot;:&quot;go to contact&quot;,&quot;label&quot;:&quot;text:contact&quot;}"
                href="https://support.github.com?tags=dotcom-footer" data-view-component="true"
                class="Link--secondary Link">Contact</a>
            </li>

            <li class="mx-2">
              <cookie-consent-link>
                <button type="button" class="Link--secondary underline-on-hover border-0 p-0 color-bg-transparent"
                  data-action="click:cookie-consent-link#showConsentManagement"
                  data-analytics-event="{&quot;location&quot;:&quot;footer&quot;,&quot;action&quot;:&quot;cookies&quot;,&quot;context&quot;:&quot;subfooter&quot;,&quot;tag&quot;:&quot;link&quot;,&quot;label&quot;:&quot;cookies_link_subfooter_footer&quot;}">
                  Manage cookies
                </button>
              </cookie-consent-link>
            </li>

            <li class="mx-2">
              <cookie-consent-link>
                <button type="button" class="Link--secondary underline-on-hover border-0 p-0 color-bg-transparent"
                  data-action="click:cookie-consent-link#showConsentManagement"
                  data-analytics-event="{&quot;location&quot;:&quot;footer&quot;,&quot;action&quot;:&quot;dont_share_info&quot;,&quot;context&quot;:&quot;subfooter&quot;,&quot;tag&quot;:&quot;link&quot;,&quot;label&quot;:&quot;dont_share_info_link_subfooter_footer&quot;}">
                  Do not share my personal information
                </button>
              </cookie-consent-link>
            </li>

          </ul>
        </nav>
      </div>
    </footer>

</template>

<style scoped>

.paginate-container {
    display: flex;
    margin-top: var(--base-size-24);
    margin-bottom: var(--base-size-12);
    justify-content: center;
}

.Button-content {
    align-items: center;
    display: grid;
    flex: 1 0 auto;
    grid-template-areas: "leadingVisual text trailingVisual";
    grid-template-columns: min-content minmax(0, auto) min-content;
    place-content: center
}

.Button-content>:not(:last-child) {
    margin-right: var(--control-medium-gap);
}

.Button-content--alignStart {
    justify-content: start
}
.text-uppercase {
    text-transform: uppercase !important
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
.SegmentedControl--iconOnly .Button--iconOnly.Button--medium,
.SegmentedControl--iconOnly .Button--iconOnly.Button--small {
    padding-inline: 0 !important;
    width: 100%
}
.Button--link {
    color: var(--fgColor-link);
    display: inline-block;
    font-size: inherit;
    height: unset;
    min-width: -moz-fit-content;
    min-width: fit-content;
    padding: 0;
    fill: var(--fgColor-link);
    border: none
}

.Button--link:hover:not(:disabled, .Button--inactive) {
    -webkit-text-decoration: underline;
    text-decoration: underline
}

.Button--link:focus,
.Button--link:focus-visible {
    outline-offset: 2px
}

.Button--link:disabled,
.Button--link[aria-disabled=true] {
    color: var(--control-fgColor-disabled);
    fill: var(--control-fgColor-disabled);
    background-color: initial;
    border-color: #0000
}

.Button--link .Button-label {
    white-space: unset
}

.Label.Label--purple {
    color: var(--fgColor-done, var(--color-done-fg));
    border-color: var(--borderColor-done-emphasis, var(--color-done-emphasis))
}
:is(.label, .Label):hover {
    -webkit-text-decoration: none;
    text-decoration: none
}
.Label,
.label {
    border: var(--borderWidth-thin) solid var(--borderColor-default);
    border-radius: var(--borderRadius-full);
    display: inline-block;
    font-size: var(--text-body-size-small);
    font-weight: var(--base-text-weight-medium);
    line-height: 18px;
    padding: 0 var(--base-size-6);
    white-space: nowrap
}
.color-fg-default,
.fgColor-default {
    color: var(--fgColor-default, var(--color-fg-default)) !important
}
.text-bold {
    font-weight: var(--base-text-weight-semibold, 600) !important
}

.color-fg-muted,
.fgColor-muted {
    color: var(--fgColor-muted, var(--color-fg-muted)) !important
}
.achievement-badge-sidebar {
    filter: drop-shadow(var(--shadow-floating-large, var(--color-shadow-large)))
}
.list-style-none {
    list-style: none !important
}
.mb-2 {
    margin-bottom: var(--base-size-8, 8px) !important
}
.h4 {
    font-size: var(--h4-size, 16px) !important
}
.d-none {
    display: none !important
}

.mt-3 {
    margin-top: var(--base-size-16, 16px) !important
}

.border-top {
    border-top: var(--borderWidth-thin, 1px) solid var(--borderColor-default, var(--color-border-default)) !important
}
.pt-3 {
    padding-top: var(--base-size-16, 16px) !important
}
.color-border-muted,
.borderColor-muted {
    border-color: var(--borderColor-muted, var(--color-border-muted)) !important
}

.btn-block {
    display: block;
    width: 100%;
    text-align: center
}

.btn {
    position: relative;
    display: inline-block;
    padding: 5px var(--base-size-16);
    font-size: 14px;
    font-weight: var(--base-text-weight-medium, 500);
    line-height: 20px;
    white-space: nowrap;
    vertical-align: middle;
    cursor: pointer;
    -webkit-user-select: none;
    user-select: none;
    border: 1px solid;
    border-radius: 6px;
    appearance: none
}

.btn:hover {
    text-decoration: none
}

.btn:disabled,
.btn.disabled,
.btn[aria-disabled=true] {
    cursor: default
}

.btn i {
    font-style: normal;
    font-weight: var(--base-text-weight-medium, 500);
    opacity: .75
}

.btn .octicon {
    margin-right: var(--base-size-4);
    color: var(--fgColor-muted, var(--color-fg-muted));
    vertical-align: text-bottom
}

.btn .octicon:only-child {
    margin-right: 0
}

.btn .Counter {
    margin-left: 2px;
    color: inherit;
    text-shadow: none;
    vertical-align: top;
    background-color: var(--buttonCounter-default-bgColor-rest, var(--color-btn-counter-bg))
}

.btn .dropdown-caret {
    margin-left: var(--base-size-4);
    opacity: .8
}

.btn {
    color: var(--button-default-fgColor-rest, var(--color-btn-text));
    background-color: var(--button-default-bgColor-rest, var(--color-btn-bg));
    border-color: var(--button-default-borderColor-rest, var(--color-btn-border));
    box-shadow: var(--button-default-shadow-resting, var(--color-btn-shadow)), var(--button-default-shadow-inset, var(--color-btn-inset-shadow));
    transition: 80ms cubic-bezier(0.33, 1, 0.68, 1);
    transition-property: color, background-color, box-shadow, border-color
}

.btn:hover,
.btn.hover,
[open]>.btn {
    background-color: var(--button-default-bgColor-hover, var(--color-btn-hover-bg));
    border-color: var(--button-default-borderColor-hover, var(--color-btn-hover-border));
    transition-duration: .1s
}

.btn:active {
    background-color: var(--button-default-bgColor-active, var(--color-btn-active-bg));
    border-color: var(--button-default-borderColor-active, var(--color-btn-active-border));
    transition: none
}

.btn.selected,
.btn[aria-selected=true] {
    background-color: var(--button-default-bgColor-selected, var(--color-btn-selected-bg));
    box-shadow: var(--shadow-inset, var(--color-primer-shadow-inset))
}

.btn:disabled,
.btn.disabled,
.btn[aria-disabled=true] {
    color: var(--fgColor-disabled, var(--color-primer-fg-disabled));
    background-color: var(--button-default-bgColor-disabled, var(--color-btn-bg));
    border-color: var(--button-default-borderColor-disabled, var(--color-btn-border))
}

.btn:disabled .octicon,
.btn.disabled .octicon,
.btn[aria-disabled=true] .octicon {
    color: var(--fgColor-disabled, var(--color-primer-fg-disabled))
}

.octicon {
    display: inline-block;
    overflow: visible !important;
    vertical-align: text-bottom;
    fill: currentColor
}

.no-wrap {
    white-space: nowrap !important
}

.no-underline {
    text-decoration: none !important
}

.mb-3 {
    margin-bottom: var(--base-size-16, 16px) !important
}

.Link--secondary {
    color: var(--fgColor-muted) !important
}

.Link--secondary:hover {
    color: var(--fgColor-accent) !important
}
:is(.Link--secondary, .Link--primary, .Link--muted):hover [class*=color-fg] {
    color: inherit !important
}

.user-profile-bio {
    overflow: hidden;
    font-size: 14px
}

.container-xl {
    max-width: 1280px;
    margin-right: auto;
    margin-left: auto
}

.px-3 {
    padding-right: var(--base-size-16, 16px) !important;
    padding-left: var(--base-size-16, 16px) !important
}

.px-md-4 {
    padding-right: var(--base-size-24, 24px) !important;
    padding-left: var(--base-size-24, 24px) !important
}

.px-lg-5 {
    padding-right: var(--base-size-32, 32px) !important;
    padding-left: var(--base-size-32, 32px) !important
}

.mt-2 {
    margin-top: var(--base-size-8, 8px) !important
}

.Layout {
    display: grid;
    --Layout-sidebar-width: 220px;
    --Layout-gutter: 16px
}

@media (min-width: 1012px) {
    .Layout {
        --Layout-sidebar-width: 296px;
    }
}

@media(max-width: 767.98px) {
    .Layout.Layout--flowRow-until-md {
        grid-auto-flow: row;
        grid-template-columns: 1fr !important
    }

    .Layout.Layout--flowRow-until-md .Layout-divider,
    .Layout.Layout--flowRow-until-md .Layout-main,
    .Layout.Layout--flowRow-until-md .Layout-sidebar {
        grid-column: 1 !important;
        width: 100% !important
    }

    .Layout.Layout--flowRow-until-md.Layout--sidebarPosition-flowRow-start .Layout-sidebar {
        grid-row: 1
    }

    .Layout.Layout--flowRow-until-md.Layout--sidebarPosition-flowRow-end .Layout-sidebar,
    .Layout.Layout--flowRow-until-md.Layout--sidebarPosition-flowRow-start .Layout-main {
        grid-row: 2/span 2
    }

    .Layout.Layout--flowRow-until-md.Layout--sidebarPosition-flowRow-end .Layout-main {
        grid-row: 1
    }

    .Layout.Layout--flowRow-until-md.Layout--sidebarPosition-flowRow-none .Layout-sidebar {
        display: none
    }

    .Layout.Layout--flowRow-until-md.Layout--divided {
        --Layout-gutter: 0
    }

    .Layout.Layout--flowRow-until-md.Layout--divided .Layout-divider {
        grid-row: 2;
        height: 1px
    }

    .Layout-divider--flowRow-hidden:is(.Layout.Layout--flowRow-until-md.Layout--divided .Layout-divider) {
        display: none
    }

    .Layout-divider--flowRow-shallow:is(.Layout.Layout--flowRow-until-md.Layout--divided .Layout-divider) {
        background: var(--bgColor-inset);
        border-color: var(--borderColor-default);
        border-style: solid;
        border-width: var(--borderWidth-thin) 0;
        height: 8px;
        margin-right: 0
    }

    .Layout.Layout--flowRow-until-md.Layout--divided .Layout-main,
    .Layout.Layout--flowRow-until-md.Layout--divided.Layout--sidebarPosition-flowRow-end .Layout-sidebar {
        grid-row: 3/span 1
    }

    .Layout.Layout--flowRow-until-md.Layout--divided.Layout--sidebarPosition-flowRow-end .Layout-main {
        grid-row: 1
    }
}

@media(max-width: 543.98px) {
    .Layout {
        grid-auto-flow: row;
        grid-template-columns: 1fr !important
    }

    .Layout .Layout-divider,
    .Layout .Layout-main,
    .Layout .Layout-sidebar {
        grid-column: 1 !important;
        width: 100% !important
    }

    .Layout.Layout--sidebarPosition-flowRow-start .Layout-sidebar {
        grid-row: 1
    }

    .Layout.Layout--sidebarPosition-flowRow-end .Layout-sidebar,
    .Layout.Layout--sidebarPosition-flowRow-start .Layout-main {
        grid-row: 2/span 2
    }

    .Layout.Layout--sidebarPosition-flowRow-end .Layout-main {
        grid-row: 1
    }

    .Layout.Layout--sidebarPosition-flowRow-none .Layout-sidebar {
        display: none
    }

    .Layout.Layout--divided {
        --Layout-gutter: 0
    }

    .Layout.Layout--divided .Layout-divider {
        grid-row: 2;
        height: 1px
    }

    .Layout-divider--flowRow-hidden:is(.Layout.Layout--divided .Layout-divider) {
        display: none
    }

    .Layout-divider--flowRow-shallow:is(.Layout.Layout--divided .Layout-divider) {
        background: var(--bgColor-inset);
        border-color: var(--borderColor-default);
        border-style: solid;
        border-width: var(--borderWidth-thin) 0;
        height: 8px;
        margin-right: 0
    }

    .Layout.Layout--divided .Layout-main,
    .Layout.Layout--divided.Layout--sidebarPosition-flowRow-end .Layout-sidebar {
        grid-row: 3/span 1
    }

    .Layout.Layout--divided.Layout--sidebarPosition-flowRow-end .Layout-main {
        grid-row: 1
    }
}

.Layout-sidebar {
    width: var(--Layout-sidebar-width)
}

.Layout.Layout--sidebarPosition-start .Layout-sidebar {
    grid-column: 1
}

.Layout.Layout--sidebarPosition-start .Layout-main {
    grid-column: 2/span 2
}

.mt-5 {
    margin-top: var(--base-size-32, 32px) !important
}

.clearfix::before {
    display: table;
    content: ""
}

.clearfix::after {
    display: table;
    clear: both;
    content: ""
}

.d-flex {
    display: flex !important
}

.flex-items-center {
    align-items: center !important
}

.mb-4 {
    margin-bottom: var(--base-size-24, 24px) !important
}

.mb-md-0 {
    margin-bottom: 0 !important
}

.position-relative {
    position: relative !important
}

.d-inline-block {
    display: inline-block !important
}

.col-1 {
    width: 8.33333333%
}

.col-2 {
    width: 16.66666666%
}

.col-3 {
    width: 24.99999999%
}

.col-4 {
    width: 33.33333332%
}

.col-5 {
    width: 41.66666665%
}

.col-6 {
    width: 49.99999998%
}

.col-7 {
    width: 58.33333331%
}

.col-8 {
    width: 66.66666664%
}

.col-9 {
    width: 74.99999997%
}

.col-10 {
    width: 83.3333333%
}

.col-11 {
    width: 91.66666663%
}

.col-12 {
    width: 100%
}

.py-3 {
    padding-top: var(--base-size-16, 16px) !important;
    padding-bottom: var(--base-size-16, 16px) !important
}

.mr-3 {
    margin-right: var(--base-size-16, 16px) !important
}

.flex-shrink-0 {
    flex-shrink: 0 !important
}

.d-block {
    display: block !important
}
.mb-md-3 {
    margin-bottom: var(--base-size-16, 16px) !important
}
@media(min-width: 768px) {
    .m-md-0 {
        margin: 0 !important
    }

    .mt-md-0 {
        margin-top: 0 !important
    }

    .mb-md-0 {
        margin-bottom: 0 !important
    }

    .mr-md-0 {
        margin-right: 0 !important
    }

    .ml-md-0 {
        margin-left: 0 !important
    }

    .mx-md-0 {
        margin-right: 0 !important;
        margin-left: 0 !important
    }

    .my-md-0 {
        margin-top: 0 !important;
        margin-bottom: 0 !important
    }

    .m-md-1 {
        margin: var(--base-size-4, 4px) !important
    }

    .mt-md-1 {
        margin-top: var(--base-size-4, 4px) !important
    }

    .mb-md-1 {
        margin-bottom: var(--base-size-4, 4px) !important
    }

    .mr-md-1 {
        margin-right: var(--base-size-4, 4px) !important
    }

    .ml-md-1 {
        margin-left: var(--base-size-4, 4px) !important
    }

    .mt-md-n1 {
        margin-top: calc(-1*var(--base-size-4, 4px)) !important
    }

    .mb-md-n1 {
        margin-bottom: calc(-1*var(--base-size-4, 4px)) !important
    }

    .mr-md-n1 {
        margin-right: calc(-1*var(--base-size-4, 4px)) !important
    }

    .ml-md-n1 {
        margin-left: calc(-1*var(--base-size-4, 4px)) !important
    }

    .mx-md-1 {
        margin-right: var(--base-size-4, 4px) !important;
        margin-left: var(--base-size-4, 4px) !important
    }

    .my-md-1 {
        margin-top: var(--base-size-4, 4px) !important;
        margin-bottom: var(--base-size-4, 4px) !important
    }

    .m-md-2 {
        margin: var(--base-size-8, 8px) !important
    }

    .mt-md-2 {
        margin-top: var(--base-size-8, 8px) !important
    }

    .mb-md-2 {
        margin-bottom: var(--base-size-8, 8px) !important
    }

    .mr-md-2 {
        margin-right: var(--base-size-8, 8px) !important
    }

    .ml-md-2 {
        margin-left: var(--base-size-8, 8px) !important
    }

    .mt-md-n2 {
        margin-top: calc(-1*var(--base-size-8, 8px)) !important
    }

    .mb-md-n2 {
        margin-bottom: calc(-1*var(--base-size-8, 8px)) !important
    }

    .mr-md-n2 {
        margin-right: calc(-1*var(--base-size-8, 8px)) !important
    }

    .ml-md-n2 {
        margin-left: calc(-1*var(--base-size-8, 8px)) !important
    }

    .mx-md-2 {
        margin-right: var(--base-size-8, 8px) !important;
        margin-left: var(--base-size-8, 8px) !important
    }

    .my-md-2 {
        margin-top: var(--base-size-8, 8px) !important;
        margin-bottom: var(--base-size-8, 8px) !important
    }

    .m-md-3 {
        margin: var(--base-size-16, 16px) !important
    }

    .mt-md-3 {
        margin-top: var(--base-size-16, 16px) !important
    }

    .mb-md-3 {
        margin-bottom: var(--base-size-16, 16px) !important
    }

    .mr-md-3 {
        margin-right: var(--base-size-16, 16px) !important
    }

    .ml-md-3 {
        margin-left: var(--base-size-16, 16px) !important
    }

    .mt-md-n3 {
        margin-top: calc(-1*var(--base-size-16, 16px)) !important
    }

    .mb-md-n3 {
        margin-bottom: calc(-1*var(--base-size-16, 16px)) !important
    }

    .mr-md-n3 {
        margin-right: calc(-1*var(--base-size-16, 16px)) !important
    }

    .ml-md-n3 {
        margin-left: calc(-1*var(--base-size-16, 16px)) !important
    }

    .mx-md-3 {
        margin-right: var(--base-size-16, 16px) !important;
        margin-left: var(--base-size-16, 16px) !important
    }

    .my-md-3 {
        margin-top: var(--base-size-16, 16px) !important;
        margin-bottom: var(--base-size-16, 16px) !important
    }

    .m-md-4 {
        margin: var(--base-size-24, 24px) !important
    }

    .mt-md-4 {
        margin-top: var(--base-size-24, 24px) !important
    }

    .mb-md-4 {
        margin-bottom: var(--base-size-24, 24px) !important
    }

    .mr-md-4 {
        margin-right: var(--base-size-24, 24px) !important
    }

    .ml-md-4 {
        margin-left: var(--base-size-24, 24px) !important
    }

    .mt-md-n4 {
        margin-top: calc(-1*var(--base-size-24, 24px)) !important
    }

    .mb-md-n4 {
        margin-bottom: calc(-1*var(--base-size-24, 24px)) !important
    }

    .mr-md-n4 {
        margin-right: calc(-1*var(--base-size-24, 24px)) !important
    }

    .ml-md-n4 {
        margin-left: calc(-1*var(--base-size-24, 24px)) !important
    }

    .mx-md-4 {
        margin-right: var(--base-size-24, 24px) !important;
        margin-left: var(--base-size-24, 24px) !important
    }

    .my-md-4 {
        margin-top: var(--base-size-24, 24px) !important;
        margin-bottom: var(--base-size-24, 24px) !important
    }

    .m-md-5 {
        margin: var(--base-size-32, 32px) !important
    }

    .mt-md-5 {
        margin-top: var(--base-size-32, 32px) !important
    }

    .mb-md-5 {
        margin-bottom: var(--base-size-32, 32px) !important
    }

    .mr-md-5 {
        margin-right: var(--base-size-32, 32px) !important
    }

    .ml-md-5 {
        margin-left: var(--base-size-32, 32px) !important
    }

    .mt-md-n5 {
        margin-top: calc(-1*var(--base-size-32, 32px)) !important
    }

    .mb-md-n5 {
        margin-bottom: calc(-1*var(--base-size-32, 32px)) !important
    }

    .mr-md-n5 {
        margin-right: calc(-1*var(--base-size-32, 32px)) !important
    }

    .ml-md-n5 {
        margin-left: calc(-1*var(--base-size-32, 32px)) !important
    }

    .mx-md-5 {
        margin-right: var(--base-size-32, 32px) !important;
        margin-left: var(--base-size-32, 32px) !important
    }

    .my-md-5 {
        margin-top: var(--base-size-32, 32px) !important;
        margin-bottom: var(--base-size-32, 32px) !important
    }

    .m-md-6 {
        margin: var(--base-size-40, 40px) !important
    }

    .mt-md-6 {
        margin-top: var(--base-size-40, 40px) !important
    }

    .mb-md-6 {
        margin-bottom: var(--base-size-40, 40px) !important
    }

    .mr-md-6 {
        margin-right: var(--base-size-40, 40px) !important
    }

    .ml-md-6 {
        margin-left: var(--base-size-40, 40px) !important
    }

    .mt-md-n6 {
        margin-top: calc(-1*var(--base-size-40, 40px)) !important
    }

    .mb-md-n6 {
        margin-bottom: calc(-1*var(--base-size-40, 40px)) !important
    }

    .mr-md-n6 {
        margin-right: calc(-1*var(--base-size-40, 40px)) !important
    }

    .ml-md-n6 {
        margin-left: calc(-1*var(--base-size-40, 40px)) !important
    }

    .mx-md-6 {
        margin-right: var(--base-size-40, 40px) !important;
        margin-left: var(--base-size-40, 40px) !important
    }

    .my-md-6 {
        margin-top: var(--base-size-40, 40px) !important;
        margin-bottom: var(--base-size-40, 40px) !important
    }

    .mt-md-7 {
        margin-top: var(--base-size-48, 48px) !important
    }

    .mb-md-7 {
        margin-bottom: var(--base-size-48, 48px) !important
    }

    .mt-md-n7 {
        margin-top: calc(-1*var(--base-size-48, 48px)) !important
    }

    .mb-md-n7 {
        margin-bottom: calc(-1*var(--base-size-48, 48px)) !important
    }

    .my-md-7 {
        margin-top: var(--base-size-48, 48px) !important;
        margin-bottom: var(--base-size-48, 48px) !important
    }

    .mt-md-8 {
        margin-top: var(--base-size-64, 64px) !important
    }

    .mb-md-8 {
        margin-bottom: var(--base-size-64, 64px) !important
    }

    .mt-md-n8 {
        margin-top: calc(-1*var(--base-size-64, 64px)) !important
    }

    .mb-md-n8 {
        margin-bottom: calc(-1*var(--base-size-64, 64px)) !important
    }

    .my-md-8 {
        margin-top: var(--base-size-64, 64px) !important;
        margin-bottom: var(--base-size-64, 64px) !important
    }

    .mt-md-9 {
        margin-top: var(--base-size-80, 80px) !important
    }

    .mb-md-9 {
        margin-bottom: var(--base-size-80, 80px) !important
    }

    .mt-md-n9 {
        margin-top: calc(-1*var(--base-size-80, 80px)) !important
    }

    .mb-md-n9 {
        margin-bottom: calc(-1*var(--base-size-80, 80px)) !important
    }

    .my-md-9 {
        margin-top: var(--base-size-80, 80px) !important;
        margin-bottom: var(--base-size-80, 80px) !important
    }

    .mt-md-10 {
        margin-top: var(--base-size-96, 96px) !important
    }

    .mb-md-10 {
        margin-bottom: var(--base-size-96, 96px) !important
    }

    .mt-md-n10 {
        margin-top: calc(-1*var(--base-size-96, 96px)) !important
    }

    .mb-md-n10 {
        margin-bottom: calc(-1*var(--base-size-96, 96px)) !important
    }

    .my-md-10 {
        margin-top: var(--base-size-96, 96px) !important;
        margin-bottom: var(--base-size-96, 96px) !important
    }

    .mt-md-11 {
        margin-top: var(--base-size-112, 112px) !important
    }

    .mb-md-11 {
        margin-bottom: var(--base-size-112, 112px) !important
    }

    .mt-md-n11 {
        margin-top: calc(-1*var(--base-size-112, 112px)) !important
    }

    .mb-md-n11 {
        margin-bottom: calc(-1*var(--base-size-112, 112px)) !important
    }

    .my-md-11 {
        margin-top: var(--base-size-112, 112px) !important;
        margin-bottom: var(--base-size-112, 112px) !important
    }

    .mt-md-12 {
        margin-top: var(--base-size-128, 128px) !important
    }

    .mb-md-12 {
        margin-bottom: var(--base-size-128, 128px) !important
    }

    .mt-md-n12 {
        margin-top: calc(-1*var(--base-size-128, 128px)) !important
    }

    .mb-md-n12 {
        margin-bottom: calc(-1*var(--base-size-128, 128px)) !important
    }

    .my-md-12 {
        margin-top: var(--base-size-128, 128px) !important;
        margin-bottom: var(--base-size-128, 128px) !important
    }

    .mx-md-auto {
        margin-right: auto !important;
        margin-left: auto !important
    }
}

@media(min-width: 768px) {
    .col-md-1 {
        width: 8.33333333%
    }

    .col-md-2 {
        width: 16.66666666%
    }

    .col-md-3 {
        width: 24.99999999%
    }

    .col-md-4 {
        width: 33.33333332%
    }

    .col-md-5 {
        width: 41.66666665%
    }

    .col-md-6 {
        width: 49.99999998%
    }

    .col-md-7 {
        width: 58.33333331%
    }

    .col-md-8 {
        width: 66.66666664%
    }

    .col-md-9 {
        width: 74.99999997%
    }

    .col-md-10 {
        width: 83.3333333%
    }

    .col-md-11 {
        width: 91.66666663%
    }

    .col-md-12 {
        width: 100%
    }
}

@media(min-width: 768px) {
    .flex-md-row {
        flex-direction: row !important
    }

    .flex-md-row-reverse {
        flex-direction: row-reverse !important
    }

    .flex-md-column {
        flex-direction: column !important
    }

    .flex-md-column-reverse {
        flex-direction: column-reverse !important
    }

    .flex-md-wrap {
        flex-wrap: wrap !important
    }

    .flex-md-nowrap {
        flex-wrap: nowrap !important
    }

    .flex-md-wrap-reverse {
        flex-wrap: wrap-reverse !important
    }

    .flex-md-justify-start {
        justify-content: flex-start !important
    }

    .flex-md-justify-end {
        justify-content: flex-end !important
    }

    .flex-md-justify-center {
        justify-content: center !important
    }

    .flex-md-justify-between {
        justify-content: space-between !important
    }

    .flex-md-justify-around {
        justify-content: space-around !important
    }

    .flex-md-items-start {
        align-items: flex-start !important
    }

    .flex-md-items-end {
        align-items: flex-end !important
    }

    .flex-md-items-center {
        align-items: center !important
    }

    .flex-md-items-baseline {
        align-items: baseline !important
    }

    .flex-md-items-stretch {
        align-items: stretch !important
    }

    .flex-md-content-start {
        align-content: flex-start !important
    }

    .flex-md-content-end {
        align-content: flex-end !important
    }

    .flex-md-content-center {
        align-content: center !important
    }

    .flex-md-content-between {
        align-content: space-between !important
    }

    .flex-md-content-around {
        align-content: space-around !important
    }

    .flex-md-content-stretch {
        align-content: stretch !important
    }

    .flex-md-1 {
        flex: 1 !important
    }

    .flex-md-auto {
        flex: auto !important
    }

    .flex-md-grow-0 {
        flex-grow: 0 !important
    }

    .flex-md-shrink-0 {
        flex-shrink: 0 !important
    }

    .flex-md-self-auto {
        align-self: auto !important
    }

    .flex-md-self-start {
        align-self: flex-start !important
    }

    .flex-md-self-end {
        align-self: flex-end !important
    }

    .flex-md-self-center {
        align-self: center !important
    }

    .flex-md-self-baseline {
        align-self: baseline !important
    }

    .flex-md-self-stretch {
        align-self: stretch !important
    }

    .flex-md-order-1 {
        order: 1 !important
    }

    .flex-md-order-2 {
        order: 2 !important
    }

    .flex-md-order-none {
        order: inherit !important
    }
}

@media(min-width: 1012px) {
    .flex-lg-row {
        flex-direction: row !important
    }

    .flex-lg-row-reverse {
        flex-direction: row-reverse !important
    }

    .flex-lg-column {
        flex-direction: column !important
    }

    .flex-lg-column-reverse {
        flex-direction: column-reverse !important
    }

    .flex-lg-wrap {
        flex-wrap: wrap !important
    }

    .flex-lg-nowrap {
        flex-wrap: nowrap !important
    }

    .flex-lg-wrap-reverse {
        flex-wrap: wrap-reverse !important
    }

    .flex-lg-justify-start {
        justify-content: flex-start !important
    }

    .flex-lg-justify-end {
        justify-content: flex-end !important
    }

    .flex-lg-justify-center {
        justify-content: center !important
    }

    .flex-lg-justify-between {
        justify-content: space-between !important
    }

    .flex-lg-justify-around {
        justify-content: space-around !important
    }

    .flex-lg-items-start {
        align-items: flex-start !important
    }

    .flex-lg-items-end {
        align-items: flex-end !important
    }

    .flex-lg-items-center {
        align-items: center !important
    }

    .flex-lg-items-baseline {
        align-items: baseline !important
    }

    .flex-lg-items-stretch {
        align-items: stretch !important
    }

    .flex-lg-content-start {
        align-content: flex-start !important
    }

    .flex-lg-content-end {
        align-content: flex-end !important
    }

    .flex-lg-content-center {
        align-content: center !important
    }

    .flex-lg-content-between {
        align-content: space-between !important
    }

    .flex-lg-content-around {
        align-content: space-around !important
    }

    .flex-lg-content-stretch {
        align-content: stretch !important
    }

    .flex-lg-1 {
        flex: 1 !important
    }

    .flex-lg-auto {
        flex: auto !important
    }

    .flex-lg-grow-0 {
        flex-grow: 0 !important
    }

    .flex-lg-shrink-0 {
        flex-shrink: 0 !important
    }

    .flex-lg-self-auto {
        align-self: auto !important
    }

    .flex-lg-self-start {
        align-self: flex-start !important
    }

    .flex-lg-self-end {
        align-self: flex-end !important
    }

    .flex-lg-self-center {
        align-self: center !important
    }

    .flex-lg-self-baseline {
        align-self: baseline !important
    }

    .flex-lg-self-stretch {
        align-self: stretch !important
    }

    .flex-lg-order-1 {
        order: 1 !important
    }

    .flex-lg-order-2 {
        order: 2 !important
    }

    .flex-lg-order-none {
        order: inherit !important
    }
}

.avatar {
    background-color: var(--avatar-bgColor);
    border-radius: var(--borderRadius-medium);
    box-shadow: 0 0 0 1px var(--avatar-borderColor);
    display: inline-block;
    flex-shrink: 0;
    line-height: 1;
    overflow: hidden;
    vertical-align: middle
}

.avatar-user {
    border-radius: 50% !important
}

.width-full {
    width: 100% !important
}

.border {
    border: var(--borderWidth-thin, 1px) solid var(--borderColor-default) !important
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

.vcard-fullname {
    font-size: 24px;
    line-height: 1.25
}

.vcard-username {
    font-size: 20px;
    font-style: normal;
    font-weight: var(--base-text-weight-light, 300);
    line-height: 24px;
    color: var(--fgColor-muted)
}

.vcard-names {
    line-height: 1
}

.float-left {
    float: left !important
}

.float-right {
    float: right !important
}

.float-none {
    float: none !important
}

.overflow-hidden {
    overflow: hidden !important
}

.d-md-block {
    display: block !important
}

.flex-column {
    flex-direction: column !important
}

.flex-order-1 {
    order: 1 !important
}

.flex-md-order-none {
    order: inherit !important
}

.mb-0 {
    margin-bottom: 0 !important
}

.mb-n1 {
    margin-bottom: calc(-1*var(--base-size-4, 4px)) !important
}

.flex-1 {
    flex: 1 !important
}

.pb-1 {
    padding-bottom: var(--base-size-4, 4px) !important
}

.user-following-container .follow,
.user-following-container.on .unfollow {
    display: inline-block
}

.user-following-container.on .follow,
.user-following-container .unfollow {
    display: none
}

.user-following-container.loading {
    opacity: .5
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