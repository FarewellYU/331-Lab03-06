<template>
  <div class="item">
    <i class="icon-wrapper">
      <slot name="icon"></slot>
    </i>
    <div class="details">
      <h3 class="item-heading">
        <slot name="heading"></slot>
      </h3>
      <div class="item-content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
.item {
  display: flex;
  align-items: center;
  padding: 1rem;
  margin-bottom: 1.5rem;
  border-radius: 12px;
  background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
}

.item:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.icon-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #fff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  margin-right: 1rem;
}

.details {
  flex: 1;
  color: #333;
}

.item-heading {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #222;
  transition: color 0.3s;
}

.item-heading:hover {
  color: #007bff;
}

.item-content {
  font-size: 1rem;
  color: #555;
}
</style>
