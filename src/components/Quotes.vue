<template>
  <div class="container">
    <div id="quoteId" class="quote">
      <h1>{{ quotes[count].text }}</h1>
    </div>
    <div id="buttonDiv">
      <button v-on:click="decrement" id="decrementId"><span>Prev</span><div class="arrow-left"></div></button>
      <div class="buttonDownload" v-on:click="download">Download</div>
      <button v-on:click="increment" id="incrementId"><span>Next</span><div class="arrow-right"></div></button>
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas';

export default {
  name: 'Quotes',
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
  mounted() {
    let quoteElement = document.getElementById("quoteId");
    setTimeout(() => quoteElement.classList.remove("quote"), 1000);
  },
  methods: {
    addClassMethod() {
      let quoteElement = document.getElementById("quoteId");
      quoteElement.classList.add("quote");
      setTimeout(() => quoteElement.classList.remove("quote"), 500);
    },
    decrement: function() {
      (this.count !== 0) ? this.count-- : this.count = -(this.count-4)
      this.addClassMethod()
    },
    increment: function() {
      (this.count !== 4) ? this.count++ : this.count = this.count-4
      this.addClassMethod()
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
.quote {
    opacity: 1;
    animation-name: example;
    animation-duration: 0.5s;
}
@keyframes example {
    0%   {opacity: 0;}
    50%  {opacity: 1;}
    100% {opacity: 1;}
}
#buttonDiv {
  margin-top: 100px;
  display: flex;
  justify-content: space-around;
}
button {
  background: #eff3f6;
  background-image: linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  -webkit-border-radius: 4;
  -moz-border-radius: 4;
  border-radius: 4px;
  font-family: Arial;
  color: #2c3e50;
  font-size: 16px;
  padding: 10px 20px 10px 20px;
  border: 1px solid #666666;
  text-decoration: none;
}
button:hover {
  background: #eff3f6;
  -webkit-box-shadow: 0px 1px 11px #2c3e50;
  -moz-box-shadow: 0px 1px 11px #2c3e50;
  box-shadow: 0px 1px 11px #2c3e50;
  background-image: -webkit-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -moz-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -ms-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -o-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  text-decoration: none;
}
.buttonDownload {
  display: inline-block;
  position: relative;
  padding: 10px 20px 10px 20px;
  -webkit-border-radius: 4;
  -moz-border-radius: 4;
  border-radius: 4px;
  border: 1px solid #666666;
  color: #2c3e50;
  font-size: 16px;
  font-family: sans-serif;
  text-decoration: none;
  text-align: center;
  text-indent: 15px;
  background-color: #eff3f6;
  background-image: linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
}
.buttonDownload:hover {
  background: #eff3f6;
  -webkit-box-shadow: 0px 1px 11px #2c3e50;
  -moz-box-shadow: 0px 1px 11px #2c3e50;
  box-shadow: 0px 1px 11px #2c3e50;
  background-image: -webkit-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -moz-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -ms-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: -o-linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  background-image: linear-gradient(-180deg, #fafbfc 0%, #eff3f6 90%);
  text-decoration: none;
}

.arrow-right {
  float: right;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent;
  border-left: 8px solid #2c3e50;
  margin-left: 10px;
}
.arrow-left {
  float: left;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent; 
  border-right:8px solid #2c3e50; 
  margin-right: 10px;
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
  color: #2c3e50;
}

/* Download arrow shape */
.buttonDownload:after {
  width: 0;
  height: 0;
  margin-left: 3px;
  margin-top: -7px;
  color: #2c3e50;
  border-style: solid;
  border-width: 4px 4px 0 4px;
  border-color: transparent;
  border-top-color: inherit;
  
}

</style>
