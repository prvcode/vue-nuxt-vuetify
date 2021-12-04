<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card elevation="4" tile shaped>
        <v-card-title>Create blockchain</v-card-title>
      <v-tabs v-model="tab" grow>
        <v-tab key='k1' href='#k1'>JSON File Upload</v-tab>
        <v-tab key='k2' href='#k2'>Array of Objects</v-tab>
      </v-tabs>
  
      <v-tabs-items v-model="tab">
        <v-tab-item key='k1' value='k1'>
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

        <v-tab-item key='k2' value='k2'>
          <v-card-text>
              <v-row align="center" class="mx-0 mt-5">
                <v-textarea
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
  </v-row>
</template>

<script>

export default {
  data () {
    return {
      tab: 'jsonObject',
      hide: false ,
      fileContent:''
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
      this.$store.dispatch('blockchain/create', this.fileContent).then(()=>{
        this.routeToSelectHop()
      })
    },

    clearBlockchain() {      
      this.$store.dispatch('blockchain/remove')
    },
    
    routeToSelectHop() {
      this.$store.dispatch('blockchain/removeTraverse')
      this.$router.push('/traverse')
    }
  }
}
</script>
