<template>
  <div class="container">
    <img src="@/assets/images/error.png" alt="error-img">
    <div>
      <p class="title">Сервер не отвечает</p>
      <p class="subtitle">Уже работаем над этим</p>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.title {
  font-weight: 700;
  font-size: 22px;
  line-height: 130%;
  white-space: nowrap
}
.subtitle {
  font-weight: 400;
  font-size: 18px;
  line-height: 130%;
  white-space: nowrap
}
</style>
