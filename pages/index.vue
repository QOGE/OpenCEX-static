<template>
  <div class="main-bottom-part">
    <Block1 :course="info.btc_usdt_price" />
    <div class="trade">
      <div class="content" style="background-color: initial">
        <CurrencyList :filteredPairs="filteredPairs" />
      </div>
    </div>
  </div>
</template>

<script>
import CurrencyList from '~/components/main/CurrencyList.vue'

import Block1 from '../components/main/Block1.vue'

export default {
  name: "Blog",
  components: { CurrencyList, Block1 },
  head() {
    return {
      title: `${this.$config.axios.title} ${this.$t('title')}`,
        meta: [
            {
                hid: "description",
                name: "description",
                content: `${this.$config.axios.title} ${this.$t("metaMainDescr")}`,
            },
            {
                hid: "og:title",
                name: "og:title",
                content: `${this.$config.axios.title} ${this.$t("metaMainTitle")}`,
            },
            {
                hid: "og:description",
                name: "og:description",
                content: `${this.$config.axios.title} ${this.$t("metaMainDescr")}`,
            },
        ],
    };
  },
  mounted() {
    this.$store.dispatch("getInfoMainPage");
  },
  computed: {
    info() {
      return this.$store.getters.info;
    },
    getPairs() {
      return this.$store.getters.pairs_data;
    },
    filteredPairs() {
      if (this.getPairs) {
        return Object.values(this.getPairs).filter((pair) => {
          return pair.pair_data.quote.code !== "USDT" ? false : pair;
        });
      }
    },
  },
}
</script>

<style lang='scss'>
.trade {
  background: #EEF1F9;
  padding: 72px 0 88px;
}
@media (max-width: 900px) {
  .trade {
    padding: 23px 0 31px;
  }
}
</style>
