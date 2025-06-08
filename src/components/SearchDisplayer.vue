<script>
import "../assets/main.css";
export default {
    name: "SearchDisplayer",
    props: {userData:Object,recentCreatedRepo:{type:Array,default: () => {}},recentCreatedRepoWithLanguage:{type:Object,default: () => {}}, gitt:String}, 
    data: function () {
        return {
            languageFrameworkColors : {
                "javascript": "#f1e05a",
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
        displayDescriptionTOPinnedRepos(description=""){
            if(description.length>220){
                let des = "";
                for(let iterator = 0;iterator<=220;iterator++){
                    if(description.length === iterator+1) break;
                    des+=description[iterator];
                }
                des+= "...";
                return des;
            }
            else{
                return description;
            }
        }
    }
}
</script>

<template>
    <div class="application-main ">
        <main>
            <div class="container-xl px-3 px-md-4 px-lg-5 mt-2">
                <div
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
                                    </div>

                                </div>

                                <div class="border-top color-border-muted pt-3 mt-3 d-none d-md-block">
                                    <h2 class="h4 mb-2"><a href="/a-x-r-o-n?tab=achievements"
                                        class="Link--primary mb-2">Achievements</a></h2>
                                    <div class="d-flex flex-wrap"><a href="/a-x-r-o-n?achievement=pull-shark&amp;tab=achievements"
                                        class="position-relative"><img
                                        src="https://github.githubassets.com/assets/pull-shark-default-498c279a747d.png"
                                        data-hovercard-type="achievement"
                                        data-hovercard-url="/users/a-x-r-o-n/achievements/pull-shark/detail?hovercard=1" width="64"
                                        alt="Achievement: Pull Shark" data-view-component="true"
                                        class="achievement-badge-sidebar" /></a><a
                                        href="/a-x-r-o-n?achievement=quickdraw&amp;tab=achievements" class="position-relative"><img
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

                    <div data-view-component="true" class="Layout-main">
                        <div class="Box mt-4 ">
                            <div class="Box-body p-4">
                                <div class="d-flex flex-justify-between">
                                    <div class="text-mono text-small mb-3">
                                        <a href="/soniyav20/soniyav20" class="no-underline Link--primary">{{userData?userData["login"]:'a'}}</a><span
                            class="color-fg-muted d-inline-block" style="padding:0px 2px;">/</span>README<span
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
                                        data-canonical-src="https://github-readme-streak-stats.herokuapp.com/?user=soniyav20&amp;theme=transparent&amp;hide_border=false"
                                        style="max-width: 100%;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/dd64b5d220a8bf4445005a129d1bf452c9cc671429974d0bc971e2d2221a0088/68747470733a2f2f6769746875622d726561646d652d73746174732e76657263656c2e6170702f6170693f757365726e616d653d736f6e697961763230267468656d653d6461726b26686964655f626f726465723d66616c736526696e636c7564655f616c6c5f636f6d6d6974733d7472756526636f756e745f707269766174653d74727565"><img
                                        :src="`https://github-readme-stats.vercel.app/api?username=${userData?userData['login']:'a'}&theme=transparent&hide_border=true`"
                                        alt=""
                                        data-canonical-src="https://github-readme-stats.vercel.app/api?username=soniyav20&amp;theme=transparent&amp;hide_border=false&amp;include_all_commits=true&amp;count_private=true"
                                        style="max-width: 100%;"></a>
                                    </p>

                                    <p dir="auto" style="display: flex; justify-content: space-evenly;">
                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/ab960ba950334e2f3f537e77c2bd1aa515b9bb7df044a06074edaab906692524/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f7265706f732d7065722d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=soniyav20&amp;theme=transparent"
                                        style="max-width: auto;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/fd66e543ec4e2f73c5a4c5ced3a590f8f69d3a8ffc47ef2bd7bcdc567aa6db90/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f70726f647563746976652d74696d653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=soniyav20&amp;theme=transparent"
                                        style="max-width: auto;"></a>

                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/af6d93cce46283b585fffba7f1ff9d55fb329eef0013975ca8a316705a3a0ded/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f6d6f73742d636f6d6d69742d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=${userData?userData['login']:'a'}&theme=transparent`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=soniyav20&amp;theme=transparent"
                                        style="max-width: 100%;"></a>
                                    </p>
                                    <!-- <p dir="auto" style="display: flex; justify-content: space-evenly;">
                                        <a target="_blank" rel="noopener noreferrer nofollow"
                                        href="https://camo.githubusercontent.com/ab960ba950334e2f3f537e77c2bd1aa515b9bb7df044a06074edaab906692524/687474703a2f2f6769746875622d70726f66696c652d73756d6d6172792d63617264732e76657263656c2e6170702f6170692f63617264732f7265706f732d7065722d6c616e67756167653f757365726e616d653d736f6e697961763230267468656d653d6769746875625f6461726b"><img
                                        :src="`https://github-readme-stats.vercel.app/api/wakatime?username=${userData?userData['login']:''}&theme=transparent&hide_border=true`"
                                        data-canonical-src="http://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=soniyav20&amp;theme=transparent"
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
                                        data-canonical-src="https://github-profile-trophy.vercel.app/?username=soniyav20&amp;theme=radical&amp;no-frame=false&amp;no-bg=false&amp;margin-w=4"
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
                                    href="/soniyav20/name_generator" data-view-component="true"
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

                                <a href="/soniyav20/name_generator/stargazers" class="pinned-item-meta Link--muted">
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

                        
                      </ol>

                      <!-- <ol class="d-flex flex-wrap list-style-none gutter-condensed mb-4">

                        <li class="mb-3 d-flex flex-content-stretch col-12 col-md-6 col-lg-6">
                          <div class="Box pinned-item-list-item d-flex p-3 width-full public source">
                            <div class="pinned-item-list-item-content">
                              <div class="d-flex v-align-middle mr-2">
                                <span data-view-component="true" class="position-relative"><a id="410462296"
                                    href="/soniyav20/name_generator" data-view-component="true"
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

                                <a href="/soniyav20/name_generator/stargazers" class="pinned-item-meta Link--muted">
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
                                    href="/soniyav20/login_app" data-view-component="true"
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

                                <a href="/soniyav20/login_app/stargazers" class="pinned-item-meta Link--muted">
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
                                    href="/soniyav20/voice_to_text" data-view-component="true"
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

                                <a href="/soniyav20/voice_to_text/stargazers" class="pinned-item-meta Link--muted">
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
                                    href="/soniyav20/ml_image_classification" data-view-component="true"
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

                                <a href="/soniyav20/ml_image_classification/stargazers"
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
                                    href="/soniyav20/sih_isl" data-view-component="true"
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

                                <a href="/soniyav20/sih_isl/stargazers" class="pinned-item-meta Link--muted">
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
                                    href="/soniyav20/dlc_lab_exps" data-view-component="true"
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

                                <a href="/soniyav20/dlc_lab_exps/stargazers" class="pinned-item-meta Link--muted">
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



                </div>
            </div>
        </main>
    </div>
</template>

<style scoped>


.Button-content {
    align-items: center;
    display: grid;
    flex: 1 0 auto;
    grid-template-areas: "leadingVisual text trailingVisual";
    grid-template-columns: min-content minmax(0, auto) min-content;
    place-content: center
}

.Button-content>:not(:last-child) {
    margin-right: var(--control-medium-gap)
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
</style>