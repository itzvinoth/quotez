<template>
  <div class="hello">
    <div id="quoteId">
      <h1>{{ quotes[count].text }}</h1>
    </div>
    <div><button v-on:click="decrement">Previous</button><button v-on:click="download" id="btnid">Download</button><button v-on:click="increment">Next</button></div>
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
      var quoteElement = document.getElementById("quoteId");
      html2canvas(quoteElement).then(canvas => {
        
        

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
</style>
