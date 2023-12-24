<template>
  <div class="body">
    <div class="cvs">
      <textarea name="cvs" v-model="cvsTextArea" placeholder="Cvs"></textarea>
    </div>
    <div class="json">
        <textarea name="json" v-model="jsonTextArea" placeholder="Json"></textarea>
    </div>
  </div>
      <div class="btn">
        <button @click="converter(jsonTextArea, cvsTextArea)">Convert</button>
        <button @click="clearField()">Clear</button>

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
  if(cvsTextArea.value == ''){
    alert("cvs is empty")
  }else{
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

  if(resultArray.length < 1){
    alert("Cvs not in right format")
    clearField()
  }else{
    jsonTextArea.value = JSON.stringify(resultArray, null, 2).replace(/},/g, "},\r\n");
  }

}
}
function clearField(){
  jsonTextArea.value = ""
  cvsTextArea.value = ""
}


</script>