<template>
  <div class="text-subtitle-1 ml-4">{{ date }}</div>
</template>

<script>
import { format, addDays} from 'date-fns'
export default {
  data(){
    return {
      date: ''
    }
  },
  methods: {
    getDate(){
      this.date = format(addDays(new Date(),1), 'MMM d, H:mm:ss')
      setTimeout(this.getDate,1000)
    }
  },
  mounted(){
    this.getDate()
  }

}
</script>

<style>

</style>