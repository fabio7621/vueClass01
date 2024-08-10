<template>
  <table class="mx-auto mt-5">
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">操作</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="item in drinks" :key="item.id">
        <tr>
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.content }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button class="btn bg-info" @click.prevent="item.qty--" type="button">
              <i class="bi bi-dash"></i>
            </button>
            {{ item.qty }}
            <button class="btn bg-info" @click.prevent="item.qty++" type="button">
              <i class="bi bi-plus"></i>
            </button>
          </td>
          <td>
            <button @click="editDrink(item)" class="btn bg-dark text-white">編輯</button>
          </td>
        </tr>
      </template>
    </tbody>
  </table>
  <table class="mx-auto mt-5">
    <tr>
      <td>
        <label for="teaname">飲料名稱</label>
        <input v-model="tempDrin.name" id="teaname" type="text" />
      </td>
      <td>
        <label for="teacontent">配料</label>
        <input v-model="tempDrin.content" id="teacontent" type="text" />
      </td>
    </tr>
    <tr>
      <td>
        <label for="teaPrice">價錢</label>
        <input v-model="tempDrin.price" id="teaPrice" type="number" min="0" />
      </td>
      <td>
        <label for="teaQty">數量</label>
        <input v-model="tempDrin.qty" id="teaQty" type="number" min="0" />
      </td>
    </tr>
  </table>
  <button @click="addOrUpdateDrink" class="mx-auto d-block mt-5" type="button">送出</button>
</template>

<script setup>
import { reactive, ref } from 'vue'

const tempDrin = ref({
  id: null,
  name: '',
  content: '',
  price: 0,
  qty: 1
})

const drinks = ref([
  { id: 1, name: '珍珠奶茶', content: '香濃奶茶搭配QQ珍珠', price: 50, qty: 20 },
  { id: 2, name: '冬瓜檸檬', content: '清新冬瓜配上新鮮檸檬', price: 45, qty: 18 },
  { id: 3, name: '翡翠檸檬', content: '綠茶與檸檬的完美結合', price: 55, qty: 34 },
  { id: 4, name: '四季春茶', content: '香醇四季春茶，回甘無比', price: 45, qty: 10 },
  { id: 5, name: '阿薩姆奶茶', content: '阿薩姆紅茶搭配香醇鮮奶', price: 50, qty: 25 },
  { id: 6, name: '檸檬冰茶', content: '檸檬與冰茶的清新組合', price: 45, qty: 20 },
  { id: 7, name: '芒果綠茶', content: '芒果與綠茶的獨特風味', price: 55, qty: 18 },
  { id: 8, name: '抹茶拿鐵', content: '抹茶與鮮奶的絕配', price: 60, qty: 20 }
])

const addOrUpdateDrink = () => {
  if (
    tempDrin.value.name !== '' &&
    tempDrin.value.content !== '' &&
    tempDrin.value.price > 0 &&
    tempDrin.value.qty > 0
  ) {
    if (tempDrin.value.id === null) {
      // 新增飲料
      tempDrin.value.id = new Date().getTime()
      drinks.value.push({ ...tempDrin.value })
    } else {
      // 修改飲料
      const index = drinks.value.findIndex((drink) => drink.id === tempDrin.value.id)
      if (index !== -1) {
        drinks.value[index] = { ...tempDrin.value }
      }
    }
    // 清空表單
    resetTempDrink()
  }
}

const editDrink = (item) => {
  tempDrin.value = { ...item }
}

const resetTempDrink = () => {
  tempDrin.value.id = null
  tempDrin.value.name = ''
  tempDrin.value.content = ''
  tempDrin.value.price = 0
  tempDrin.value.qty = 1
}
</script>
