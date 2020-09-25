<template>
  <div>
    <div class="columns is-mobile" style="margin-bottom: 2rem">
      <div class="column" style="height: 700px; border: solid black 4px; padding: 2rem;overflow-y: scroll" ref="mainWindow">
        <div v-for="disc in discussion" class="columns">
          <div :id="disc.id" class="column is-4 transition" style="border: solid black 1px; width: 50%; margin-bottom: 1rem; "
               :class="{'is-offset-6' : disc.who}">{{disc.Mess}}</div>
        </div>
      </div>
    </div>
    <div class="columns  is-mobile">
      <form class="column" v-on:submit.prevent="printMessage">
        <input aria-placeholder="Ecris ici !" style="height: 50px; border: solid black 1px; text-align: center; width: 100%"
               v-model="message" v-on:submit="printMessage()">
        </input>
      </form>
    </div>
  </div>


</template>

<script>
export default {
  name: "mainBox",
  data() {
    return {
      discussion: [{ Mess : "Bienvenue sur le tchat", who : 0, id : 0}, {Mess :"Essaye maintenant", who : 0, id : 1}],
      message :""
    }
  },
  methods: {
    printMessage(e) {
      if (this.message !== "") {
        let newid = new Date().valueOf()
        this.discussion.push({Mess : this.message, who : 1, id : newid})
        this.message = ""

        this.updateScroll(newid)
      }

    },
    updateScroll(id){
      setTimeout(() => {
        console.log(this.$refs.mainWindow.lastChild)
        this.$refs.mainWindow.scrollTo(0, document.getElementById(id).scrollHeight)
      }, 500)

    }
  }
}
</script>

<style scoped>
@keyframes appearFromWhite {
  0% {
    opacity: 0;
    transform: translateY(10px);
  }
  100% {
    opacity: 100;
  }
}
.transition {
  animation: 0.5s appearFromWhite;
}
</style>
