<template>
<div id="testTable" class="tableContainer" v-bind:class="{ 'scrollable': scrollable }">
  <div class="resizeContainer"></div>
  <table>
    <thead>
      <tr>
        <th v-for="header in headers" v-bind:key="header.reference">
          {{header.title}}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(line, index) in lines" v-bind:key="index">
        <td v-for="header in headers" v-bind:key="header.reference + '_' + index"
            v-bind:title="line[header.reference]">
          {{ line[header.reference] }}
        </td>
      </tr>
    </tbody>
  </table>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    scrollable: Boolean
  },
  data: function(){
    return {
      headers:[
        { title: "Header 1", reference: "PropOne" },
        { title: "Header 2", reference: "PropTwo" },
        { title: "Very very very very very very very very very very very long header", reference: "PropThree" },
        { title: "Header 4", reference: "PropFour" },
        { title: "Header 5", reference: "PropFive" },
        { title: "SmH", reference: "PropSix" },
        { title: "Header 7", reference: "PropSeven" },
      ],
      lines:[
        { PropOne: "test1", PropTwo: "Longer property test", PropThree: "test3", PropFour: "test4", PropFive: "test5", PropSix: "test6", PropSeven: "test7" },
        { PropOne: "test1", PropTwo: "test2", PropThree: "test3", PropFour: "test4", PropFive: "test5", PropSix: "test6", PropSeven: "test7" },
        { PropOne: "test1", PropTwo: "test2", PropThree: "test3", PropFour: "test4", PropFive: "Another longer property test", PropSix: "This is longer than the others", PropSeven: "test7" },
        { PropOne: "Very very very very long property", PropTwo: "test2", PropThree: "test3", PropFour: "test4", PropFive: "test5", PropSix: "test6", PropSeven: "test7" },
      ]
    }
  },
  mounted:function(){
    let testTable = document.getElementById("testTable");
    let resizeContainer = testTable.getElementsByClassName("resizeContainer")[0];
    let headers = testTable.getElementsByTagName("th");

    let tableGenerated = headers.length === this.headers.length;

    let handles = [];

    if(tableGenerated){
      let offsetX = 0;//testTable.getBoundingClientRect().x;
      for(let i = 0; i < headers.length; i++){
        let header = headers[i];
        
        let handle = document.createElement("div");
        
        resizeContainer.appendChild(handle);

        handle.className = "resize-handle";
        handle.style.position = "absolute";
        handle.style.top = "0px";
        handle.style.left = offsetX + header.width + 'px';

        handles.push(handle);

        offsetX += header.width;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tableContainer{
  flex: 0 0 auto;
  max-width: 50%;
  position: relative;
}

.resizeContainer{
  width:100%;
  height:30px;
  position: absolute;
  top:0;
  left:0;
}

table{
  width:100%;
  table-layout: fixed;
  border-collapse: collapse;
}

.tableContainer.scrollable{
    flex: 1 1 auto;
    overflow: auto;
}

.tableContainer.scrollable table{
  width:auto;
}

table tr{
  height: 30px;;
  line-height: 30px;
}

table thead tr{
  background-color: dodgerblue;
}

table tbody tr:nth-child(odd){
  background-color: #eee;
}

table tbody tr:hover{
  cursor:pointer;
  background-color:aquamarine;
}

table td, table th{
  border:1px solid white;
  padding:3px 5px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

</style>
