<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card elevation="4" tile shaped>
        <v-card-title>Create blockchain</v-card-title>
        <v-card-text>
           <v-row align="center" class="mx-0">
             <v-file-input
              accept="json/*"
              label="Upload JSON File"
            ></v-file-input>
           </v-row>
           <v-row align="center" class="mx-0">
            <v-textarea
              name="input-7-1"
              label="Add JSON Object"
            ></v-textarea>
           </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
