<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card elevation="4" tile shaped>
        <v-card-title>Create blockchain</v-card-title>
      <v-tabs v-model="tab" grow>
        <v-tab key='jsonFile' href='#jsonFile'>JSON File Upload</v-tab>
        <v-tab key='arrayObject' href='#arrayObject'>Array of Objects</v-tab>
      </v-tabs>
  
      <v-tabs-items v-model="tab">
        <v-tab-item key='jsonFile' value='jsonFile'>
          <v-card-text>
              <v-row align="center" class="mx-0 mt-5">
                <v-file-input
                  small-chips
                  accept="application/json"
                  label="Upload JSON File"
                  @change="onFileChange"
                ></v-file-input>
            </v-row>
            </v-card-text>
        </v-tab-item>

        <v-tab-item key='arrayObject' value='arrayObject'>
          <v-card-text>
              <v-row align="center" class="mx-0 mt-5">
                <v-textarea
                  v-model="textarea"
                  name="input-7-1"
                  label="Array of Objects"
                ></v-textarea>
              </v-row>
            </v-card-text>
        </v-tab-item>
      </v-tabs-items>
       <v-card-actions class="pa-5">
          <v-btn @click="createBlockchain()">Create Blockchain</v-btn>
          <v-btn @click="clearBlockchain()" color="red" class="justify-right">Remove Blockchain</v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
    <v-snackbar v-model="snackbar" :timeout="timeout">
      {{ text }}
      <template v-slot:action="{ attrs }">
        <v-btn color="blue" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>    
  </v-row>
</template>

<script>

export default {
  data () {
    return {
      tab: 'jsonFile',
      hide: false ,
      fileContent:'',
      snackbar: false,
      text: '',
      timeout: 4000,
      textarea: null
    }
  },
   methods: {
    async onFileChange(file) {
      let read = new FileReader();
      read.readAsBinaryString(file);
      read.onloadend = (()=>{ 
          this.fileContent = read.result;
      })      
    },

    createBlockchain() {   
      if(this.tab === 'jsonFile') {
        this.$store.dispatch('blockchain/create', this.fileContent).then(()=>{
          this.routeToSelectHop()
        })
      } else {
        if(this.isJsonString(this.textarea)) {
          this.$store.dispatch('blockchain/create', this.textarea).then(()=>{
            this.routeToSelectHop()
          }).catch(err=> {
            this.snackbar = true
            this.text = 'Invalid JSON, Check Provided data is an array and has all the data elements'
          })
        } else {
          this.snackbar = true
          this.text = "Invalid JSON Format"
        }
      }
    },

    clearBlockchain() {      
      this.$store.dispatch('blockchain/remove')
      this.snackbar = true
      this.text = "Blockchain is cleared"
    },
    
    routeToSelectHop() {
      this.$store.dispatch('blockchain/removeTraverse')
      this.$router.push('/traverse')
    },
    isJsonString(str) {
      try {
          JSON.parse(str);
      } catch (e) {
          return false;
      }
      return true;
    }
  }
}
</script>
