 <template>
    <v-app>
      <v-content>
        <v-container>
        <v-card flat tile> </v-card>
            <v-toolbar color="deep-purple darken-1 white--text">
              <v-toolbar-side-icon dark></v-toolbar-side-icon>
              <v-toolbar-title>Meow or Not!</v-toolbar-title>
              <v-spacer></v-spacer>
              <v-toolbar-items class="hidden-sm-and-down">
                <v-btn dark flat value="true">Kitty tour</v-btn>
                <v-btn dark flat>Ranking</v-btn>
                <v-btn dark flat>Upload</v-btn>
                <v-btn dark color="white--text" flat>Sign Up</v-btn>
              </v-toolbar-items>    
              </v-toolbar>
            <v-layout align-center justify-center class="color-purple">
                <v-btn color="pink lighten-4 grey--text text--darken-4
                " large @click="loadNextImage" class="mt-3">
                    Another Kitty &nbsp;  <v-icon>refresh</v-icon>
                </v-btn>
            </v-layout>

            <v-layout row wrap>
                <v-flex xs12 >
                <v-card flat tile class="d-flex" style="background-color:#474747">
                    <v-img height="650px" :src="image.url" tile="true">
                    </v-img>
                </v-card>
                </v-flex>
            </v-layout>

        </v-container>
      </v-content>
    </v-app>
  </template>

  <script>
    import Vue from 'vue';
    import Vuetify from 'vuetify'
    import axios from 'axios'

    Vue.use(axios);
    Vue.use(Vuetify);
   export default { 
        data: () =>({
            image: { url: ""}
        }),
        created(){
            this.loadNextImage();
        } ,
        methods:{
            async loadNextImage()
            {
                try{
                    axios.defaults.headers.common['x-api-key'] = "DEMO-API-KEY" // Replace this with your API Key

                    let response = await axios.get('https://api.thecatapi.com/v1/images/search', { params: { limit:1, size:"full" } } ) // Ask for 1 Image, at full resolution
                    
                    this.image = response.data[0] // the response is an Array, so just use the first item as the Image

                    console.log("-- Image from TheCatAPI.com")
                    console.log("id:", this.image.id)
                    console.log("url:", this.image.url)

                }catch(err){
                    console.log(err)
                }
            }
        }
    }
    
  </script>
<style scoped>
    body{
        background-color:grey;
        }
    .container{
        min-width: 100%;
        min-height: 100%;
        background-size:cover;
        background-color:#333;
    }
    .v-content_wrap{
        background:#357;
    }
    .v-responsive__content{
        border-top:15px solid #0a0e2c;;
        border-bottom:15px solid #0a0e2c;;
        border-left:15px solid #5E35B1;
        border-right:15px solid #5E35B1;
        border-bottom-right-radius:20px;
        border-bottom-left-radius:20px;
    }
    .rounded-card{
       height:50%;
    }
    .color-purple{
        background-color:#0a0e2c;
    }
    .v-image__image{
        border-radius:50px;
    }
</style>
