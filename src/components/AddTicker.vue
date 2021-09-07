<template>
  <section>
    <div class="flex">
      <div class="max-w-xs">
        <label for="wallet" class="block text-sm font-medium text-gray-700"
          >Тикер</label
        >
        <div class="mt-1 relative rounded-md shadow-md">
          <input
            @keydown.enter="add"
            type="text"
            name="wallet"
            id="wallet"
            v-model="ticker"
            class="block w-full pr-10 border-gray-300 text-gray-900 focus:outline-none focus:ring-gray-500 focus:border-gray-500 sm:text-sm rounded-md"
            placeholder="Например DOGE"
          />
        </div>
      </div>
    </div>
    <AddButton @add-ticker="add" :disabled="disabled" />
  </section>
</template>

<script>
import AddButton from "./AddButton.vue";

export default {
  name: "AddTicker",
  components: {
    AddButton
  },

  props: {
    disabled: {
      type: Boolean,
      required: false,
      default: false
    }
  },

  emits: {
    "add-ticker": value => typeof value === "string" && value.length > 0
  },

  data() {
    return {
      ticker: ""
    };
  },

  methods: {
    add() {
      if (this.ticker.length === 0) {
        return;
      }
      this.$emit("add-ticker", this.ticker);
      this.ticker = "";
    }
  }
};
</script>
