<template>
  <div class="price-list">
    <h4 class="price-list__level">{{ level }}</h4>
    <h3 class="price-list__price">${{ price }}</h3>
    <ul class="price-list__list">
      <li class="price-list__item" v-for="(item, index) in info" :key="index">
        <p class="price-list__info">{{ item.text }}</p>
      </li>
    </ul>
    <a class="price-list__button">
      <p class="price-list__content">LEARN MORE</p></a
    >
  </div>
</template>

<script>
export default {
  name: "price-list",
  props: {
    level: {
      type: String,
      required: true,
    },
    price: {
      type: Number,
      required: true,
    },
    info: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.price-list {
  position: relative;
  box-sizing: border-box;
  width: 327px;
  padding: 31px 29px;
  box-shadow: 0px 20px 40px rgba(212, 210, 244, 0.5);
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 32px;
  opacity: 1;
  cursor: pointer;
  transition: padding 0.2s ease-out;

  & h4,
  & h3,
  &__info,
  .price-list__content,
  .price-list__info {
    transition: color 0.2s ease-out;
  }

  &::after {
    position: absolute;
    z-index: -1;
    content: "";
    width: 100%;
    height: 100%;
    background: linear-gradient(135deg, #a2a7f0 0.06%, #696edd 100.06%);
    opacity: 0;
    transition: opacity 0.2s ease-out;
    border-radius: 10px;
  }

  &::before {
    position: absolute;
    z-index: -1;
    content: "";
    width: 100%;
    height: 100%;
    background-color: #fff;
    transition: opacity 0.2s ease-out;
    border-radius: 10px;
  }

  &:hover {
    &::after {
      opacity: 1;
    }

    & h4,
    & h3,
    .price-list__info {
      color: #fff;
    }

    .price-list__content {
      color: #6d72de;
    }

    .price-list__button::after {
      opacity: 0;
    }

    @media (min-width: 1110px) {
      padding-top: 50px;
      padding-bottom: 50px;
    }
  }

  &__level {
    font-size: 18px;
    line-height: 28px;
    color: #6e728e;
    text-align: center;
  }

  &__price {
    font-size: 72px;
    line-height: 71px;
    letter-spacing: -2.16px;
    color: #4a4d60;
    text-align: center;
  }

  &__info {
    padding: 13px 0;
    font-size: 15px;
    line-height: 28px;
    text-align: center;
    color: #6e728e;
  }

  &__list {
    padding: 0;
    margin: 0;
  }

  &__item {
    list-style: none;
    border-top: 1px solid #dbdce3;
    cursor: pointer;
    box-sizing: border-box;
    width: 288px;

    &:last-child {
      border-bottom: 1px solid #dbdce3;
    }
  }

  &__button {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 6px;
    width: 100%;
    min-height: 44px;

    &::after {
      position: absolute;
      z-index: 0;
      content: "";
      width: 100%;
      height: 100%;
      background: linear-gradient(135deg, #a2a7f0 0.06%, #696edd 100.06%);
      transition: opacity 0.2s ease-out;
      border-radius: 6px;
      opacity: 1;
    }

    &::before {
      position: absolute;
      z-index: 0;
      content: "";
      width: 100%;
      height: 100%;
      background: #fff;
      transition: opacity 0.2s ease-out;
      border-radius: 6px;
      opacity: 1;
    }
  }

  &__content {
    font-size: 13px;
    line-height: 16px;
    text-align: center;
    letter-spacing: 1.39286px;
    color: #fff;
    z-index: 1;
  }
}
</style>
