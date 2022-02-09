<template>
  <div>
    <button v-if="!isConnected" @click="handleConnectBtnClick">Connect</button>
    <button v-if="isConnected" @click="handleDisconnectBtnClick">
      Disconnect
    </button>
    <pre><code>address: {{ address }}</code></pre>
    <pre
      v-if="phaLink"
    ><code>link: {{ JSON.stringify(phaLink, null, 2) }}</code></pre>
    <span id="alert-area">Phantasma alert area</span>
  </div>
</template>

<script>
import { PhantasmaLink, disconnectLink } from "../domain/phantasma";

export default {
  data() {
    return {
      address: "none",
      phaLink: null,
      isConnected: false,
    };
  },
  methods: {
    handleConnectBtnClick() {
      if (!this.phaLink) {
        this.phaLink = new PhantasmaLink("Blood Rune Token Sale");
      }
      try {
        this.phaLink.login(
          (success) => {
            console.log("success", success);
            this.isConnected = true;
          },
          (p) => {
            console.error(p);
          },
          (x) => {
            console.debug(x);
          }
        );
      } catch (e) {
        console.error(e);
      }
      console.log("click");
    },

    handleDisconnectBtnClick() {
      console.log("disconecting");
      this.phaLink = null;
      this.isConnected = false;
    },
  },
};
</script>

<style scoped>
button {
  font-size: 2rem;
  padding: 0.5rem 1rem;
}
pre {
  font-size: 1rem;
  line-height: 2;
  background: #333;
  padding: 1rem;
  text-align: left;
  margin-bottom: 2rem;
}
</style>
