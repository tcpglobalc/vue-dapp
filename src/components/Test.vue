<template>
  <div id="app">
    <web3-modal-vue
      ref="web3modal"
      :theme="theme"
      :provider-options="providerOptions"
      cache-provider
    />
  </div>
</template>
<script>
import Web3ModalVue from "web3modal-vue";
import WalletConnectProvider from "@walletconnect/web3-provider";
import { web3Modal } from "./config/mixins";
import Header from "@/components/Header";

export default {
  components: {
    Header,
    Web3ModalVue,
  },
  mixins: [web3Modal],
  data() {
    return {
      theme: "light",
      providerOptions: {
        walletconnect: {
          package: WalletConnectProvider,
          options: {
            infuraId: "-",
          },
        },
      },
      number: 0,
      balance: 0,
    };
  },
  created() {
    if (
      window.matchMedia &&
      window.matchMedia("(prefers-color-scheme: dark)").matches
    ) {
      this.theme = "dark";
    }
  },
  mounted() {
    this.$nextTick(async () => {
      const web3modal = this.$refs.web3modal;
      this.$store.commit("setWeb3Modal", web3modal);
      if (web3modal.cachedProvider) {
        await this.$store.dispatch("connect");
        this.subscribeMewBlockHeaders();
      }
    });
  },
  methods: {
    connect() {
      this.$store.dispatch("connect");
    },
  },
};
</script>