<script setup>
import { Inertia } from '@inertiajs/inertia';

defineProps({
  id : String,
  animals: String,
  blog: Object,
})

const deleteConfirm = (id) => {
  console.log("kidding", id);
  Inertia.delete(`/inertia/${id}`, {
    onBefore : () => {
      confirm("本当に削除しますか？");
    }
  });
}
</script>

<template>
  <div class="m-4">
    你是{{ id }}号🎉
  </div>

  <table class="border-2">
  <thead class="border-2">
    <tr>
      <th scope="col">号码</th>
      <th scope="col">主题</th>
      <th scope="col">&nbsp;&nbsp;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>{{ id }}</td>
      <td>{{ blog.title }}</td>
      <td>
        <button type="button" @click="deleteConfirm(blog.id)">删除</button>
      </td>
    </tr>
  </tbody>
</table>
  
    
  
</template>
