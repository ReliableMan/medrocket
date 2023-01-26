<template>
  <div class="empty">
    <img src="@/assets/images/empty.png" alt="empty-img">
    <p class="title">Список избранного пуст</p>
    <p class="subtitle">Добавляйте изображения, нажимая на звездочки</p>
  </div>
</template>

<style scoped>
.empty {
  margin: 25% 25%;
}
.title {
  font-weight: 700;
  font-size: 22px;
  line-height: 130%;
}
.subtitle {
  font-weight: 400;
  font-size: 18px;
  line-height: 130%;
  white-space: nowrap
}
</style>
