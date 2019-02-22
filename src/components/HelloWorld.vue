<template>
  <div class="hello">
    <div id="div1" @drop="drop" @dragover="allowDrop">
      <img v-for="item in srcImg" :key="item" :src="item" style="width:10%;height:auto"/>
    </div>
    <img id="img" :src="imgData" draggable="true" @dragstart="drag" style="width:20%;height:auto"/>
  </div>
  <!-- <div class='drag-content' id="dragCon" >
    <div class='project-content'>
      <div class='select-item' draggable='true' @dragstart='drag($event)' v-for="pjdt in projectdatas">{{pjdt.name}}</div>
    </div>
    <div class='people-content'>
      <div class='drag-div' v-for="ppdt in peopledata" @drop='drop($event)' @dragover='allowDrop($event)'>
        <div class='select-project-item'>
          <label class='drag-people-label'>{{ppdt.name}}:</label>
        </div>
      </div>
    </div>
  </div> -->
</template>

<script>
import draggable from 'vuedraggable'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      srcImg: [],
      imgData: 'http://www.pptbz.com/pptpic/UploadFiles_6909/201203/2012031220134655.jpg',
    }
  },
  components: {
    draggable
  },
  methods: {
    drag(event) {
      console.log("event is ",event);
      event.dataTransfer.setData("Text",event.target.currentSrc);
    },
    drop(event) {
      event.preventDefault();
      let data = event.dataTransfer.getData("Text");
      console.log("data is ",data);
      this.srcImg.push(data);
      console.log("srcImg is ",this.srcImg);
    },
    allowDrop(event) {
      event.preventDefault();
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#div1{
  border: 1px solid #ec0023;
  width: 100%;
  height:200px;

}
.select-item {
  background-color: #5bc0de;
  display: inline-block;
  text-align: center;
  border-radius: 3px;
  margin-right: 10px;
  cursor:pointer;
  padding: 6px 20px;
  color: #fff;
}
 .cursored{
  cursor: default;
}
.project-content,.people-content {
    margin: 30px 50px;
}
.people-content {
    margin-top: 30px;
}
.drag-div {
    border: 1px solid #5bc0de;
    padding:10px;
    margin-bottom: 10px;
    width: 800px;
    cursor: pointer;
}
.select-project-item {
    display: inline-block;
    text-align: center;
    border-radius: 3px;
}
.drag-people-label{
  margin-bottom:0;
  padding-right:10px;
}
[v-cloak]{
    display:none;
}
</style>
