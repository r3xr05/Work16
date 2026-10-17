<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <h2 class="mb-4">ระบบตัดเกรด</h2>

        <div class="mb-3">
          <label class="form-label">คะแนน</label>
          <input
            type="number"
            class="form-control"
            v-model="score"
            placeholder="กรอกคะแนน"
          />
        </div>

        <button class="btn btn-primary" @click="calculateGrade">
          คำนวณเกรด
        </button>

        <div v-if="grade !== ''" class="alert alert-success mt-3">
          เกรดของคุณ: <strong>{{ grade }}</strong>
        </div>

        <div v-if="errorMessage" class="alert alert-danger mt-3">
          {{ errorMessage }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      score: '',
      grade: '',
      errorMessage: ''
    }
  },
  methods: {
    calculateGrade() {
      if (this.score === '') {
        this.errorMessage = 'กรุณากรอกคะแนนก่อนคำนวณ'
        this.grade = ''
        return
      }

      const score = Number(this.score)

      if (score > 100) {
        this.errorMessage = 'กรุณากรอกคะแนนให้ถูกต้อง (0-100)'
        this.grade = ''
        return
      }

      this.errorMessage = ''

      if (score >= 80) {
        this.grade = 'A'
      } else if (score >= 70) {
        this.grade = 'B'
      } else if (score >= 60) {
        this.grade = 'C'
      } else if (score >= 50) {
        this.grade = 'D'
      } else {
        this.grade = 'F'
      }
    }
  }
}
</script>
