<template>
  <div class="body">
    <div class="json">
        <textarea name="json" v-model="jsonTextArea"></textarea>
    </div>
    <div class="cvs">
      <textarea name="cvs" v-model="cvsTextArea"></textarea>
    </div>
  </div>
      <div class="btn">
        <button @click="converter(jsonTextArea, cvsTextArea)">Convert</button>
      </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

let jsonTextArea = ref<string>('')
let cvsTextArea = ref<string>('')
let imports = ref<string>('')

function importing(){
  jsonTextArea.value =  imports.value
}

function converter(json: string, cvs: string){
  let resultArray: string[][] = [];
  let jsonLines: string[] = json.split("\n");
  let jsonHeaders: string = jsonLines.shift() || "";
  let headers: string[] = jsonHeaders.split(",");

  console.log(headers, jsonLines);
  
  for (let i = 0; i < jsonLines.length; i++) {
    if(jsonLines[i] != ''){
      let jsonStrings = jsonLines[i].split(",")
      let mainItem: string[] = []
      for (let e = 0; e < jsonStrings.length; e++) {
        let index = jsonStrings.indexOf(jsonStrings[e])
        mainItem.push(headers[index], jsonStrings[index])

        console.log(mainItem);
        
      }
      resultArray.push(mainItem)
    }
  }

  for (let i = 0; i < resultArray.length; i++) {

    
  }

  cvsTextArea.value = JSON.stringify(resultArray, null, 2).replace(/},/g, "},\r\n");
  

}
</script>