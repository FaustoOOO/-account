<template>
  <el-card>
    <template #header>记账凭证</template>
    <el-button type="primary">新增凭证</el-button>
    <el-table :data="[]">
      <el-table-column prop="code" label="凭证号" />
      <el-table-column prop="date" label="日期" />
      <el-table-column prop="debit" label="借方" />
      <el-table-column prop="credit" label="贷方" />
    </el-table>
    <el-divider />
    <el-button>借贷平衡校验</el-button>
  </el-card>
</template>

<script setup>
</script>



