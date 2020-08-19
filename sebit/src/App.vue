<template>
  <div id="app">
    <div class="button-container">
      <a class="btn-grey">Follow Demo</a>
      <a class="btn-blue">
        <svg
          class="svg-logo logo-tumblr"
          width="64"
          height="15px"
          viewBox="0 0 245 50"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
        >
          <g
            class="logotype"
            stroke="none"
            stroke-width="1"
            fill="#ffffff"
            fill-rule="evenodd"
          >
            <path
              d="M28.087 49.57h-8.286c-7.461 0-13.021-3.835-13.021-13.01V21.863H0v-7.957C7.461 11.97 10.582 5.556 10.94 0h7.749v12.616h9.04v9.248h-9.04v12.795c0 3.836 1.937 5.162 5.022 5.162h4.376v9.749zm143.951.43c-3.766 0-7.246-1.254-10.151-3.692v3.262h-11.372V7.993h-4.95V0h17.075v15.305c2.224-1.72 5.919-3.119 9.613-3.119 10.51 0 15.676 7.312 15.676 18.46 0 11.612-5.56 19.354-15.89 19.354zm18.115-.43v-7.921h4.197V7.993h-4.95V0h16.93v41.649h4.377v7.92h-20.554zm-112.456 0v-7.921h4.197V20.68h-4.95v-8.065H92.26V17.6c2.582-3.549 7.39-5.413 11.765-5.413 5.525 0 9.22 2.223 11.658 5.914 1.938-3.261 6.529-5.914 12.125-5.914 11.335 0 14.205 8.961 14.205 16.56v12.903h4.125v7.92h-20.16v-7.92h4.054V27.348c0-3.047-1.04-5.628-5.309-5.628-5.273 0-6.816 4.122-6.816 6.13v13.799h4.233v7.92h-20.267v-7.92H106V27.348c0-3.047-.86-5.628-5.093-5.628-5.238 0-6.96 4.122-6.96 6.13v13.799h4.162v7.92H77.697zm137.494 0v-7.921h4.09V20.68h-4.449v-8.065h15.39v5.341c1.9-3.548 6.133-5.77 10.725-5.77H245V22.76h-5.022c-3.766 0-8.717 1.541-8.717 8.566V41.65h4.126v7.92H215.19zM47.53 50c-11.765 0-14.348-8.853-14.348-14.552V12.616h12.411v22.33c0 3.083.754 5.52 4.807 5.52 6.313 0 7.246-4.695 7.246-5.807V20.681h-4.807v-8.065h16.86V41.65h3.55v7.92H59.296V44.91C56.641 48.172 51.762 50 47.529 50zm121.926-8.996c1.902-.215 6.278-.538 6.278-10.287 0-6.774-2.978-9.498-6.35-9.498-2.905 0-7.102 1.54-7.102 10.25 0 7.24 3.551 9.535 7.174 9.535z"
              fill-rule="evenodd"
            />
          </g>
        </svg>
      </a>
    </div>
    <div class="container">
      <headerSection></headerSection>
      <section class="main-content-container">
        <div class="posts-container">
          <div
            v-for="(value, post) in filteredPosts"
            :key="post.id"
            class="posts-sub-container"
          >
            <h2>{{ value.tumblelog.title }}</h2>
            <p v-if="value.type == `quote`">{{ value["quote-text"] }}</p>
            <img
              v-if="value.type == `photo`"
              :src="value['photo-url-100']"
              alt
            />
            <p>{{ value.date | moment("DD/mm/YYYY") }}</p>
            <a @click="openNewTab(value.url)">Read More</a>
            <a>Read as Modal </a>
          </div>
        </div>
        <div class="sidebar">
          <input type="text" />
          <button>Search</button>
          <p class="text-lorem">
            Lorem ipsum dolor sit amet, consectetuer adipiscing elit
            <wbr />, sed diam nonummy nibh euismod tincidunt ut laoreet dolore
            magna aliquam erat volutpat.
            <wbr />
          </p>
          <h3>Filter</h3>
          <h3>
            Toplamda {{ posts[0]["posts-total"] }} adet post bulunmaktadır.
          </h3>
          <div class="filters">
            <a @click="activeFilter = `photo`">Photo</a>
            <a @click="activeFilter = `link`">Link</a>
            <a @click="activeFilter = `quote`">Quote</a>
            <a @click="activeFilter = ``">Clear</a>
          </div>

          <span></span>
          <a href>Archive</a>
        </div>
      </section>
      <footer>
        <a>Powered by Tumblr</a>
      </footer>
    </div>
  </div>
</template>

<script>
import headerSection from "./components/headerSection";
import axios from "axios";

export default {
  created() {
    this.getPosts();
  },
  data() {
    return {
      activeFilter: "",
      methods: {},

      posts: [
        {
          tumblelog: {
            title: "Demo",
            description:
              "Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.",
            name: "demo",
            timezone: "US/Eastern",
            cname: false,
            feeds: [],
          },
          "posts-start": 0,
          "posts-total": 7,
          "posts-type": false,
          posts: [
            {
              id: "236",
              url: "https://demo.tumblr.com/post/236",
              "url-with-slug":
                "https://demo.tumblr.com/post/236/it-does-not-matter-how-slow-you-go-so-long-as-you",
              type: "quote",
              "date-gmt": "2006-11-08 19:27:00 GMT",
              date: "Wed, 08 Nov 2006 14:27:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1163014020,
              format: "html",
              "reblog-key": "iKvmNy9T",
              slug: "it-does-not-matter-how-slow-you-go-so-long-as-you",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="236" data-blog-name="demo" id="like_button_236"><iframe id="like_iframe_236" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=236&amp;color=black&amp;rk=iKvmNy9T" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_236"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/236/iKvmNy9T" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "108138",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "quote-text":
                "It does not matter how slow you go so long as you do not stop.",
              "quote-source":
                'Wisdom of\u00a0<a href="http://en.wikipedia.org/wiki/Confucius">Confucius</a>',
              tags: ["wisdom"],
            },
            {
              id: "459265350",
              url: "https://demo.tumblr.com/post/459265350",
              "url-with-slug":
                "https://demo.tumblr.com/post/459265350/passing-through-times-square-by-mareen-fischinger",
              type: "photo",
              "date-gmt": "2006-11-08 19:26:00 GMT",
              date: "Wed, 08 Nov 2006 14:26:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1163013960,
              format: "html",
              "reblog-key": "gOMUPmdx",
              slug: "passing-through-times-square-by-mareen-fischinger",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="459265350" data-blog-name="demo" id="like_button_459265350"><iframe id="like_iframe_459265350" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=459265350&amp;color=black&amp;rk=gOMUPmdx" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_459265350"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/459265350/gOMUPmdx" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "46641",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "photo-caption":
                '<p>Passing through Times Square by\u00a0<a href="http://www.mareenfischinger.com/">Mareen Fischinger</a></p>',
              width: 1280,
              height: 853,
              "photo-url-1280":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_1280.jpg",
              "photo-url-500":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_500.jpg",
              "photo-url-400":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_400.jpg",
              "photo-url-250":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_250.jpg",
              "photo-url-100":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_100.jpg",
              "photo-url-75":
                "https://66.media.tumblr.com/tumblr_kzjlfiTnfe1qz4rgho1_75sq.jpg",
              photos: [],
              tags: ["Mareen Fischinger", "New York City", "Times Square"],
            },
            {
              id: "234",
              url: "https://demo.tumblr.com/post/234",
              "url-with-slug":
                "https://demo.tumblr.com/post/234/my-favorite-web-site",
              type: "link",
              "date-gmt": "2006-11-08 19:25:00 GMT",
              date: "Wed, 08 Nov 2006 14:25:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1163013900,
              format: "html",
              "reblog-key": "as2i9gTb",
              slug: "my-favorite-web-site",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="234" data-blog-name="demo" id="like_button_234"><iframe id="like_iframe_234" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=234&amp;color=black&amp;rk=as2i9gTb" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_234"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/234/as2i9gTb" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "9606",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "link-text": "My favorite web site",
              "link-url": "http://",
              "link-description":
                "<p>Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.</p>",
            },
            {
              id: "233",
              url: "https://demo.tumblr.com/post/233",
              "url-with-slug":
                "https://demo.tumblr.com/post/233/jack-hey-you-know-what-sucks-lindsey",
              type: "conversation",
              "date-gmt": "2006-11-08 19:24:00 GMT",
              date: "Wed, 08 Nov 2006 14:24:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1163013840,
              format: "html",
              "reblog-key": "5eI0YaaG",
              slug: "jack-hey-you-know-what-sucks-lindsey",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="233" data-blog-name="demo" id="like_button_233"><iframe id="like_iframe_233" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=233&amp;color=black&amp;rk=5eI0YaaG" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_233"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/233/5eI0YaaG" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "46533",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "conversation-title": null,
              "conversation-text":
                "Jack: Hey, you know what sucks?\nLindsey: vacuums\nJack: Hey, you know what sucks in a metaphorical sense?\nLindsey: black holes\nJack: Hey, you know what just isn't cool?\nLindsey: lava?",
              conversation: [
                {
                  name: "Jack",
                  label: "Jack:",
                  phrase: "Hey, you know what sucks?",
                },
                {
                  name: "Lindsey",
                  label: "Lindsey:",
                  phrase: "vacuums",
                },
                {
                  name: "Jack",
                  label: "Jack:",
                  phrase: "Hey, you know what sucks in a metaphorical sense?",
                },
                {
                  name: "Lindsey",
                  label: "Lindsey:",
                  phrase: "black holes",
                },
                {
                  name: "Jack",
                  label: "Jack:",
                  phrase: "Hey, you know what just isn't cool?",
                },
                {
                  name: "Lindsey",
                  label: "Lindsey:",
                  phrase: "lava?",
                },
              ],
              tags: ["funny"],
            },
            {
              id: "459260683",
              url: "https://demo.tumblr.com/post/459260683",
              "url-with-slug":
                "https://demo.tumblr.com/post/459260683/allison-weiss-fingers-crossed",
              type: "audio",
              "date-gmt": "2006-11-07 19:23:00 GMT",
              date: "Tue, 07 Nov 2006 14:23:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1162927380,
              format: "html",
              "reblog-key": "wEe8GcU4",
              slug: "allison-weiss-fingers-crossed",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="459260683" data-blog-name="demo" id="like_button_459260683"><iframe id="like_iframe_459260683" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=459260683&amp;color=black&amp;rk=wEe8GcU4&amp;root_id=228022847" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_459260683"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/459260683/wEe8GcU4" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "15132",
              "reblogged-from-url":
                "https://aw-archives.tumblr.com/post/228022847/allison-weiss-fingers-crossed-from-the-2009",
              "reblogged-from-name": "aw-archives",
              "reblogged-from-title": "A.W. Tumblr",
              reblogged_from_avatar_url_512:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_512.png",
              reblogged_from_avatar_url_128:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_128.png",
              reblogged_from_avatar_url_96:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_96.png",
              reblogged_from_avatar_url_64:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_64.png",
              reblogged_from_avatar_url_48:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_48.png",
              reblogged_from_avatar_url_40:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_40.png",
              reblogged_from_avatar_url_30:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_30.png",
              reblogged_from_avatar_url_24:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_24.png",
              reblogged_from_avatar_url_16:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_16.png",
              "reblogged-root-url":
                "https://aw-archives.tumblr.com/post/228022847/allison-weiss-fingers-crossed-from-the-2009",
              "reblogged-root-name": "aw-archives",
              "reblogged-root-title": "A.W. Tumblr",
              reblogged_root_avatar_url_512:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_512.png",
              reblogged_root_avatar_url_128:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_128.png",
              reblogged_root_avatar_url_96:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_96.png",
              reblogged_root_avatar_url_64:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_64.png",
              reblogged_root_avatar_url_48:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_48.png",
              reblogged_root_avatar_url_40:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_40.png",
              reblogged_root_avatar_url_30:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_30.png",
              reblogged_root_avatar_url_24:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_24.png",
              reblogged_root_avatar_url_16:
                "https://66.media.tumblr.com/avatar_4fbd50d1259e_16.png",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "id3-artist": "Allison Weiss",
              "id3-album": "...Was Right All Along",
              "id3-year": "2009",
              "id3-track": "2 of 10",
              "id3-title": "Fingers Crossed",
              "audio-caption":
                '<p><strong><a href="http://allisonweiss.tumblr.com/">Allison Weiss</a>\u00a0\u2014</strong> Fingers Crossed</p>',
              "audio-player":
                '<iframe class="tumblr_audio_player tumblr_audio_player_459260683" src="https://demo.tumblr.com/post/459260683/audio_player_iframe/demo/tumblr_ksc4i2SkVU1qz8ouq?audio_file=https%3A%2F%2Fa.tumblr.com%2Ftumblr_ksc4i2SkVU1qz8ouqo1_r2.mp3" frameborder="0" allowtransparency="true" scrolling="no" width="540" height="169"></iframe>',
              "audio-embed":
                '<iframe class="tumblr_audio_player tumblr_audio_player_459260683" src="https://demo.tumblr.com/post/459260683/audio_player_iframe/demo/tumblr_ksc4i2SkVU1qz8ouq?audio_file=https%3A%2F%2Fa.tumblr.com%2Ftumblr_ksc4i2SkVU1qz8ouqo1_r2.mp3" frameborder="0" allowtransparency="true" scrolling="no" width="540" height="169"></iframe>',
              "audio-plays": 0,
            },
            {
              id: "232",
              url: "https://demo.tumblr.com/post/232",
              "url-with-slug":
                "https://demo.tumblr.com/post/232/an-example-post",
              type: "regular",
              "date-gmt": "2006-11-07 19:22:00 GMT",
              date: "Tue, 07 Nov 2006 14:22:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1162927320,
              format: "html",
              "reblog-key": "jaHD5AfB",
              slug: "an-example-post",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="232" data-blog-name="demo" id="like_button_232"><iframe id="like_iframe_232" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=232&amp;color=black&amp;rk=jaHD5AfB" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_232"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/232/jaHD5AfB" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "24294",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "regular-title": "An example post",
              "regular-body":
                '<p>Lorem ipsum dolor sit amet, consectetuer <a href="/">adipiscing elit</a>. Aliquam nisi lorem, pulvinar id, commodo feugiat, vehicula et, mauris. Aliquam mattis porta urna. Maecenas dui neque, rhoncus sed, vehicula vitae, auctor at, nisi. Aenean id massa ut lacus molestie porta. Curabitur sit amet quam id libero suscipit venenatis.</p>\n<ul><li>Lorem ipsum dolor sit amet.</li>\n<li>Consectetuer adipiscing elit. </li>\n<li>Nam at tortor quis ipsum tempor aliquet.</li>\n</ul><p>Cum sociis <a href="/">natoque penatibus</a> et magnis dis parturient montes, nascetur ridiculus mus. Suspendisse sed ligula. Sed volutpat odio non turpis gravida luctus. Praesent elit pede, iaculis facilisis, vehicula mattis, tempus non, arcu.</p>\n<blockquote>Donec placerat mauris commodo dolor. Nulla tincidunt. Nulla vitae augue.</blockquote>\n<p>Suspendisse ac pede. Cras <a href="/">tincidunt pretium</a> felis. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Pellentesque porttitor mi id felis. Maecenas nec augue. Praesent a quam pretium leo congue accumsan.</p>',
            },
            {
              id: "459009076",
              url: "https://demo.tumblr.com/post/459009076",
              "url-with-slug":
                "https://demo.tumblr.com/post/459009076/lorem-ipsum-dolor-sit-amet-consectetuer",
              type: "regular",
              "date-gmt": "2006-10-01 04:00:00 GMT",
              date: "Sun, 01 Oct 2006 00:00:00",
              bookmarklet: 0,
              mobile: 0,
              "feed-item": "",
              "from-feed-id": 0,
              "unix-timestamp": 1159675200,
              format: "html",
              "reblog-key": "uHt0TEhP",
              slug: "lorem-ipsum-dolor-sit-amet-consectetuer",
              "is-submission": false,
              "like-button":
                '<div class="like_button" data-post-id="459009076" data-blog-name="demo" id="like_button_459009076"><iframe id="like_iframe_459009076" src="https://assets.tumblr.com/assets/html/like_iframe.html?_v=66c22ab5319d742bca5762b8d18f9d06#name=demo&amp;post_id=459009076&amp;color=black&amp;rk=uHt0TEhP" scrolling="no" width="20" height="20" frameborder="0" class="like_toggle" allowTransparency="true" name="like_iframe_459009076"></iframe></div>',
              "reblog-button":
                '<a href="https://www.tumblr.com/reblog/459009076/uHt0TEhP" class="reblog_button"style="display: block;width:20px;height:20px;"><svg width="100%" height="100%" viewBox="0 0 21 21" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><path d="M5.01092527,5.99908429 L16.0088498,5.99908429 L16.136,9.508 L20.836,4.752 L16.136,0.083 L16.1360004,3.01110845 L2.09985349,3.01110845 C1.50585349,3.01110845 0.979248041,3.44726568 0.979248041,4.45007306 L0.979248041,10.9999998 L3.98376463,8.30993634 L3.98376463,6.89801007 C3.98376463,6.20867902 4.71892527,5.99908429 5.01092527,5.99908429 Z"></path><path d="M17.1420002,13.2800293 C17.1420002,13.5720293 17.022957,14.0490723 16.730957,14.0490723 L4.92919922,14.0490723 L4.92919922,11 L0.5,15.806 L4.92919922,20.5103758 L5.00469971,16.9990234 L18.9700928,16.9990234 C19.5640928,16.9990234 19.9453125,16.4010001 19.9453125,15.8060001 L19.9453125,9.5324707 L17.142,12.203"></path></svg></a>',
              "note-count": "9029",
              tumblelog: {
                title: "Demo",
                name: "demo",
                cname: false,
                url: "https://demo.tumblr.com/",
                timezone: "US/Eastern",
                avatar_url_512:
                  "https://assets.tumblr.com/images/default_avatar_512.png",
                avatar_url_128:
                  "https://assets.tumblr.com/images/default_avatar_128.png",
                avatar_url_96:
                  "https://assets.tumblr.com/images/default_avatar_96.png",
                avatar_url_64:
                  "https://assets.tumblr.com/images/default_avatar_64.png",
                avatar_url_48:
                  "https://assets.tumblr.com/images/default_avatar_48.png",
                avatar_url_40:
                  "https://assets.tumblr.com/images/default_avatar_40.png",
                avatar_url_30:
                  "https://assets.tumblr.com/images/default_avatar_30.png",
                avatar_url_24:
                  "https://assets.tumblr.com/images/default_avatar_24.png",
                avatar_url_16:
                  "https://assets.tumblr.com/images/default_avatar_16.png",
              },
              "regular-title": null,
              "regular-body":
                '<p>Lorem ipsum dolor sit amet, consectetuer <a href="/">adipiscing elit</a>. Aliquam nisi lorem, pulvinar id, commodo feugiat, vehicula et, mauris. Aliquam mattis porta urna. Maecenas dui neque, rhoncus sed, vehicula vitae, auctor at, nisi. Aenean id massa ut lacus molestie porta. Curabitur sit amet quam id libero suscipit venenatis.</p>',
            },
          ],
        },
      ],
    };
  },
  name: "App",
  components: {
    headerSection,
  },
  computed: {
    filteredPosts() {
      if (this.activeFilter == "") {
        return this.posts[0].posts;
      }
      return this.posts[0].posts.filter(
        (post) => post.type == this.activeFilter
      );
    },
  },

  methods: {
    openNewTab(openlink) {
      window.open(openlink, "_blank");
    },
    getPosts() {
      axios
        .get("https://demo.tumblr.com/api/read/json?debug=1")
        .then((response) => (this.posts = response.data))
        .catch((error) => {
          this.errors.push(error);
        });
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: Helvetica, Arial, sans-serif;
}

a {
  color: var(--main-grey);
  text-decoration: none;
}
a:hover {
  cursor: pointer;
}

/*VARIABLES START*/

:root {
  --main-blue: #6498cc;
  --main-grey: rgba(68, 68, 68, 0.4);
  --main-deep-blue: #001935;
}

.container {
  display: grid;
  justify-content: center;
  row-gap: 20px;
}

.button-container {
  position: fixed;
  top: 0;
  right: 0;
  padding: 15px;
  display: grid;
  grid-auto-flow: column;
  column-gap: 10px;
}
.posts-container {
  display: grid;
}
.main-content-container {
  display: grid;
  grid-auto-flow: column;
}

.sidebar {
  max-width: 160px;
  text-align: right;
}

.posts-sub-container {
  display: grid;
}

.btn-grey {
  background: var(--main-grey);
  color: white;
  padding: 6px 12px;
  border-radius: 5px;
  font-weight: bold;
  display: grid;
  place-items: center;
}

.btn-blue {
  background: var(--main-deep-blue);
  border-radius: 5px;
  padding: 8px;
}

footer {
  padding: 20px;

  bottom: 0;
  width: calc(100% - 20px);
  text-align: center;
}
.date-container {
  display: grid;
  grid-auto-flow: column;
  column-gap: 10px;
  align-items: start;
}
.date {
  background: var(--main-blue);
  color: white;
  font-weight: bold;
  padding: 5px;
}

.day {
  color: var(--main-grey);
  font-size: 2.125rem;
}

.filters {
  display: grid;
}
</style>
