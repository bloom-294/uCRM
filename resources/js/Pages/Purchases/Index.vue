<script setup>
import { onMounted, ref } from 'vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link } from '@inertiajs/vue3';
import FlashMessage from '@/Components/FlashMessage.vue';
import Pagination from '@/Components/Pagination.vue';
import { Inertia } from '@inertiajs/inertia';
import dayjs from 'dayjs';

const props = defineProps({
  orders : Object,
});

onMounted(() => {
  console.log(props.orders.data);
});
</script>

<template>
  <Head title="購買履歴" />

  <AuthenticatedLayout>
      <template #header>
          <h2 class="font-semibold text-xl text-gray-800 leading-tight">購買履歴</h2>
      </template>

      
      <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
          <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
            <div class="p-6 text-gray-900">
              <section class="text-gray-600 body-font">
                <div class="container px-5 py-8 mx-auto">
                  <FlashMessage />
                  <div class="flex pl-4 my-4 lg:w-2/3 w-full mx-auto">
                          <div class="flex">
                            <input type="text" name="search" v-model="search" class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out" placeholder="タナカ"/>
                            <button class="flex mx-auto text-white bg-blue-300 border-0 py-2 px-4 ml-1 focus:outline-none hover:bg-blue-400 rounded whitespace-nowrap items-center"
                            @click="searchCustomers">検索</button>
                          </div>
                        </div>
                        <div class="lg:w-2/3 w-full mx-auto overflow-auto">
                          <table class="table-auto w-full text-left whitespace-no-wrap">
                            <thead>
                              <tr>
                                <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100 rounded-tl rounded-bl">ID</th>
                                <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">氏名</th>
                                <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">合計金額</th>
                                <th class="px-4 py-3 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100">ステータス</th>
                                <th class="w-10 title-font tracking-wider font-medium text-gray-900 text-sm bg-gray-100 rounded-tr rounded-br">購入日</th>
                              </tr>
                            </thead>
                            <tbody>
                              <tr v-for="order in props.orders.data" :key="order.id">
                                <td class="border-b-2 border-gray-200 px-4 py-3 text-blue-300 hover:text-blue-500">
                                  <Link :href="route('purchases.show', { purchase:order.id })">{{ order.id }}</Link>
                                </td>
                                <td class="border-b-2 border-gray-200 px-4 py-3">{{ order.customer_name }}</td>
                                <td class="border-b-2 border-gray-200 px-4 py-3">{{ order.total }}</td>
                                <td class="border-b-2 border-gray-200 px-4 py-3">{{ order.status }}</td>
                                <td class="border-b-2 border-gray-200 px-4 py-3 whitespace-nowrap">{{ dayjs(order.created_at).format('YYYY-MM-DD HH:mm') }}</td>
                              </tr>
                            </tbody>
                          </table>
                        </div>

                      </div>
                      <Pagination :links="props.orders.links"></Pagination>
                    </section>
                  </div>
              </div>
          </div>
      </div>
  </AuthenticatedLayout>
</template>
