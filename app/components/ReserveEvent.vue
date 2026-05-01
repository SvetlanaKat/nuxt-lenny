<template>
  <article class="event">
    <div class="event__container">

    <form class="reserve event__reserve" @submit="onSubmit" >

      <div class="reserve__checks"  >
    <h4 class="reserve__section-title">
      Забронировать столик
    </h4>

    <div class="reserve__book">

<FieldCheck 
v-for="(val, key) in checks" 
:key="key" 
:checkedValue="+key" 
name="table"
:label="`${key} стол`"
class="reserve__check"
:red="val.red || false"
:disabled="val.disabled || false"
/>
    </div>
  </div>

 <ReserveScheme 
 :checks="checks" 
 :values="values" 
 @table-click="onTableClick"
 />

      <!-- <div class="reserve__scheme">
  <div class="reserve__scheme-container">
    <h4 class="reserve__scheme-title">Сцена</h4>
    <div class="reserve__scheme-wrapper">
      <SvgIcon
        class="reserve__scene scene"
        name="scene"
        width="780"
        height="399"
      />
    </div>
  </div>
</div> -->

      <div class="reserve__order">
  <h4 class="reserve__section-title">Ваши пригласительные билеты</h4>

  <div 
  class="reserve__tickets-list"
  id="js-reserveTicketsList"
  data-caption="шт." 
  data-currency="₽" 
  >
    <div class="reserve__tickets">
      <div 
      class="reserve__qty" 
      data-caption="шт." 
      data-currency="₽" 
      :data-price="price.red">
      {{red}}
    </div>
      <div class="reserve__sum" data-currency="₽">{{redCost}}</div>
    </div>

    <div class="reserve__tickets">
      <div 
      class="reserve__qty" 
      data-caption="шт." 
      data-currency="₽" 
      :data-price="price.black">
      {{black}}
    </div>
      <div class="reserve__sum" data-currency="₽">{{blackCost}}</div>
      </div>
    </div>

  <div 
  class="reserve__total" 
  data-caption="Сумма" 
  data-currency="₽"
  >
  {{ redCost +  blackCost }}
  </div>

  <button 
  type="submit" 
  class="btn2 btn2--red btn__submit"
  >
    Купить билеты
  </button>
</div>


      <div class="reserve__legend">
    <div class="reserve__prise">
<h4 class="reserve__section-title-right">Стоимость пригласительного билета</h4>

<div
class="reserve__prise-list"
id="js-reservePriceList"
data-caption="₽ | 1 персона"
></div>
  
<div class="reserve__cost-list">
    <div class="reserve__cost">
      <SvgIcon
        class="reserve__icon"
        name="rectangle_red"
        width="24"
        height="24"
      />
      <div class="reserve__qty-right" data-caption="₽ | 1 персона">{{ price.red }}</div>
       <SvgIcon
        class="reserve__icon"
        name="rectangle_black"
        width="24"
        height="24"
      />
      <div class="reserve__qty-right" data-caption="₽ | 1 персона"> {{ price.black }} </div>
    </div>
  </div>

  <div class="event__notation">
     <h4 class="reserve__section-title-ps">Примечание</h4>
  <div class="reserve__tickets-list">
    <div class="reserve__tickets-right">
      <SvgIcon
        class="icon--black"
        name="ellipse_black"
        width="24"
        height="24"
      />
      <SvgIcon
        class="reserve__icon--red"
        name="ellipse_red"
        width="24"
        height="24"
      />
      <div class="reserve__available">доступные места</div>
    </div>
    <div class="reserve__tickets-right">
      <SvgIcon
        class="reserve__icon reserve__icon--gray"
        name="ellipse_gray"
        width="24"
        height="24"
      />
      <div class="reserve__booked">забронировано</div>
    </div>

</div>

    </div>
  </div>
</div>
      
    </form>
</div>
   </article>
</template>

<script setup>
import { useForm } from 'vee-validate';
import { ref } from 'vue';

const checks = ref({
  1: { red: true },
  2: {},
  3: {},
  4: { red: true },
  5: { disabled: true },
  6: {},
  7: { red: true },
  8: { red: true },
  9: { red: true },
  10: {},
  11: {}
});

const price = ref({ red: 1400, black: 1250 });

const { submitCount, handleSubmit, setFieldValue, values} = useForm({
  initialValues: {
    table: []
  }
});

const black = computed(() => {
  return Array.isArray(values.table) ? values.table.reduce(function(sum, current) {
    return sum + (checks.value[current]?.red ? 0 : 1)
  }, 0 ) : 0;
});

const blackCost = computed(() => black.value * price.value.black);

const red = computed(() => {
  return Array.isArray(values.table) ? values.table.reduce(function(sum, current) {
    return sum + (checks.value[current]?.red ? 1 : 0)
  }, 0 ) : 0;
});

const redCost = computed(() => red.value * price.value.red);

const onSubmit = handleSubmit((submitValues)=> {
  console.log(submitValues)
});

const onTableClick = (table) => {
  if (checks.value[table]?.disabled) return;

  const currentArray = Array.isArray(values.table) ? values.table : [];

  let newArray;

  if (currentArray.includes(table)) {
    newArray = currentArray.filter((check) => check !== table)

  } else {
    newArray = [...currentArray, table]
  }

  setFieldValue("table", newArray);
}
</script>

<style lang="less">
.event {
  // padding: 40px 0 150px;
  width: 100%;
  display:block;
  align-items: center;
    &__container {
    .container();
  }
}

.reserve {
  display: grid;
  gap: 65px 11%;
  grid-template-columns: 405px 1fr;
  // grid-template-columns: 405px calc(89% - 405px);
  grid-template-areas:
    "checks scheme"
    "order legend";
  width: 100%;
  margin-bottom: 150px;

  @media @bw1340 {
    gap: 65px 6.5%;
    grid-template-columns: 350px 1fr;
  }

  @media @bw1020 {
    gap: 60px;
    grid-template-columns: 1fr 390px;
    grid-template-areas:
      "scheme scheme"
      "checks legend"
      "checks order";
  }

  @media @bw768 {
    grid-template-columns: 100%;
    grid-template-areas:
      "scheme"
      "legend"
      "checks"
      "order";
  }

  &__book {
    box-sizing: border-box;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    min-height: 23px;
    // padding-left: 23px;

    // color: @black;
    // cursor: pointer;

    // &:last-child {
    //   margin-bottom: 0;
    // }

  }

  &__checks {
    grid-area: checks;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    // background-color: yellow;
  }

  &__check {
    margin-top: 0;
    margin-bottom: 10px;
    padding-left: 0;
  }

  &__reserve>div {
    box-sizing: border-box;
    padding: 10px;
    background-color: coral;
    text-align: center;
  }

  &__scheme {
    grid-area: scheme;
    
    // background-color: rgb(255, 162, 0);
  }

  &__order {
    grid-area: order;
    // background-color: rgb(76, 0, 255);
  }

  &__legend {
    grid-area: legend;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    // background-color: rgb(255, 0, 81);
  }

  &__reserve>div {
    box-sizing: border-box;
    padding: 10px;
    background-color: coral;
    text-align: center;
  }

  &__scheme-wrapper {
    position: relative;
    width: 100%;

    &::after {
      content: "";
      display: block;
      width: 100%;
      padding-top: 51.15384%;
    }
  }

  &__scene {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

&__scheme-title {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto 40px;
  width: 162px;
  height: 34px;
  
  background-color: @black;
  color: @white;
  font-family: @font1;
  font-weight: 600;
  font-size: 16px;
  line-height: 22px;
  text-align: center;
  text-transform: uppercase;
}

  &__tickets {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
  }
&__tickets-right {
display: flex;
    justify-content: flex-end;
}


  &__qty {
    display: block;
    margin-bottom: 16px;
    width: 108px;
    color: @black;
    font-family: @font1;
    font-weight: 400;
    font-size: 16px;
    line-height: 22px;

    &::after {
      content: " " attr(data-caption) " | " attr(data-price);
    }
  }

  &__qty-right {
    box-sizing: border-box;
    position: relative;
    display: block;
    text-align: right;
    margin-bottom: 15px;
    width: 128px;
    color: @black;
    font-family: @font1;
    font-weight: 400;
    font-size: 14px;
    line-height: 19px;

    &::after {
      content: " " attr(data-caption) "  " attr(data-price);
    }
  }

&__available {
  display: flex;
    justify-content: flex-end;
    margin-bottom: 18px;
    margin-top: 0;
    width: 128px;
    color: @black;
    font-family: @font1;
    font-weight: 400;
    font-size: 14px;
    line-height: 19px;
}

&__booked {
  display: flex;
    justify-content: flex-end;
    margin-bottom: 18px;
    margin-top: 0;
    width: 128px;
    color: @black;
    font-family: @font1;
    font-weight: 400;
    font-size: 14px;
    line-height: 19px;
}

  
  &__sum {
    &::after {
      content: attr(data-currency);
      margin-left: 4px;
      font-size: 0.95em;
    }
  }

  &__total {
    text-align: center;
    display: block;
    margin-bottom: 53px;
    margin-top: 10px;
    width: 405px;
    color: @black;
    font-family: @font1;
    font-weight: 600;
    font-size: 20px;
    line-height: 27px;

    &::before {
      content: attr(data-caption);
      margin-right: 30px;
    }

    &::after {
      content: attr(data-currency);
      margin-left: 4px;
      font-size: 0.95em;
    }
  }

  &__order {
    box-sizing: border-box;
    position: relative;
    display: flex;
    flex-direction: column;
    // align-items: flex-start;
    min-height: 23px;
  }

  &__section-title {
    align-items: flex-start;
    display: block;
    margin-bottom: 20px;
    width: 405px;
    color: @black;
    font-family: @font1;
    font-weight: 700;
    font-size: 18px;
    line-height: 25px;
  }

  &__section-title-ps {
    
    margin-bottom: 23px;
    width: 350px;
    color: @black;
    font-family: @font1;
    font-weight: 600;
    font-size: 18px;
    line-height: 25px;
   text-align: right;

  }


&__section-title-right {
    margin-bottom: 20px;
    width: 355px;
    color: @black;
    font-family: @font1;
    font-weight: 700;
    font-size: 18px;
    line-height: 25px;
    
  }

  &__submit {
    display: flex;

    align-items: center;
    text-align: center;
    border: 2px;
    border-color: @red;
    margin-top: 0;
    max-width: 405px;
    width: 100%;
    height: 52px;
    font-family: @font1;
    font-weight: 600;
    font-size: 16px;
    line-height: 22px;

  }
  &__cost-list {
    display: flex;
    justify-content: flex-end;
  }

  &__icon {
    display: flex;
    position: absolute;
    transform: translateX(-37px);

    &--gray {
      color: #bfbfbf;
      transform: translateX(-137px);
    }

    &--red {
color: rgba(188, 51, 36, 1);
transform: translateX(-10px);
    }

    &--black {
      color: rgba(31, 30, 30, 1);
      transform: translateX(2px);
    }
  }
}

.btn2 {
  
  box-sizing: border-box;
  padding: 15px 40px;
  border: 1px solid @black;
  text-decoration: none;
  background-color: transparent;
  outline: none;
  color: @black;
  font-family: @font1;
  font-weight: 600;
  font-size: 16px;
  line-height: 1.375;
  text-align: center;
  overflow: hidden;
  cursor: pointer;
  transition: background-color 0.2s, color 0.2s, border-color 0.2s;

  &:hover {
    background-color: @black;
    color: @white;
  }

  &--red {
    background-color: @red;
    border-color: @red;
    color: @white;

    @media @bw650 {
      order: 1;
      font-size: 14px;
      padding: 15px 70px;
    }

    &:hover {
      background-color: @red_dark;
      border-color: @red_dark;
    }
  }

  &--black {
    background-color: @black;
    border-color: @black;
    color: @white;
  }

  &--white {
    @media @bw650 {
      order: -1;
      font-size: 14px;
      padding: 15px 70px;
    }
  }
}


</style>