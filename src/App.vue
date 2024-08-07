<script setup>
import { ref } from 'vue'

const items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    subscription: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    total: 'num1',
    way: 'minus1'
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    subscription: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    subscription: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    name: '四季春茶',
    subscription: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    subscription: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    subscription: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    subscription: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    subscription: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])
const changeStockNum = (item, action) => {
  if (action === 'plus') {
    item.stock += 1
  } else if (action === 'minus') {
    if (item.stock >= 1) item.stock -= 1
  }
}
const tempEdit = ref({
  id: '',
  name: ''
})
const prepareEdit = (item) => {
  tempEdit.value = { ...item }
  console.log(tempEdit.value)
}
const confrimEdit = () => {
  const index = items.value.findIndex((item) => item.id === tempEdit.value.id)
  console.log(index)
  items.value[index] = tempEdit.value
  tempEdit.value = {}
}
</script>

<template>
  <h1>目前是App.vue</h1>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.name }}</td>
        <td>
          <small>{{ item.subscription }}</small>
        </td>
        <td>{{ item.price }}</td>
        <td>
          <button type="button" @click="changeStockNum(item, 'minus')">-</button>
          {{ item.stock }}<button type="button" @click="changeStockNum(item, 'plus')">+</button>
          <button type="button" @click="prepareEdit(item)">編輯</button>
        </td>
      </tr>
    </tbody>
  </table>
  <hr />
  <div>當前修改的值{{ tempEdit.name }}</div>
  <input type="text" v-model="tempEdit.name" />
  <button type="button" @click="confrimEdit">確認編輯</button>
</template>

<style></style>
