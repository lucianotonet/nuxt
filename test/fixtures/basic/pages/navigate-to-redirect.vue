<template>
  <div>You should not see me</div>
</template>

<script setup>
definePageMeta({
  middleware: async () => {
    await new Promise(resolve => setTimeout(resolve, 1))
    return navigateTo({ path: '/' }, { redirectCode: 307 })
  }
})
</script>
