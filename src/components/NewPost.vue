<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500">
      <template v-slot:activator="{ on }">
        <v-btn color="primary" v-on="on">Criar novo post</v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>Criar novo post</v-card-title>

        <v-form ref="form" v-model="valid" lazy-validation style="margin: 20px">
          <v-text-field v-model="title"  label="Titulo" required></v-text-field>

          <v-textarea v-model="body" label="Corpo" required></v-textarea>

          <v-btn :disabled="!valid" color="success" class="mr-4" @click="sendPost">Salvar</v-btn>

        </v-form>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
         
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data: () => ({
    url:"http://localhost:4200/",
    dialog: false,
    title: '',
    body: '',
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+\..+/.test(v) || "E-mail must be valid"
    ],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false
  }),
    created() {
        var self = this;
    },
  methods: {
    sendPost(){
      var self = this;
      this.axios.post(self.url+'posts', {userId: 1, title: self.title, body: self.body}).then((response) => {
        if(!response.data.Error){
          alert(response.data.Message);
          self.dialog = false;
          self.$emit('refresh');
        }
        else 
          alert("Problemas com o servidor.")
      })
    },
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true;
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>