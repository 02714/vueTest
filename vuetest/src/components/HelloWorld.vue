<template>
 <div class="a">
   <!-- 搜索功能 -->
   <form action="">
     <div class="bar">
       <input type="text" v-model="search" placeholder="搜索">
     </div>
     <ul>
       <!-- 循环输出数据 -->
       <li v-for="article in filteredArticles" :key="article.title">
         <img v-bind:src="article.image" alt="">
         <p>{{article.title}}</p>
       </li>
     </ul>
   </form>
 </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
          search:'',
    articles:[
            {
              "title":"What You Need To Know About Css Variables",
              "image":"https://static.runoob.com/images/icon/css.png"
            },
            {
                "title": "Freebie: 4 Great Looking Pricing Tables",
                "image": "https://static.runoob.com/images/icon/html.png"
            },
            {
                "title": "20 Interesting JavaScript and CSS Libraries for February 2016",
                "image": "https://static.runoob.com/images/icon/css3.png"
            },
            {
                "title": "Quick Tip: The Easiest Way To Make Responsive Headers",
                "image": "https://static.runoob.com/images/icon/css3.png"
            },
            {
                "title": "Learn SQL In 20 Minutes",
                "image": "https://static.runoob.com/images/icon/sql.png"
            },
            {
                "title": "Creating Your First Desktop App With HTML, JS and Electron",
                "image": "https://static.runoob.com/images/icon/html.png"
            }
    ]
    }
  },
  computed:{
    filteredArticles:function(){
      var articles_array = this.articles,
      search = this.search;

      if(!search){
        return articles_array;
      }

      search = search.trim().toLowerCase();

      articles_array = articles_array.filter(function(item){
        if(item.title.toLowerCase().indexOf(search) !== -1){
          return item;
        }
      })
      return articles_array;;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 auto;
  display: flex;
  justify-content: flex-start;
  align-items: center;

}
a {
  color: #42b983;
}

</style>
