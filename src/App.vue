<template>
  <table class="mx-auto mt-5">
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="item in drinks" :key="item.name">
        <tr>
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.content }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button @click.prevent="item.qty--" type="button">-</button>
            {{ item.qty }}
            <button @click.prevent="item.qty++" type="button">+</button>
          </td>
        </tr>
      </template>
    </tbody>
  </table>
</template>

<script setup>
import { ref } from 'vue'

const drinks = ref([
  {
    name: '珍珠奶茶',
    content: '香濃奶茶搭配QQ珍珠',
    price: 50,
    qty: 20
  },
  {
    name: '冬瓜檸檬',
    content: '清新冬瓜配上新鮮檸檬',
    price: 45,
    qty: 18
  },
  {
    name: '翡翠檸檬',
    content: '綠茶與檸檬的完美結合',
    price: 55,
    qty: 34
  },
  {
    name: '四季春茶',
    content: '香醇四季春茶，回甘無比',
    price: 45,
    qty: 10
  },
  {
    name: '阿薩姆奶茶',
    content: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    qty: 25
  },
  {
    name: '檸檬冰茶',
    content: '檸檬與冰茶的清新組合',
    price: 45,
    qty: 20
  },
  {
    name: '芒果綠茶',
    content: '芒果與綠茶的獨特風味',
    price: 55,
    qty: 18
  },
  {
    name: '抹茶拿鐵',
    content: '抹茶與鮮奶的絕配',
    price: 60,
    qty: 20
  }
])
</script>

<style></style>
