<template>
  <div id="app">
   
   <div id="adiv"  >
    <div id="he" v-if="lowWidth">
    <div style="margin-top: 200px">
    <h1>its not responsive for low width screens (like mobile) </h1> 
    <el-button type="info" @click="removeS">ok</el-button>
    </div>
    </div>
    </div> 
    <div id="left"  @click='addE(2) ;moveXY("left")' class="tri y ">
    </div> 
       <div  id="right"  @click='addE(4); moveXY("right")' class="tri y ">
    </div> 
  
      <div  id="up"  @click=' addE(1) ; moveXY("up")' class="tri x ">
    </div>
    <div  id="down"   @click='addE(3); moveXY("down")' class="tri x">
    </div>
   
     <div v-bind:class='{upba: directions.up,leftba:directions.left,downba:directions.down,rightba:directions.right,centerba:directions.center}'  class="bouncingBall"></div>
  <div>
    <el-row id="row1" type="flex" class="row-bg" justify="end" > 
    <div id="form">
    
    <h2>Simon Game</h2>
     <el-button type="warning"  @click="startFunc(); allC()">start</el-button>
     <el-button type="danger" @click="stop">stop</el-button>
     <div id="score">score : {{score}}</div>
     <p>Developed by Nader Atef</p>
      
     </div>
      </el-row>  
   
  </div>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  },
  data:function(){
    return {
      directions:{
     down:false,
     up:false,
     left:false,
     right:false,
     center:false,
      },
      ranInt: undefined,
      lowWidth: false,
      circleObjects: [
        {
          name:1,
          direction:'up',
          soundPath:'https://s3.amazonaws.com/freecodecamp/simonSound1.mp3'
        },{
          name:2,
          direction:'left',
          soundPath:'https://s3.amazonaws.com/freecodecamp/simonSound2.mp3'
        },{
          name:3,
          direction:'down',
          soundPath:'https://s3.amazonaws.com/freecodecamp/simonSound3.mp3'
        },{
          name:4,
          direction:'right',
          soundPath:'https://s3.amazonaws.com/freecodecamp/simonSound4.mp3'
        }
      ],
      scoreArray:[],
      counter:0,
      counterT:1,
      userArray:[],
      ident: undefined,
      equaler: undefined,
      eqTry: undefined,
      score: 0,
    }
  },
    methods:{
      stop:function(){
        var self = this
        self.ident=false
        self.scoreArray=[]
        self.userArray=[]
      },
      allC:function(){
       for(var key in circleObjects){
         let el = document.getElementById(self.circleObjects[key].direction)
         el.classList.remove('lighter')
       }
      },
      removeS:function(){
        let self = this 
         self.el =  document.getElementById('adiv')
       // console.log(self.el.style)
        self.el.style.height= 0
        self.el.style.width= 0
        self.el.style.zIndex = -4
        self.el =  document.getElementById('he')
        console.log(self.el.style)
        self.el.style.height= 0
        self.el.style.width= 0
        self.el.style.zIndex = -4
        self.lowWidth = false

      },
      moveXY:function(direct){
        var self = this  
       
       
        for( var key in self.directions){
        self.directions[key] = false         
        }
        self.directions[direct] = true
         if(direct== "center"){
          self.directions.center = true
        }
        if(direct !== 'center'){
          for(var key in self.circleObjects){
            if(self.circleObjects[key].direction == direct){
              self.aud = new Audio(self.circleObjects[key].soundPath)
              self.aud.play()
             // self.onaud = setInterval
            }
          }
 let ele =  document.getElementById(direct)
  //      console.log(ele.classList)
        self.onhit = setInterval(function(){
         ele.classList.add('lighter')
          window.clearInterval(self.onhit)
         },250)
        // self.onsh = setInterval(function(){
         ele.classList.remove('lighter')
          //window.clearInterval(self.onsh)
      //   },250) 
          //self.onit = setInterval(function(){
     //    ele.classList.remove('lighter')
          //window.clearInterval(self.onit)
         //},550) 
            }
           
       
         
     
      },
      addE:function(num){
       let self = this 
       if(self.ident){
       self.userArray.push(num)
       self.thArr = []
             self.anArr = []
       for(var key in self.scoreArray){
         self.anArr.push(self.scoreArray[key])
       }
       self.ar = []
       for(var je  in self.userArray){
         self.ar.push(self.userArray[je])
       }
       for(var ke in self.ar){
         for(var key in self.anArr){         
           if(self.ar[ke] === self.anArr[key] ){
             if(ke === key){
//console.log(self.ar.indexOf(self.ar[self.ar.length-1]),self.anArr.indexOf(self.anArr[self.anArr.length-1]),self.anArr[key],self.ar[ke])       
             //  console.log('how?')
             self.thArr.push(self.ar[ke])
             }
           }
         }
       }
    
 
    //   console.log("anArr is " , self.anArr)     
   if(self.ar.length == self.thArr.length && self.thArr.length !== self.scoreArray.length){
         self.equaler= true
         self.eqTry=  false
       }else  if(self.thArr.length == self.anArr.length){
       self.eqTry = true
       self.equaler = false
       }
       else{
         self.equaler = false
         self.eqTry = false
       }
       
     //  console.log(self.equaler,self.eqTry)
    //  console.log(self.scoreArray,self.thArr) 
   //  console.log('anArr',self.anArr,' thArr',self.thArr )
     // self.onshot = setInterval(function(){
      self.moveXY(self.circleObjects[num-1].direction)
       window,clearInterval(self.onshot)
   //   },100)
   
       if(self.eqTry){
          ///console.log("it got to here")
          self.userArray = []
          self.score++
           self.scoreArray.push(self.randNo(1,4))
         self.onhot = setInterval(function(){
      self.startFunc()
       window,clearInterval(self.onhot)
      },1000)
        }else if(self.equaler){
         //console.log('equaler is true')
        }else{
        //  console.log(self.userArray, self.anArr,self.thArr,'hi')    
             self.buz = new Audio('http://soundbible.com/grab.php?id=1501&type=mp3')
             self.buz.play()
             self.score = 0
          self.scoreArray = []
          self.userArray=[]
          self.startFunc()
          self.removeLight()
        }
       }
      },
      removeLight:function(){
        for(var key in circleObjects){
          let el =  document.getElementById(self.circleObjects[key].direction)
          el.classList.remove('lighter')
          el.classList.add('darker')
        }
      },
      randNo:function(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
      },
      startFunc:function(){
         let self = this 
         self.ident = false
         self.counter = 0
         self.userArray = []
                   self.moveXY('center') 
         if(!self.scoreArray.length){
           let r = self.randNo(1,4)
           self.scoreArray.push(r)
         }
        self.intrn = setInterval(function(){
          if(self.counter<self.scoreArray.length){
              self.moveXY(self.circleObjects[self.scoreArray[self.counter]-1].direction)

          }else{

            window.clearInterval(self.intrn)
           setTimeout(function(){
         self.moveXY('center')
         },1000)
             self.ident = true
        console.log(self.directions)
          }
         self.counter++ 
        },500)
        
      },
      timeoutFunc:function(){

      }
    },
    mounted:function(){
      let self = this
     if(window.innerWidth < 660){
       self.lowWidth = true
     }
   //let ele  = document.getElementById('adiv')
   //console.log(ele.style)
     var el =  document.getElementById('adiv')
        console.log(el.style)
       for(var key in self.circleObjects){
          let el =  document.getElementById(self.circleObjects[key].direction)
      
         el.classList.remove('lighter')
          el.classList.add('lighter')
        }
    }
 
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height:100%;
  background: #a9a9a9;
}
.tri{
  height:100px;
  width:100px;
  border-radius:50%;
  position:absolute;
  cursor:pointer;
  z-index: 3;
  transition: all 0.1s;
}
.x{
  background:#00f3da;
 left:40%
}
.y{
   background:#0083da;
  top:30%;
}
#left{
  left:30%;
}
#right{
left:50%;
background:#0033ff;

}
#up{
top:10%
}
#down{
top:50%;
background:#ff0000;
}

.bouncingBall{
  height:30px;
  width:30px;
  border-radius:50%;
  background:#fff;
  position:absolute;
  top:34.5%;
   left:42.5%;
    z-index:5;
    transition: all 0.5s;
}
.centerba{
   position:absolute;
   top:34.5%;
   left:42.5%;
}
.upba{
  position:absolute;
    top:14.3%;
  left:42.5%;
}
.leftba{
  position:absolute;
  top:34.5%;
  left:32.3%;
}
.downba{
  position:absolute;
  top:54.6%;
  left:42.5%;
}
adiv{
  overflow:hidden
}
.rightba{
  position:absolute;
   top:34.5%;
   left:52.3%;
}
#row1{
 
}

#he{
  height: 100%;
  width: 100%;
  position :absolute;
  top: 0px;
  left: 0px;
  background:#000;
  text-align:  center;
  color: #FFF;
  z-index: 9;
  overflow:hidden;

}
.lighter{
    box-shadow:5px 5px 4px yellow,
 -5px -5px 4px yellow;
}
.darker{
    box-shadow:6px 5px 4px #a9a9a9,
 -5px -5px 4px #a9a9a9;
}
#form{
  margin-right: 100px;
  padding:20px;
  border-radius:25%;
  margin-top:100px;
  text-align:center;
  background: white;

}
#score{
  margin-top:10px;
  color:red;
  background: #3d3d3d;
  padding: 4px;
}
</style>
