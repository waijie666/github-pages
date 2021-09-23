<template>
  <div v-if="pageloadcomplete">
    <div class="instructions">
    <img :src=imageProp style="max-width: 100%">
    <b><h1>Welcome to the {{sorterNameProp}} Sorter!</h1></b>Pick which character you prefer in each battle to get an accurate list of your favourites.<br />Have fun, choose wisely and take your time!<br /><br />Note: Hitting 'skip' or 'I like both' frequently will negatively affect your results.
    <div id="battleNumber"><b>Battle #{{numQuestion}}<br>{{battlePercent}}% sorted.</b></div>
    </div>
    <table id="mainTable" align="center">
    <tbody>
    <tr>
      <td id="leftField" @click="if(!finishFlag) sortList(-1);" rowspan="2" style="text-align:center;">
        <div style="display: grid" v-if="namMember[leftindex]">
        <div><img style="width:100px" v-bind:src="namMember[leftindex].image" /></div>
        <div>{{ namMember[leftindex].name }}</div>
        </div>       
      </td>
      <td class="middleField" @click="if(!finishFlag) sortList(0);" style="text-align:center;">
        I Like Both
      </td>
      <td id="rightField" @click="if(!finishFlag) sortList(1);" rowspan="2" style="text-align:center;">
        <div style="display: grid" v-if="namMember[rightindex]">
        <div><img style="width:100px" v-bind:src="namMember[rightindex].image"  /></div>
        <div>{{ namMember[rightindex].name }}</div>
        </div>
      </td>
      </tr>
      <tr>
      <td class="middleField" @click="if(!finishFlag) sortList(0);" style="text-align:center;">
        Skip
      </td>
    </tr>
    </tbody></table>
    <template v-for="(value, name) in AllDictionaryObject" :key="value">
      <input type="checkbox" v-model="AllDictionaryObject[name].checked">
        {{ name }}
    </template>
    <p />
    <div>
      <button @click="initList">Filter</button>
      <button @click="loadResult">Load Previous Results</button>
      Limit maximum number of characters: <input v-model="maxSize" size="5"/>
    </div>
    <br />
    <div id="resultField" style="text-align: center;" v-if="finishFlag">
      <table style="border-radius:10px; padding:10px 15px 10px 0px; box-shadow: 1px 1px 4px #d96991, -1px -1px 4px #d96991; width:90%; max-width:550px; font-size:18px; background-color:#fff; line-height:130%; margin-left:auto; margin-right:auto; border-collapse: separate; border: 0px solid #4A86C1;" align="center" ><tr><td>
        <table id="resulttable" style="border-radius:10px; width:100%; padding:5px 5px 5px 5px; border-collapse: separate;">
        <tr style="background-color:#fff"><td colspan="2" style="vertical-align:middle; background-color:#fff;padding-bottom:10px;font-size:140%;height:50px;">My {{sorterNameProp}} Ranking</td></tr>
        <tr style="height:40px; background-color:#fff"><td style="background-color:#fff; text-align:center;">Rank</td><td style="background-color:#fff; text-align:center;">Idol</td></tr>
        <template v-for="member in resultMember" :key="member">
          <tr style="background-color:#fff; box-sizing:border-box; margin-right:5px"><td style="color: #4A86C1; text-align:center; background-color:#fff">{{member.ranking}}</td><td class="idolname" style="border:1px solid #ccc; color: #4A86C1; padding:5px; background-color:#fff"><div style="display: grid; grid-template-rows: auto; grid-template-columns: 3fr 1fr;"><div style="margin: auto;">{{member.name}}</div><div><img style="width:100px" v-bind:src="member.image" /></div></div></td></tr>
        </template>
        <tr><td colspan=2>Results on {{new Date(resultDate).toLocaleString()}} </td></tr>
        </table></td></tr><tr><td><button type="button" class="btn btn-primary" @click="generateImage" style="margin: auto">Save Results as Image</button></td></tr></table>
    </div>  
  </div>
</template>

<style scoped>
#mainTable{
font-size: 19px;
text-align: center;
vertical-align: middle;
width: 90%;
max-width: 800px;
margin-left: auto;
margin-right: auto;
border-collapse: separate;
border-spacing: 10px 15px;
}
#leftField:hover,#rightField:hover,.middleField:hover{
color: #4A86C1;
}
#leftField img{
margin-right:10px;
vertical-align: middle;
}
#rightField img{
margin-left:10px;
vertical-align: middle;
}
td{
border-radius:13px;
text-shadow: none;
}
#leftField{
width: 40%;
height: auto;
cursor: pointer;
border: 0px solid #e46f6b;
background: rgba(255,255,255,0.8);
box-shadow: 1px 1px 5px #d96991, -1px -1px 5px #d96991;
text-shadow: none;
vertical-align: middle;
-webkit-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
}
#rightField{
width: 40%;
height: auto;
cursor: pointer;
border: 0px solid #e46f6b;
background: rgba(255,255,255,0.8);
box-shadow: 1px 1px 5px #d96991, -1px -1px 5px #d96991;
text-shadow: none;
-webkit-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
}
.middleField{
width: 120px;
height: 80px;
cursor: pointer;
border: 0px solid #e46f6b;
background: rgba(255,255,255,0.8);
box-shadow: 1px 1px 5px #d96991, -1px -1px 5px #d96991;
text-shadow: none;
-webkit-user-select: none;
-moz-user-select: none;
-ms-user-select: none;
user-select: none;
}
#resultField img{
vertical-align: middle;
}
#resultField > table tr:nth-child(n+3) > td > img {
position: absolute;
right: 5px;
top: 5px;
}
#resultField > table tr:nth-child(n+3)  > td {
position: relative;
overflow: hidden;
height: 80px;
margin: 10px;
}
.idolname img{
text-align: right;
max-height: 70px;
max-width: 70px;
}
#battleNumber{
margin: 45px 0px -25px 0px;
font-size:140%;
text-shadow: #4A86C1 1px 1px 3px, #4A86C1 -1px -1px 3px, #4A86C1 -1px 1px 3px, #4A86C1 1px -1px 3px,
#4A86C1 3px 3px 7px, #4A86C1 -3px -3px 5px, #4A86C1 -3px 3px 5px, #4A86C1 3px -3px 7px;
}
a{
color: #5b17ba;
text-decoration : none;
}
a:hover{
color: #945ce3;
}

html{
  touch-action: manipulation;
  background: url("https://i.imgur.com/f6kOhXb.jpg") no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  
}
body {
background-color: transparent;
/*width: 940px;*/
margin: 0 auto;
font-family: 'Source Sans Pro', sans-serif;
font-weight: bold;
color: #E75099;
text-shadow: #d96991 1px 1px 3px, #d96991 -1px -1px 3px, #d96991 -1px 1px 3px, #d96991 1px -1px 3px,
#d96991 3px 3px 7px, #d96991 -3px -3px 5px, #d96991 -3px 3px 5px, #d96991 3px -3px 7px;
}
.instructions,.filter {
 color: #fff;
 margin:15px;
 padding:15px;
 text-align: center;
 text-shadow: #4A86C1 1px 1px 3px, #4A86C1 -1px -1px 3px, #4A86C1 -1px 1px 3px, #4A86C1 1px -1px 3px,
#4A86C1 3px 3px 7px, #4A86C1 -3px -3px 5px, #4A86C1 -3px 3px 5px, #4A86C1 3px -3px 7px;
}  
</style>

<script>
// @ is an alias to /src

import html2canvas from 'html2canvas'

export default {
  name: 'Sorter',
  components: {
  },
  props: {
    sorterNameProp: {
      type: String,
      default: "Placeholder"
    },
    dictionaryObjectProp: {
      type: Object,
      default() {
        return {
          "Food": {
            array: [
              {name: "Rice", image: ""},
              {name: "Noodle", image: ""},
              {name: "Bread", image: ""}
            ]
          }
        }
      }
    },
    imageProp: String
  },
  data()  {
    return  {
      namMember: new Array(),
      lstMember: new Array(),
      resultMember: new Array(),
      parent: new Array(),
      equal: new Array(),
      rec: new Array(),
      cmp1: 0,
      cmp2: 0,
      head1: 0,
      nrec: 0,
      numQuestion: 1,
      totalSize: 0,
      finishSize: 0,
      finishFlag: false,
      pageloadcomplete: false,
      leftindex: 0,
      rightindex: 0,
      resultDate: 0,
      maxSize :"",
      AllDictionaryObject: this.dictionaryObjectProp
    }
  },
  mounted() {
    for (var key in this.AllDictionaryObject) {
      this.AllDictionaryObject[key]["checked"] = true
    }
    this.initList()
  },
  methods:{
    initList()
    {
      //Return if nothing is checked
      var checked = 0
      var key
      for (key in this.AllDictionaryObject){
        if (this.AllDictionaryObject[key].checked)
        {
          checked ++
        }
      }
      if (checked == 0)
      {
        return
      }

      this.pageloadcomplete = false
      function shuffleArray(array) {
        for (var i = array.length - 1; i > 0; i--) {
            var j = Math.floor(Math.random() * (i + 1));
            var temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
      }

      this.namMember = new Array()
      this.lstMember = new Array()
      this.parent = new Array()
      this.equal = new Array()
      this.rec = new Array()
      for (key in this.AllDictionaryObject){
        if (this.AllDictionaryObject[key].checked)
        {
          this.namMember = this.namMember.concat(this.AllDictionaryObject[key].array)
        }
      }
      shuffleArray(this.namMember)

      var arraySize = parseInt(this.maxSize)
      if (arraySize && arraySize < this.namMember.length)
      {
        this.namMember = this.namMember.slice(0, arraySize)
      }
      var n = 0;
      var mid;
      var i;
      //The sequence that you should sort
      this.lstMember[n] = new Array();
      for (i=0; i<this.namMember.length; i++) {
        this.lstMember[n][i] = i;
      }
      this.parent[n] = -1;
      this.totalSize = 0;
      n++;
      for (i=0; i<this.namMember.length; i++) {
        //And element divides it in two/more than two
        //Increase divided sequence of last in first member
        if(this.lstMember[i].length>=2) {
          mid = Math.ceil(this.lstMember[i].length/2);
          this.lstMember[n] = new Array();
          this.lstMember[n] = this.lstMember[i].slice(0,mid);
          this.totalSize += this.lstMember[n].length;
          this.parent[n] = i;
          n++;
          this.lstMember[n] = new Array();
          this.lstMember[n] = this.lstMember[i].slice(mid,this.lstMember[i].length);
          this.totalSize += this.lstMember[n].length;
          this.parent[n] = i;
          n++;
        }
      }
      //Preserve this sequence
      for (i=0; i<this.namMember.length; i++) {
        this.rec[i] = 0;
      }
      this.nrec = 0
      //List that keeps your results
      //Value of link initial
      // Value of link initial
      for (i=0; i<=this.namMember.length; i++) {
        this.equal[i] = -1;
      }
      this.cmp1 = this.lstMember.length-2;
      this.cmp2 = this.lstMember.length-1;
      this.head1 = 0;
      this.head2 = 0;
      this.numQuestion = 1;
      this.finishSize = 0;
      this.finishFlag = false;
      this.leftindex = this.lstMember[this.cmp1][this.head1]
      this.rightindex = this.lstMember[this.cmp2][this.head2]
      this.pageloadcomplete = true
      //console.log(this.lstMember)      
    },
    sortList(flag){
      this.pageloadcomplete = false
      var i;
      //rec preservation
      if (flag<0) {
      this.rec[this.nrec] = this.lstMember[this.cmp1][this.head1];
      this.head1++;
      this.nrec++;
      this.finishSize++;
      while (this.equal[this.rec[this.nrec-1]]!=-1) {
      this.rec[this.nrec] = this.lstMember[this.cmp1][this.head1];
      this.head1++;
      this.nrec++;
      this.finishSize++;
      }
      }
      else if (flag>0) {
      this.rec[this.nrec] = this.lstMember[this.cmp2][this.head2];
      this.head2++;
      this.nrec++;
      this.finishSize++;
      while (this.equal[this.rec[this.nrec-1]]!=-1) {
      this.rec[this.nrec] = this.lstMember[this.cmp2][this.head2];
      this.head2++;
      this.nrec++;
      this.finishSize++;
      }
      }
      else {
      this.rec[this.nrec] = this.lstMember[this.cmp1][this.head1];
      this.head1++;
      this.nrec++;
      this.finishSize++;
      while (this.equal[this.rec[this.nrec-1]]!=-1) {
      this.rec[this.nrec] = this.lstMember[this.cmp1][this.head1];
      this.head1++;
      this.nrec++;
      this.finishSize++;
      }
      this.equal[this.rec[this.nrec-1]] = this.lstMember[this.cmp2][this.head2];
      this.rec[this.nrec] = this.lstMember[this.cmp2][this.head2];
      this.head2++;
      this.nrec++;
      this.finishSize++;
      while (this.equal[this.rec[this.nrec-1]]!=-1) {
      this.rec[this.nrec] = this.lstMember[this.cmp2][this.head2];
      this.head2++;
      this.nrec++;
      this.finishSize++;
      }
      }
      //Processing after finishing with one list
      if (this.head1<this.lstMember[this.cmp1].length && this.head2==this.lstMember[this.cmp2].length) {
      //List the remainder of this.cmp2 copies, list this.cmp1 copies when finished scanning
      while (this.head1<this.lstMember[this.cmp1].length){
      this.rec[this.nrec] = this.lstMember[this.cmp1][this.head1];
      this.head1++;
      this.nrec++;
      this.finishSize++;
      }
      }
      else if (this.head1==this.lstMember[this.cmp1].length && this.head2<this.lstMember[this.cmp2].length) {
      //List the remainder of this.cmp1 copies, list this.cmp2 copies when finished scanning
      while (this.head2<this.lstMember[this.cmp2].length){
      this.rec[this.nrec] = this.lstMember[this.cmp2][this.head2];
      this.head2++;
      this.nrec++;
      this.finishSize++;
      }
      }
      //When it arrives at the end of both lists
      //Update a pro list
      if (this.head1==this.lstMember[this.cmp1].length && this.head2==this.lstMember[this.cmp2].length) {
      for (i=0; i<this.lstMember[this.cmp1].length+this.lstMember[this.cmp2].length; i++) {
      this.lstMember[this.parent[this.cmp1]][i] = this.rec[i];
      }
      this.lstMember.pop();
      this.lstMember.pop();
      this.cmp1 = this.cmp1-2;
      this.cmp2 = this.cmp2-2;
      this.head1 = 0;
      this.head2 = 0;
      //Initialize the rec before performing the new comparison
      if (this.head1==0 && this.head2==0) {
      for (i=0; i<this.namMember.length; i++) {
      this.rec[i] = 0;
      }
      this.nrec = 0;
      }
      }
      if (this.cmp1<0) {
        //showResult();        
        var ranking = 1;
        var sameRank = 1;
        this.resultMember = new Array()
        for (i=0; i<this.namMember.length; i++) {
          var memberObject = this.namMember[this.lstMember[0][i]]
          memberObject.ranking = ranking
          this.resultMember.push(memberObject)
          if (i<this.namMember.length-1){
            if (this.equal[this.lstMember[0][i]]==this.lstMember[0][i+1]) {         
              sameRank++;
            }
            else {
              ranking += sameRank;
              sameRank = 1;
            }
          }
        }
        this.finishFlag = true;
        this.resultDate = new Date().getTime()
        localStorage.setItem("Results "+this.sorterNameProp, JSON.stringify({"resultArray": this.resultMember, "resultDate": this.resultDate }))
        //console.log(this.resultMember)
      }
      else {
        this.numQuestion += 1
        this.leftindex = this.lstMember[this.cmp1][this.head1]
        this.rightindex = this.lstMember[this.cmp2][this.head2]
      //showImage();
      }
      this.pageloadcomplete = true
    },
    loadResult(){
      this.resultMember = JSON.parse(localStorage.getItem("Results "+this.sorterNameProp))["resultArray"]
      this.resultDate = JSON.parse(localStorage.getItem("Results "+this.sorterNameProp))["resultDate"]
      this.finishFlag = true;
    },
    generateImage(){
      function download(url, filename){
        var link = document.createElement('a');
        link.download = filename;
        link.href = url;
        link.click();
      }
      var element = document.getElementById("resulttable")
      html2canvas(element, {allowTaint: true, useCORS: true, scrollY: -window.scrollY}).then((canvas) => {
        //document.body.appendChild(canvas);
        download(canvas.toDataURL(), this.sorterNameProp +' sorter.png');
      })
    }
      
  },
  computed:{
    battlePercent() {
      return Math.floor(this.finishSize*100/this.totalSize)
    }
  }
}
</script>
