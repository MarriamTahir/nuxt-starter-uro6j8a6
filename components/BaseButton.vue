<template>
  <NuxtLink :to="to" class="btn-wrap interactive" ref="btn">
    <div class="btn-content">
      <span class="btn-text">
        <span class="text-inner">{{ text }}</span>
        <span class="text-inner hover-text">{{ text }}</span>
      </span>
      <div class="btn-dot"></div>
    </div>
  </NuxtLink>
</template>

<script setup>
defineProps({ text: String, to: String });
</script>

<style scoped>
.btn-wrap {
  display: inline-flex; position: relative; padding: 16px 36px;
  background: #e2d9c8; border-radius: 100px; overflow: hidden;
  text-decoration: none; transition: transform 0.3s ease-out;
}
.btn-wrap::before {
  content: ""; position: absolute; inset: 0; background: #151415;
  transform: translateY(100%); transition: transform 0.6s cubic-bezier(0.19, 1, 0.22, 1);
}
.btn-wrap:hover::before { transform: translateY(0); }
.btn-content { position: relative; z-index: 1; display: flex; align-items: center; gap: 10px; }
.btn-text { display: block; height: 1.2em; overflow: hidden; position: relative; font-size: 13px; text-transform: uppercase; font-weight: 600; }
.text-inner { display: block; transition: transform 0.6s cubic-bezier(0.19, 1, 0.22, 1); color: #151415; }
.hover-text { position: absolute; top: 100%; left: 0; color: #e2d9c8; }
.btn-wrap:hover .text-inner { transform: translateY(-100%); }
.btn-dot { width: 5px; height: 5px; background: #151415; border-radius: 50%; transition: background 0.4s; }
.btn-wrap:hover .btn-dot { background: #e2d9c8; }
</style>