<template>
  <section class="order-section">
    <div class="layout-wrapper">
      
      <div class="content-wrapper">
        <h2 class="section-title">Choose your pizza</h2>
    <div v-if="pizzas.length" class="pizza-options">
      <div
        v-for="(pizza, i) in pizzas"
        :key="pizza.id"
        :class="['pizza-card', { active: selectedPizza === i }]"
        @click="selectPizza(i)"
      >
        <img :src="`/${pizza.name}.png`" :alt="pizza.name" class="pizza-img" />
        <div class="pizza-card-content">
          <h3 class="pizza-name">{{ pizza.name }}</h3>
          <div class="pizza-price">
           <span class="discounted" v-if="pizza.discount.is_active">
             ${{ pizza.discount.final_price.toFixed(2) }}
           </span>
           <span :class="{ strikethrough: pizza.discount.is_active }">
             ${{ pizza.price.toFixed(2) }}
           </span>
          </div>
        </div>
        <img
          v-if="pizza.discount.is_active"
          src="/ribbon.svg"
          alt="Offer Ribbon"
          class="offer-svg"
        />
      </div>
    </div>

    <div class="custom-pizza">
      <h2 class="section-title">Custom Pizza</h2>

      <div class="size-selection" ref="sizeSection">
        <strong>Size</strong>
        <div class="size-options">
          <label v-for="size in sizes" :key="size.id">
            <input
              type="radio"
              name="size"
              :value="size"
              v-model="selectedSize"
            />
            {{ size.name }}
            <span v-if="size.extra_price > 0">
              (+${{ size.extra_price }})
            </span>
          </label>
        </div>
      </div>

      <div class="topping-selection">
        <strong>Toppings</strong>
        <div class="topping-options">
          <label
            v-for="topping in toppings"
            :key="topping.id"
            class="topping-pill"
            :class="{ disabled: !allowedToppingIds.includes(topping.id) }"
          >
            <input
              type="checkbox"
              :value="topping"
              v-model="selectedToppings"
              :disabled="!allowedToppingIds.includes(topping.id)"
            />
            <span>{{ topping.name }}</span>
          </label>
        </div>
      </div>
    </div>
  </div>

  
  <div class="payment-summary">
    <h3>Payment Summary</h3>

    <div class="summary-row">
      <span>{{ pizzas[selectedPizza]?.name }}</span>
      <span>${{ displayPizzaPrice }}</span>
    </div>

    <div class="summary-row">
      <span>Size - {{ selectedSize.name }}</span>
      <span v-if="selectedSize.extra_price > 0">
        ${{ selectedSize.extra_price }}
      </span>
      <span v-else>$0</span>
    </div>

    <div
      v-for="(topping, i) in selectedToppings"
      :key="i"
      class="summary-row"
    >
      <span>{{ topping.name }}</span>
      <span>${{ topping.price }}</span>
    </div>

    <div class="total">
      <span>Total Price</span>
      <span class="total-amount">${{ totalPrice }}</span>
    </div>

    <button class="order-btn" @click="showPopup = true">
      Order Now
    </button>
  </div>
</div>


<div v-if="showPopup" class="popup-overlay">
  <div class="popup-card">
    <div class="popup-icon">
      <img src="/order-success.svg" alt="Success Icon" />
    </div>
    <h2>Order Success</h2>
    <p>Thank you, we have received your order successfully.</p>
    <button class="popup-close" @click="showPopup = false">
      Close
    </button>
  </div>
</div>

  </section>
</template>


<script setup>
import { ref, computed } from 'vue'
import pizzaJson from '../assets/pizza-list.json'
import sizeJson from '../assets/size-list.json'
import toppingJson from '../assets/topping-list.json'

const pizzas = ref(pizzaJson.data)
const sizes = ref(sizeJson.data)
const toppings = ref(toppingJson.data)

const selectedPizza = ref(0)
const selectedSize = ref(sizes.value[0])
const selectedToppings = ref([])

const showPopup = ref(false)
const sizeSection = ref(null) 

function selectPizza(index) {
  if (selectedPizza.value === index) {

    sizeSection.value?.scrollIntoView({ behavior: 'smooth', block: 'start' })
  } else {
    selectedPizza.value = index
    selectedSize.value = sizes.value[0]
    selectedToppings.value = []
  }
}

const allowedToppingIds = computed(() => {
  return pizzas.value[selectedPizza.value]?.toppings || []
})

const sizePrice = computed(() => selectedSize.value?.extra_price || 0)

const displayPizzaPrice = computed(() => {
  const pizza = pizzas.value[selectedPizza.value]
  return pizza.discount.is_active
    ? pizza.discount.final_price
    : pizza.price
})

const totalPrice = computed(() => {
  const toppingCost = selectedToppings.value.reduce((sum, topping) => {
    return sum + (topping?.price || 0)
  }, 0)

  return (displayPizzaPrice.value + sizePrice.value + toppingCost).toFixed(2)
})
</script>



<style scoped>

.order-section {
  padding: 3rem;
  background-color: #F8F8F6;
  font-family: 'Open Sans', sans-serif;
}

.section-title {
  color: #e77e23;
  font-size: 3rem;
  font-weight: 700;
  text-align: left;
  margin-bottom: 1.5rem;
}

.layout-wrapper {
  display: flex;
  justify-content: space-between;
  gap: 2rem;
}

.content-wrapper {
  flex: 1;
  max-width: 81.25rem;
  margin-top: 6.8rem;
  margin-left: 5.3rem;
}

/* Pizza Options */
.pizza-options {
  display: flex;
  flex-wrap: wrap;
  gap: 1.8rem;
  margin-top: 2.8rem;
  margin-bottom: 3rem;
}

.pizza-card {
  display: flex;
  align-items: center;
  width: 24.5rem;
  height: 12.8rem;
  background: #F8F8F6;
  border: 1px solid #ddd;
  border-radius: 1rem;
  padding: 1rem 1.5rem;
  position: relative;
  cursor: pointer;
  transition: background-color 0.3s;
}
.pizza-card:hover {
  background-color: #F8D8BD;
}
.pizza-card.active {
  background-color: #e77e23;
  color: white;
}

.pizza-img {
  width: 9rem;
  height: 9rem;
  object-fit: contain;
  margin: 0.625rem 2rem 0.625rem 0.625rem;
  flex-shrink: 0;
  transition: transform 0.3s ease;
}
.pizza-card:hover .pizza-img,
.pizza-card.active .pizza-img {
  transform: rotate(15deg);
}

.pizza-card-content {
  display: flex;
  flex-direction: column;
}
.pizza-name {
  font-weight: 720;
  font-size: 1.25rem;
  margin-bottom: 0.1875rem;
}
.pizza-price {
  font-size: 1.25rem;
}
.strikethrough {
  text-decoration: line-through;
  color: #aaa;
  margin-left: 0.3rem;
}
.pizza-card.active .discounted {
  color: white;
}
.pizza-card.active .strikethrough {
  color: rgba(255, 255, 255, 0.7);
}
.offer-svg {
  position: absolute;
  top: -0.1rem;
  right: -0.1rem;
  width: 10rem;
  height: auto;
  z-index: 10;
}

/* Custom Pizza */
.custom-pizza {
  margin-top: 9.5rem;
}
.size-selection,
.topping-selection {
  font-size: 1.43rem;
  margin-top: 2rem;
  text-align: left;
}
.size-options {
  display: flex;
  gap: 1.5rem;
  margin-top: 1rem;
}
.size-options span {
  color: grey;
}

.size-options input[type='radio'] {
  appearance: none;
  width: 1.25rem;
  height: 1.25rem;
  border: 0.125rem solid #ccc;
  border-radius: 50%;
  margin-top: 0.75rem;
  margin-right: 0.6rem;
  cursor: pointer;
  position: relative;
  transition: border 0.2s ease;
}
.size-options input[type='radio']:checked {
  border-color: #e77e23;
}
.size-options input[type='radio']::before {
  content: "";
  position: absolute;
  top: 0.2rem;
  left: 0.2rem;
  width: 0.6rem;
  height: 0.6rem;
  border-radius: 50%;
  background-color: #e77e23;
  opacity: 0;
  transition: opacity 0.2s ease;
}
.size-options input[type='radio']:checked::before {
  opacity: 1;
}

/* Topping Pills */
.topping-options {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 2rem 0;
  margin-top: 2rem;
  margin-bottom: 7rem;
}
.topping-pill {
  position: relative;
  width: 100%;
  max-width: 10.6rem;
  border-radius: 999px;
  cursor: pointer;
  text-align: center;
}
.topping-pill input[type='checkbox'] {
  position: absolute;
  opacity: 0;
  pointer-events: none;
}
.topping-pill span {
  display: inline-block;
  width: 100%;
  height: 3.4rem;
  line-height: 3.4rem;
  padding: 0 1rem;
  font-size: 1.25rem;
  font-weight: 600;
  border: 1px solid #000;
  border-radius: 999px;
  transition: all 0.2s ease;
}
.topping-pill.disabled span {
  background-color: #f5f5f5;
  color: #aaa;
  border-color: #ddd;
  cursor: not-allowed;
}
.topping-pill.disabled:hover span {
  border-color: #ddd;
}
.topping-pill input[type='checkbox']:checked + span {
  background-color: #F8D8BD;
  border-color: #e77e23;
  color: #e77e23;
}
.topping-pill:not(.disabled):hover span {
  border-color: #e77e23;
  color: #e77e23;
}

/* Payment Summary */
.payment-summary {
  background: white;
  border-radius: 1rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  margin-top: 6.8rem;
  margin-left: -3.1rem;
  margin-right: 4.4rem;
  width: 24.375rem;
  padding: 1.5rem;
  height: fit-content;
}
.payment-summary h3 {
  color: #e77e23;
  font-size: 1.5rem;
  margin: 0.8rem 0.5rem 1rem;
}
.summary-row {
  font-size: 1.25rem;
  color: gray;
  margin: 0 0.5rem 0.8rem;
  display: flex;
  justify-content: space-between;
}
.payment-summary .total {
  border-top: 1px solid #eee;
  margin-top: 1.5rem;
  padding-top: 1.25rem;
  font-weight: 700;
  font-size: 1.3rem;
  display: flex;
  justify-content: space-between;
}
.payment-summary .total-amount {
  color: #e77e23;
}
.order-btn {
  display: block;
  width: 100%;
  padding: 1rem 1.5rem;
  font-size: 1.1rem;
  font-weight: 700;
  background: #e77e23;
  color: white;
  border: none;
  border-radius: 999px;
  cursor: pointer;
  margin: 2rem auto 0;
}
.order-btn:hover {
  background: #cf6e1d;
}

/* Popup */
.popup-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}
.popup-card {
  background: white;
  padding: 2rem;
  width: 90%;
  max-width: 22.5rem;
  text-align: center;
  border-radius: 1rem;
  box-shadow: 0 0.75rem 1.5rem rgba(0, 0, 0, 0.15);
}
.popup-icon img {
  width: 4rem;
  height: 4rem;
  margin-bottom: 1rem;
}
.popup-card h2 {
  font-size: 1.4rem;
  margin-bottom: 0.5rem;
}
.popup-card p {
  font-size: 1.25rem;
  color: #444;
  margin-bottom: 1.5rem;
}
.popup-close {
  background-color: #e67e22;
  color: white;
  padding: 1rem 1.5rem;
  border: none;
  border-radius: 1.5rem;
  font-size: 1.1rem;
  cursor: pointer;
  width: 100%;
}

@media (max-width: 992px) {
  .layout-wrapper {
    flex-direction: column;
    align-items: center;
  }

  .content-wrapper {
    margin: 4rem 2rem 0;
    max-width: 100%;
  }

  .pizza-card {
    flex-direction: row;
    width: 100%;
    max-width: 28rem;
  }

  .pizza-img {
    width: 7.5rem;
    height: 7.5rem;
    margin-right: 1.25rem;
  }

  .topping-options {
    grid-template-columns: repeat(3, 1fr);
    gap: 1.2rem 0.5rem;
  }

  .payment-summary {
    width: 80%;
    margin: 4rem auto;
  }

  .section-title {
    text-align: center;
    font-size: 2.5rem;
  }
}
</style>
