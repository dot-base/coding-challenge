<template>
  <div>
    <h1>hello world test</h1>
    asdfadfs
    <Button label="Verify" />
    <pre>{{ data }}</pre>
  </div>
</template>

<script setup lang="ts">
const { data } = await useFetch("/api/user");
</script>
