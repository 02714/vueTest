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
   <!-- 增删改 -->
   <div class="ZSG">
     <div class="add">
      <input type="text" placeholder="Tittle" v-model="input.name">
      <input type="text" placeholder="Publisher" v-model="input.user">
      <input type="date" placeholder="Releasetime" v-model="input.date">
      <button :disabled="!input.name||!input.user||!input.date"  @click="addItem()">新增</button>      
    </div>
    <table cellpadding="0" cellspacing="0">
      <thead>
        <tr>
          <th><input type="checkbox" v-model="checkALL" @change="selectAllItem()">序号</th>
          <th>Tittle</th>
          <th>Publisher</th>
          <th>Releasetime</th>
          <th>Oprate</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(v,i) in items" :key="v.id">
          <td> <input type="checkbox" v-model="v.check" @change="selectItem(v)">{{v.id}}</td>
          <td>{{v.name}}</td>
          <td>{{v.user}}</td>
          <td>{{v.date}}</td>
          <td>
            <button @click="delItem(i)">Delete</button>
            <button @click="updateShow(v)">Edit</button>
          </td>
        </tr>
      </tbody>
    </table>
    <div id="layer" v-show="flag">
      <div class="mask">
        <div class="Tittle">
          Edit
          <span @click="flag=false">x</span>
        </div>
        <div class="content">
          <input type="text" placeholder="Tittle" v-model="edit.name">
          <input type="text" placeholder="Publisher" v-model="edit.user">
          <input type="date" placeholder="Releasetime" v-model="edit.date">
          <button @click="updateItem()" :disabled="!edit.name||!edit.user||!edit.date">Update</button>
          <button @click="flag=false">Cancle</button>
        </div>
      </div>
    </div>
</div>
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
          check:false,
          flag:false,
          isShow:false,
          checkALL:false,
          //搜索数据
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
                ],
                input:{
                  name:'',
                  user:'',
                  date:'',
                  check:false,
                },
                items:[
                  {name:'增删改查',user:'叽哩哗啦',date:'2302-05-04',id:1,check:false},
                  {name:'增改',user:'咕哩哗啦',date:'2320-04-05',id:2,check:false}
                ],
                edit:{
                  name:'',
                  user:'',
                  date:'',
                  check:false,
                },
        }
  },
  methods:{
        showToggle:function(){
            this.isShow = !this.isShow
            console.log('power!!!!')
        },

        addItem(){
          var _id = Math.max (...this.items.map(v => v.id)) +1;
          var {name,user,date,check} = this.input;
          this.items.push({
            name,
            user,
            date,
            id:_id,
            check,
          })
        },
        selectAllItem(){
          this.items.forEach(v =>{ v.check = this.checkALL});
  
        },
        selectItem(v){
          this.checkALL = this.items.every(v => v.check)
        },
        // 删除
        delItem(i){
          this.items = this.items.filter((v,index) => index != 1)
        },
        // 修改
        updateShow(v){
          this.flag = true;
          this.edit={
            name: v.name,
            user: v.user,
            date: v.user,
            id: v.id,
            check:v.check,
          }
        },
        updateItem(){
          var {name,user,date,id,check} = this.edit;
          this.items.forEach((v,i) => {
            if(v.id == id){
              v.name = name;
              v.user = user,
              v.date = date,
              v.id = id,
              v.check = check
            }
          })
          this.flag = false
        },
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
input{
  width: 200px;
  margin: 10px;
  padding: 8px 8px;
  border-radius: 5px;
}
button{
  border-radius: 5px;
  width: 60px;
  height: 30px;
  margin: 10px 0 0 10px;
}
table{
  margin: 0 auto;
}
</style>
