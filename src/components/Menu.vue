<template>
  <div id="menu">
    <button @click="connectWallet">Connect Wallet</button>
    <button @click="connectW3">Connect Web3</button>
  </div>
</template>

<script>
import Web3 from "web3";
import getWeb3 from "../utils/getWeb3";

export default {
  components: {},
  data() {
    return {};
  },
  methods: {
    async connectWallet(event) {
      try {
        let web3 = new Web3(Web3.givenProvider || "ws://localhost:8545");
        console.log(web3.version);
        if (typeof window.ethereum !== "undefined") {
          console.log("MetaMask is installed!");
          window.ethereum.request({ method: "eth_requestAccounts" });
          const accounts = await window.ethereum.request({
            method: "eth_requestAccounts",
          });
          const account = accounts[0];
          console.log(account);
          console.log(window.ethereum.selectedAddress);
        }
      } catch {
        console.log("catch");
      } finally {
        console.log("finally");
      }
    },
    async connectW3(event) {
      try {
        let connection = new getWeb3();
        connection.getWeb3();
      } catch {
        console.log("catch");
      } finally {
        console.log("finally");
      }
    },
  },
};
</script>

<style>
</style>