<template>
  <div>
    <p>
      User iD: {{userId}}
    </p>
  </div>
</template>

<script>
export default {
  data(){
    return{
      userId: this.$route.params.id
    }
  }
}
</script>
