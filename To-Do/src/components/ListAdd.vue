<template>
  <div>
    <v-textarea
      outline
      v-model="memo"
      label="Add To-Do here."
      value=""
    ></v-textarea>
    <v-btn v-if="mode === 'add'" @click="listAdd">Add</v-btn>
    <v-btn v-else @click="listEdit">Modifying</v-btn>
  </div>
</template>

<script>
import { eventBus } from "../main"
export default {
  data() {
    return {
      memo: null,
      index: null,
      mode: "add"
    }
  },
  created() {
    eventBus.$on("listEdit", (memo, index) => {
      this.memo = memo
      this.index = index
      this.mode = "edit"
    })
  },
  methods: {
    listAdd() {
      if (this.memo === null) {
        alert("Please enter your content.")
      } else {
        this.$emit("listAdd", this.memo)
        this.memo = null
      }
    },
    listEdit() {
      if (this.memo === null) {
        alert("Please enter your content.")
      } else {
        this.$emit("listEdit", this.memo, this.index)
        this.memo = null
        this.mode = "add"
      }
    }
  }
}
</script>