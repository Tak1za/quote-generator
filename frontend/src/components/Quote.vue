<template>
  <div class="container">
    <h1>Words to live by...</h1>
    <blockquote v-if="quote != null" :cite="quote.author">{{quote.text}}</blockquote>
    <!-- <a @click="getNewQuote">
      Press Me!
    </a>-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      quote: null,
      interval: null,
    };
  },
  methods: {
    getNewQuote: function () {
      var self = this;
      this.interval = setInterval(() => {
        window.backend.Quotes.GetQuote().then((result) => {
          self.quote = result;
        });
      }, 5000);
    },
  },
  created() {
    this.getNewQuote();
  },
  beforeDestroy() {
    clearInterval(this.interval);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 100%;
  max-width: 480px;
  min-width: 320px;
  padding: 1.5em;
  opacity: 0.8;
  border-radius: 1em;
  border-color: #117;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

p {
  margin-bottom: 1.5em;
}
p:last-child {
  margin-bottom: 0;
}

blockquote {
  display: block;
  border-width: 2px 0;
  border-style: solid;
  border-color: #eee;
  padding: 2.5em 0 0.5em;
  margin: 1.5em 0;
  position: relative;
  color: #fffb04;
}

blockquote:before {
  content: "\201C";
  position: absolute;
  top: 0em;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #131313;
  width: 3rem;
  height: 2rem;
  font: 6em/1.08em sans-serif;
  color: #eee;
  text-align: center;
}
blockquote:after {
  content: "\2013 \2003"attr(cite);
  display: block;
  text-align: right;
  font-size: 1.15em;
  color: #53cdff;
  margin: 1em;
}

/* https://fdossena.com/?p=html5cool/buttons/i.frag */

a:hover {
  font-size: 1.7em;
  border-color: blue;
  background-color: blue;
  color: white;
  border: 3px solid white;
  border-radius: 10px;
  padding: 9px;
  cursor: pointer;
  transition: 500ms;
}
a {
  font-size: 1.7em;
  border-color: white;
  background-color: #121212;
  color: white;
  border: 3px solid white;
  border-radius: 10px;
  padding: 9px;
  cursor: pointer;
  display: inline-block;
}
</style>
