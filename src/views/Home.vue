<template>
  <div class="home">
     <v-container>
       <v-row style="margin: 30px">
         <NewPost @refresh="initData"/>
       </v-row>
      <v-row dense>
        <v-col cols="12" v-for="post, i in posts" :key="i">
          <v-card
            color="#385F73"
            dark
          >
            <v-card-title class="headline">{{post.id}} - {{post.title}}</v-card-title>

            <v-card-subtitle>{{post.body}}</v-card-subtitle>
            <div style="margin: 20px">
              <Comments :post="post"/>
            </div>
            <v-card-actions>
              <EditPost @refresh="initData" :post="post"/>
              <v-btn @click="deletPost(post)" text>Deletar</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
     </v-container>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import EditPost from '@/components/EditPost';
import NewPost from '@/components/NewPost';
import Comments from '@/components/Comments';

export default {
  name: 'home',
  data() {
    return {
      url:"http://localhost:4200/",
      posts: []
    }
  },
  created() {
    var self = this;
    self.initData();
  },
  methods: {
    initData(){
      var self = this;
      this.axios.get(self.url+'posts').then((response) => {
        if(!response.data.Error)
          self.posts = response.data.Data;
        else 
          alert("Problemas com o servidor.")
      })
    },
    deletPost(post){
      var self = this;
      this.axios.delete(self.url+'posts/'+post.id).then((response) => {
        if(!response.data.Error){
          alert(response.data.Message) ;
          self.posts.remove(post);
        }
        else 
          alert("Problemas com o servidor.")
      })
    }
  },
  components: {
    HelloWorld,
    EditPost,
    NewPost,
    Comments
  }
}

</script>
