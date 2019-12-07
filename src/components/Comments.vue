<template>
  

    <v-list three-line>
      <template v-for="(item, index) in items">
        <v-subheader
          v-if="item.header"
          :key="item.header"
          v-text="item.header"
        ></v-subheader>

        <v-divider
          v-else-if="item.divider"
          :key="index"
          :inset="item.inset"
        ></v-divider>

        <v-list-item
          v-else
          :key="item.title"
          @click=""
        >
          <v-list-item-avatar>
            <v-img :src="item.avatar"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.title"></v-list-item-title>
            <v-list-item-subtitle v-html="item.subtitle"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </template>
    </v-list>
</template>
<script>
  export default {
      props:["post"],
      created() {
          var self = this;
            this.axios.get(self.url+'comments?postId='+self.post.id).then((response) => {
                if( response.data.Data.length > 0){
                    response.data.Data.forEach(el=>{
                        var item = {
                            avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
                            title: el.name + el.email,
                            subtitle: `<span class='text--primary'>`+el.body+'</span>'
                        }
                        self.items.push(item)
                        self.items.push({ divider: true, inset: true })
                    })
                
                }
            })
      },
    data: () => ({
    url:"http://localhost:4200/",
      items: [
        { header: 'Comentários' },
      ],
    }),
  }
</script>