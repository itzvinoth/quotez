<template>
  <div class="container">
    <div id="quoteId" >
      <h1>{{ quotes[count].text }}</h1>
    </div>
    <div id="buttonDiv">
      <button v-on:click="decrement"><span>Previous</span><div class="arrow-left"></div></button>
      <button v-on:click="download"><div class="buttonDownload">Download</div></button>
      <button v-on:click="increment"><span>Next</span><div class="arrow-right"></div></button>
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas';


export default {
  name: 'HelloWorld',
  data() {
    return {
      quotes: [{
          text: "That's one small step for a man, one giant leap for mankind - Neil Armstrong"
        }, {
          text: "The Universe is under no obligation to make sense to you - Neil deGrasse Tyson"
        }, {
          text: "I would like to die on Mars. Just not on impact - Elon Musk"
        }, {
          text: "If we can conquer space, we can conquer childhood hunger - Buzz Aldrin"
        }, {
          text: "The eternal silence of these infinite spaces frightens me - Blaise Pascal"
        }
      ],
      count: 0
    }
  },
  methods: {
    decrement: function() {
      (this.count !== 0) ? this.count-- : this.count = -(this.count-4)
    },
    increment: function() {
      (this.count !== 4) ? this.count++ : this.count = this.count-4
      
    },
    download: function() {
      
      var self = this;
      let quoteElement = document.getElementById("quoteId");
      html2canvas(quoteElement).then(canvas => {
        var ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        ctx.font = "32px 'Avenir', Helvetica, Arial, sans-serif";
        ctx.fillStyle = "red";
        var textLength = this.quotes[this.count].text.length;

        ctx.fillText(this.quotes[this.count].text, window.innerWidth/Number(textLength/10), window.innerHeight/2);

        var dataContext = ctx.getImageData(0, 0, canvas.width, canvas.height);
        var compositeOperation = ctx.globalCompositeOperation;

        //set to draw behind current content
        ctx.globalCompositeOperation = "destination-over";

        //set background color
        ctx.fillStyle = "#FFF";

        //draw background / rect on entire canvas
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        var imageData = canvas.toDataURL("image/png");
        var data = imageData.replace(/^data:image\/png/, "data:application/octet-stream");
        var link = document.createElement("a");
        link.download = "quote.png";
        link.href = data;
        document.body.appendChild(link);
        link.click();
      });
    }
  }
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
#quoteId {
    opacity: 1;
    animation-name: example;
    animation-duration: 1s;
}
@keyframes example {
    0%   {opacity: 0;}
    50%  {opacity: 1;}
    100% {opacity: 1;}
}
#buttonDiv {
  margin-top: 100px;
}
button {
  background: #1890ff;
  background-image: -webkit-linear-gradient(top, #1890ff, #1890ff);
  background-image: -moz-linear-gradient(top, #1890ff, #1890ff);
  background-image: -ms-linear-gradient(top, #1890ff, #1890ff);
  background-image: -o-linear-gradient(top, #1890ff, #1890ff);
  background-image: linear-gradient(to bottom, #1890ff, #1890ff);
  -webkit-border-radius: 4;
  -moz-border-radius: 4;
  border-radius: 4px;
  text-shadow: 1px 1px 3px #666666;
  -webkit-box-shadow: 0px 1px 11px #666666;
  -moz-box-shadow: 0px 1px 11px #666666;
  box-shadow: 0px 1px 11px #666666;
  font-family: Arial;
  color: #FFF;
  font-size: 16px;
  padding: 10px 20px 10px 20px;
  border: solid #1890ff 0px;
  text-decoration: none;
}

button:hover {
  background: #3cb0fd;
  background-image: -webkit-linear-gradient(top, #3cb0fd, #3498db);
  background-image: -moz-linear-gradient(top, #3cb0fd, #3498db);
  background-image: -ms-linear-gradient(top, #3cb0fd, #3498db);
  background-image: -o-linear-gradient(top, #3cb0fd, #3498db);
  background-image: linear-gradient(to bottom, #3cb0fd, #3498db);
  text-decoration: none;
}
.arrow-right {
  float: right;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 10px solid #FFF;
  margin-left: 10px;
}
.arrow-left {
  float: left;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent; 
  border-right:10px solid #FFF; 
  margin-right: 10px;
}

.buttonDownload {
  display: inline-block;
  position: relative;
  padding: 10px 25px;
  
  background-color: #1890ff;
  color: white;
  
  font-family: sans-serif;
  text-decoration: none;
  font-size: 0.9em;
  text-align: center;
  text-indent: 15px;
}

.buttonDownload:hover {
  background-color: #333;
  color: white;
}

.buttonDownload:before, .buttonDownload:after {
  content: ' ';
  display: block;
  position: absolute;
  left: 15px;
  top: 52%;
}

/* Download box shape  */
.buttonDownload:before {
  width: 10px;
  height: 2px;
  border-style: solid;
  border-width: 0 2px 2px;
}

/* Download arrow shape */
.buttonDownload:after {
  width: 0;
  height: 0;
  margin-left: 3px;
  margin-top: -7px;
  
  border-style: solid;
  border-width: 4px 4px 0 4px;
  border-color: transparent;
  border-top-color: inherit;
  
  animation: downloadArrow 2s linear infinite;
  animation-play-state: paused;
}

</style>
