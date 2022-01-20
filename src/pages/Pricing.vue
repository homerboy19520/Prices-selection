<template>
  <div class="pricing-wrapper">
    <div class="pricing-header">
      <h2 class="pricing-header__title">Our Pricing</h2>
      <div class="pricing-header__container">
        <p class="pricing-header__size">Annually</p>
        <div
          class="radio"
          @click="toogle"
          :class="{ 'm-monthly': IsMonthly }"
        ></div>
        <p class="pricing-header__size">Monthly</p>
      </div>
    </div>

    <div class="pricing-container">
      <priceList
        v-for="(item, index) in mokData"
        :key="index"
        :level="item.level"
        :price="item.price"
        :info="item.info"
      />
    </div>

    <div class="pricing-header__box">
      <img
        class="pricing-header__img"
        src="@/assets/background-image.png"
        alt="background-image"
      />
    </div>
        <div class="pricing-header__box_screen">
      <img
        class="pricing-header__img"
        src="@/assets/background-image.png"
        alt="background-image"
      />
    </div>
  </div>
</template>

<script>
import priceList from "@/components/priceList.vue";

export default {
  name: "Pricing",
  components: {
    priceList,
  },
  data() {
    return {
      procent: 20,
      IsMonthly: true,
      pricesWithoutDiscount: [],
      mokData: [
        {
          level: "Basic",
          price: 19.99,
          info: [
            { text: "500 GB Storage" },
            { text: "2 Users Allowed" },
            { text: "Send up to 3 GB" },
          ],
        },
        {
          level: "Professional",
          price: 24.99,
          info: [
            { text: "1 TB Storage" },
            { text: "5 Users Allowed" },
            { text: "Send up to 10 GB" },
          ],
        },
        {
          level: "Master",
          price: 39.99,

          info: [
            { text: "2 TB Storage" },
            { text: "10 Users Allowed" },
            { text: "Send up to 20 GB" },
          ],
        },
      ],
    };
  },

  methods: {
    toogle: function () {
      this.IsMonthly = !this.IsMonthly;

      if (this.IsMonthly == false) {
        this.makeDiscount();
      } else {
        this.makeReverse();
      }
    },

    makeDiscount: function () {
      this.mokData.forEach((item) => {
        let fullPriceMonthly = Math.ceil(item.price);
        let fullPriceAnnualy = fullPriceMonthly * 10;
        let priceWithDiscount =
          fullPriceAnnualy * ((100 - this.procent) / 100);
        item.price = priceWithDiscount;
      });
    },

    makeReverse: function () {
      this.mokData.forEach((item, index) => {
        item.price = this.pricesWithoutDiscount[index];
      });
    },
  },
  mounted() {
    this.mokData.forEach((item) => {
      this.pricesWithoutDiscount.push(item.price);
    });
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  font-family: "Montserrat", sans-serif;
  font-weight: 700;
  background-color: #f7f7fe;
}
h1,
h2,
h3,
h4,
h5,
p {
  margin: 0;
}

.pricing-wrapper {
  position: relative;
  padding: 64px 24px 71px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  gap: 80px;
  overflow: hidden;
}

.pricing-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  gap: 40px;

  &__title {
    color: #6e728e;
    font-size: 32px;
    line-height: 39px;
  }

  &__box {
    position: absolute;
    z-index: -2;
    right: -280px;
    top: -130px;
    width: 470px;
    height: 760px;

    &_screen {
      display: none;

      @media (min-width: 600px) {
        position: absolute;
        z-index: -2;
        display: block;
        left: -11%;
        top: 74%;
        transform: scale(1, -1);
      }
    }
  }

  &__img {
    width: 100%;
    height: 100%;
  }

  &__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;
    gap: 24px;
  }

  &__size {
    font-size: 15px;
    line-height: 28px;
    color: #6e728e;
    opacity: 0.5;
  }
}

.radio {
  display: block;
  position: relative;
  box-sizing: border-box;
  width: 52px;
  height: 32px;
  background: linear-gradient(135deg, #a2a7f0 0%, #696edd 100%);
  border-radius: 16px;
  cursor: pointer;

  &.m-monthly::after {
    left: calc(100% - 28px);
  }

  &::after {
    content: "";
    position: absolute;
    width: 24px;
    height: 24px;
    background-color: #fff;
    border-radius: 50%;
    left: 4px;
    top: 50%;
    transform: translate(0, -50%);
    transition: left 0.2s ease-out;
  }

  &__label {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    cursor: pointer;
  }

  &__checkbox {
  }
}
.pricing-container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
  gap: 32px;

  @media (min-width: 900px) {
    justify-content: space-around;
    flex-direction: row;
    flex-wrap: wrap;
  }

  @media (min-width: 1110px) {
    justify-content: center;
    align-items: center;
    height: 550px;
  }
}
</style>
