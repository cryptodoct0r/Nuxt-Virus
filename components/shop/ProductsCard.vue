<template>
  <div
    v-b-tooltip.hover
    class="card card__hover store-item"
    style="width: 18rem;"
    :title="name"
  >
    <img
      loading="lazy"
      width="200px"
      height="200px"
      :src="image"
      class="card-img-top img-fluid store-img"
      :alt="name"
    >
    <hr class="desktop-only">
    <div class="card-body">
      <nuxt-link :to="link">
        <h5 class="card-title crop">
          {{ name | capitalize }}
        </h5>
      </nuxt-link>
      <p class="card-text desktop-only">
        {{ summary }}
      </p>
      <div class="mobile-only">
        <div class="row">
          <div class="col-6 pr-0">
            <p class="card-price">
              {{ price }}
              <span>ГРН</span>
            </p>
          </div>
          <div class="col-6 pl-0">
            <small
              v-show="stock === false"
              class="notInStock"
            >Не в наявності</small>
            <small
              v-show="stock === true"
              class="inStock"
            >В наявності</small>
          </div>
        </div>
      </div>
    </div>
    <div class="card-footer desktop-only">
      <div class="row bg-transparent">
        <div class="col-6 bg-transparent cost">
          <small>
            <s
              v-if="discountPrice>0"
              class="discount-price"
            >{{ discountPrice | currency({symbol: 'грн', thousandsSeparator: ',', fractionCount: '0', fractionSeparator: '.', symbolPosition: 'back', symbolSpacing: true}) }}</s>
            <s
              v-else
              style="color: transparent;"
            >{{ discountPrice | currency({symbol: 'грн', thousandsSeparator: ',', fractionCount: '0', fractionSeparator: '.', symbolPosition: 'back', symbolSpacing: true}) }}</s>
          </small>
          <p class="card-price">
            {{ price | currency({symbol: '', thousandsSeparator: ',', fractionCount: '0', fractionSeparator: '.', symbolPosition: 'back', symbolSpacing: true}) }}
            <span>ГРН</span>
          </p>
        </div>
        <div class="col-6 bg-transparent btn-container">
          <small
            v-show="stock === true"
            class="inStock"
          >В наявності</small>
          <small
            v-show="stock === false"
            class="notInStock"
          >Не в наявності</small>
          <br>

          <nuxt-link
            :to="link"
            tag="button"
            class="btn"
          >
            Купити
          </nuxt-link>
        </div>
      </div>
    </div>

    <nuxt-link
      :to="link"
      tag="button"
      class="card-footer mobile-only"
    >
      Купити
    </nuxt-link>
  </div>
</template>

<script>
export default {
  filters: {
    capitalize: (item) => {
      return item.toUpperCase()
    }
  },
  props: {
    name: {
      type: String,
      required: false,
      default: ''
    },
    brand: {
      type: String,
      required: false,
      default: ''
    },
    type: {
      type: Array || String,
      required: false,
      default: [] | (() => [])
    },
    summary: {
      type: String,
      required: false,
      default: ''
    },
    price: {
      type: String,
      required: false,
      default: ''
    },
    discountPrice: {
      type: String,
      required: false,
      default: ''
    },
    image: {
      type: String,
      required: false,
      default: ''
    },
    link: {
      type: Object,
      required: false,
      default: {} | (() => [])
    },
    stock: {
      type: Boolean,
      default: true,
      required: false
    },
    sales: {
      type: Boolean,
      default: true,
      required: false
    }
  }

}
</script>

<style lang="scss" scoped>
.mobile-only {
  display: none;
}
.card {
  background: #ffffff;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.35);
  border-radius: 16.7347px;

  width: 100%;
  min-width: 250px;
  max-width: 250px;
  height: 250px;
  border: 0;
}

.card-body {
  padding: 5px 20px;
}

.card-img-top {
  border-radius: 16.7347px 16.7347px 0px 0px;
  width: 250px;
  height: 100%;
  min-height: 135px;
  max-height: 135px;
  object-fit: scale-down;
  object-position: center;
}

hr {
  width: 82%;
  align-self: center;
  margin: 0;
  border: 1px solid #c4c4c4;
}

.card-title {
  font-family: $mainFont;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 16px;

  color: #000000;
  text-align: left;
  margin-bottom: 5px;
}

.crop {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  width: 205px;
}

.card-text {
  font-family: $mainFont;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 11px;

  color: #8b8b8b;
  text-align: left;
  margin-bottom: 3px;
}

.card-footer {
  background: transparent;
  border-top: 0;
  border-bottom-left-radius: 16.7347px;
  border-bottom-right-radius: 16.7347px;

  padding: 0 20px;
}

.cost {
  text-align: left;
}

.btn-container {
  margin-top: -10px;
}

.discount-price {
  font-family: $mainFont;
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
  line-height: 14px;
  text-align: center;
  text-decoration-line: line-through;

  color: #d7000b;
}

.inStock {
  font-family: $secondaryFont;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;

  text-align: center;

  color: #239a0f;
}

.notInStock {
  font-family: $secondaryFont;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;

  text-align: center;

  color: #d7000b;
}

.card-price {
  font-family: $mainFont;
  font-style: normal;
  font-weight: bold;
  font-size: 20px;
  line-height: 19px;
  letter-spacing: -0.05em;

  color: #8b8b8b;

  span {
    font-family: $mainFont;
    font-style: normal;
    font-weight: bold;
    font-size: 12px;
    line-height: 10px;

    text-align: center;

    color: #8b8b8b;
  }
}

.btn {
  background: #d41f26;
  border-radius: 41.8367px;

  padding: 7px 22px;

  font-family: $secondaryFont;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 16px;

  text-align: center;

  color: #ffffff;
}

.card__hover {
  transition: transform 500ms;
  -webkit-transition: transform 500ms;
  -moz-transition: transform 500ms;
  -ms-transition: transform 500ms;
  -o-transition: transform 500ms;

  &::after {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transition: opacity 2s cubic-bezier(0.165, 0.84, 0.44, 1);
    box-shadow: 0 8px 17px 0 rgba(0, 0, 0, 0.2),
      0 6px 20px 0 rgba(0, 0, 0, 0.15);
    content: "";
    opacity: 0;
    z-index: -1;
    border-radius: 20px;
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
    -ms-border-radius: 20px;
    -o-border-radius: 20px;
  }

  &:hover,
  &:focus {
    transform: scale3d(1.01, 1.01, 1);
    -webkit-transform: scale3d(1.01, 1.01, 1);
    -moz-transform: scale3d(1.01, 1.01, 1);
    -ms-transform: scale3d(1.01, 1.01, 1);
    -o-transform: scale3d(1.01, 1.01, 1);

    &::after {
      opacity: 1;
    }
  }
}

@include mediaMd {
  .mobile-only {
    display: block;
  }

  .crop {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 142px;
  }

  .desktop-only {
    display: none;
  }

  .card {
    background: #ffffff;
    box-shadow: 0px 4px 13.3333px rgba(0, 0, 0, 0.25);
    border-radius: 10px;

    width: 100%;
    min-width: 160px;
    max-width: 160px;
    height: 160px;
  }

  .card-body {
    padding: 2.5px 10px;
  }

  .card-img-top {
    border-radius: 10px;
    width: 160px;
    height: 100%;
    min-height: 80px;
    max-height: 80px;
    object-fit: scale-down;
    object-position: center;
  }

  .card-title {
    font-size: 12px;
    line-height: 14px;
  }

  .card-footer {
    padding: 4px 52px;
    background: #d41f26;
    border-radius: 0px 0px 10px 10px;

    border: 0;

    font-family: $secondaryFont;
    font-style: normal;
    font-weight: bold;
    font-size: 18px;
    line-height: 21px;

    align-items: center;
    text-align: center;

    color: #ffffff;
  }

  .card-price {
    font-family: $mainFont;
    font-style: normal;
    font-weight: bold;
    font-size: 14px;

    letter-spacing: -0.05em;
    text-align: left;

    color: #8b8b8b;

    margin: auto;
    padding-top: 5px;

    span {
      font-size: 14px;
    }
  }

  .inStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: #239a0f;
  }

  .notInStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: $redColor;
  }
}

@include mediaSm {
  .mobile-only {
    display: block;
  }

  .desktop-only {
    display: none;
  }

  .card {
    background: #ffffff;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.25);
    border-radius: 10px;

    width: 100%;
    min-width: 160px;
    max-width: 160px;
    height: 160px;
  }

  .card-body {
    padding: 2.5px 10px;
  }

  .card-img-top {
    border-radius: 10px;
    width: 160px;
    height: 100%;
    min-height: 80px;
    max-height: 80px;
    object-fit: scale-down;
    object-position: center;
  }

  .card-title {
    font-size: 12px;
    line-height: 14px;
  }

  .card-footer {
    padding: 4px 52px;
    background: #d41f26;
    border-radius: 0px 0px 10px 10px;

    border: 0;

    font-family: $secondaryFont;
    font-style: normal;
    font-weight: bold;
    font-size: 18px;
    line-height: 21px;

    align-items: center;
    text-align: center;

    color: #ffffff;
  }

  .card-price {
    font-family: $mainFont;
    font-style: normal;
    font-weight: bold;
    font-size: 14px;

    letter-spacing: -0.05em;
    text-align: left;

    color: #8b8b8b;

    margin: auto;
    padding-top: 5px;

    span {
      font-size: 14px;
    }
  }

  .inStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: #239a0f;
  }

  .notInStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: $redColor;
  }
}

@include mediaXSm {
  .crop {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 120px;
  }

  .card {
    background: #ffffff;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.25);
    border-radius: 10px;

    width: 100%;
    min-width: 130px;
    max-width: 130px;
    height: 130px;
  }

  .card-body {
    padding: 1.25px 5px;
  }

  .card-img-top {
    border-radius: 10px;
    width: 130px;
    height: 100%;
    min-height: 55px;
    max-height: 55px;
    object-fit: scale-down;
    object-position: center;
  }

  .card-title {
    font-size: 12px;
    line-height: 14px;
  }

  .card-footer {
    padding: 4px 25px;
    background: #d41f26;
    border-radius: 0px 0px 10px 10px;

    border: 0;

    font-family: $secondaryFont;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 20px;

    align-items: center;
    text-align: center;

    color: $lightColor;
  }

  .card-price {
    font-family: $mainFont;
    font-style: normal;
    font-weight: bold;
    font-size: 12px;

    letter-spacing: -0.05em;
    text-align: left;

    color: #8b8b8b;

    margin: auto;
    padding-top: 5px;

    span {
      font-size: 12px;
    }
  }

  .inStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: #239a0f;
  }

  .notInStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 10px;

    align-items: center;
    text-align: right;

    color: $redColor;
    margin-left: -2.5px;
  }
}

@include mediaXXSm {
  .crop {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    width: 120px;
  }

  .card {
    background: #ffffff;
    box-shadow: 0px 4px 13.3333px rgba(0, 0, 0, 0.25);
    border-radius: 10px;

    width: 100%;
    min-width: 130px;
    max-width: 130px;
    height: 130px;
  }

  .card-body {
    padding: 1.25px 5px;
  }

  .card-img-top {
    border-radius: 10px;
    width: 130px;
    height: 100%;
    min-height: 55px;
    max-height: 55px;
    object-fit: scale-down;
    object-position: center;
  }

  .card-title {
    font-size: 12px;
    line-height: 14px;
  }

  .card-footer {
    padding: 4px 25px;
    background: #d41f26;
    border-radius: 0px 0px 10px 10px;

    border: 0;

    font-family: $secondaryFont;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 20px;

    align-items: center;
    text-align: center;

    color: $lightColor;
  }

  .card-price {
    font-family: $mainFont;
    font-style: normal;
    font-weight: bold;
    font-size: 12px;

    letter-spacing: -0.05em;
    text-align: left;

    color: #8b8b8b;

    margin: auto;
    padding-top: 5px;

    span {
      font-size: 12px;
    }
  }

  .inStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 12px;

    align-items: center;
    text-align: right;

    color: #239a0f;
  }

  .notInStock {
    font-family: $secondaryFont;
    font-style: normal;
    font-weight: normal;
    font-size: 10px;
    line-height: 10px;

    align-items: center;
    text-align: right;

    color: $redColor;
    margin-left: -2.5px;
  }
}
</style>
