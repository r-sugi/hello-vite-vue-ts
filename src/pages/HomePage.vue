<template>
  <div class="homePage">
    <h2>HomePage</h2>
    <CounterButton label="Homeページのカウント" :value="count" @countup="addCount" />
    <input type="radio" id="use_all" value="use_all" v-model="picked" @click="onClickRadio('use_all')">
    <label for="use_all">use_all</label>
    <br>
    <input type="radio" id="use_part" value="use_part" v-model="picked" @click="onClickRadio('use_part')">
    <label for="use_part">use_part</label>
    <br>
    <span>Picked: {{ picked }}</span>
    <br>
    <input type="text" id="start" v-model="start" :readonly="rangeReadOnly" :disabled="rangeDisabled">
    <input type="text" id="start" v-model="end" :readonly="rangeReadOnly" :disabled="rangeDisabled">
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import CounterButton from '../components/CounterButton.vue'
import { useRootStore } from '../store'
export default defineComponent({
  components: {
    CounterButton
  },
  setup() {

    const picked = ref("use_all");
    const start = ref("")
    const end = ref("")
    const rangeDisabled = computed(() => picked.value === "use_all")
    const rangeReadOnly = computed(() => picked.value === "use_part")
    const onClickRadio = (value: string) => {
      picked.value = value;
    }

    const store = useRootStore()
    const count = computed(() => store.state.countHome)
    const addCount = () => store.dispatch('addCountHome')
    return {
      count,
      addCount,
      onClickRadio,
      picked,
      start,
      end,
      rangeDisabled,
      rangeReadOnly
    }
  }
})
</script>
