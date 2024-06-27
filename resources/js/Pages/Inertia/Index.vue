<script setup>
import { Link } from '@inertiajs/inertia-vue3';

defineProps({
  blogs: Array,
})
</script>

<template>
  <div v-if="$page.props.flash.message">{{ $page.props.flash.message }}</div>
  <ul>
    <li v-for="blog in blogs" :key="blog.id">
      主题：<Link :href="route('inertia.show', {id: blog.id})">{{ blog.title }}</Link>,
      文本：{{ blog.content }}
    </li>
  </ul>
  <p class="m-3">
    她也喝茶吗?🍵
  </p>
</template>
