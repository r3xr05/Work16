<template>
  <div class="container my-5">
    <h2 class="text-center mb-4">💰 ราคาทองวันนี้</h2>

    <div class="text-center mb-3">
      <button class="btn btn-primary" @click="fetchGold">
        🔄 อัปเดต
      </button>
    </div>

    <table class="table table-bordered table-striped text-center">
      <thead class="table-dark">
        <tr>
          <th>ประเภททอง</th>
          <th>ราคารับซื้อ</th>
          <th>ราคาขายออก</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="item in golds" :key="item.name">
          <td>{{ item.name }}</td>
          <td class="text-success">
            {{ formatNumber(item.buy) }} บาท
          </td>
          <td class="text-danger">
            {{ formatNumber(item.sell) }} บาท
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const golds = ref([])

const fetchGold = async () => {
  try {
    const res = await fetch('https://api.chnwt.dev/thai-gold-api/latest')
    const data = await res.json()
    const price = data.response.price

    golds.value = [
      {
        name: 'ทองรูปพรรณ',
        buy: parseFloat(price.gold.buy.replace(/,/g, '')),
        sell: parseFloat(price.gold.sell.replace(/,/g, ''))
      },
      {
        name: 'ทองคำแท่ง',
        buy: parseFloat(price.gold_bar.buy.replace(/,/g, '')),
        sell: parseFloat(price.gold_bar.sell.replace(/,/g, ''))
      }
    ]
  } catch (error) {
    console.error('โหลดข้อมูลผิดพลาด:', error)
  }
}

const formatNumber = (num) => {
  return num.toLocaleString()
}

onMounted(fetchGold)
</script>
