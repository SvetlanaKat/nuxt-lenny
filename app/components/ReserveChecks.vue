<template>
 <div class="reserve__checks">
    <h4 class="reserve__section-title">
      Забронировать столик
    </h4>

    <div class="reserve__book">
    <label class="reserve__check check check--red">
      <input
        type="checkbox"
        name="table_1"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">1 стол</span>
    </label>

    <label class="reserve__check check">
      <input
        type="checkbox"
        name="table_2"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">2 стол</span>
    </label>

   <label class="reserve__check check">
      <input
        type="checkbox"
        name="table_3"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">3 стол</span>
    </label>

    <label class="reserve__check check check--red">
      <input
        type="checkbox"
        name="table_4"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">4 стол</span>
    </label>

   <label class="reserve__check check check--disabled">
      <input
        type="checkbox"
        name="table_5"
        class="check__input"
        disabled
      />
      <span class="check__mark"></span>
      <span class="check__label">5 стол </span>
    </label>

    <label class="reserve__check check">
      <input
        type="checkbox"
        name="table_6"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">6 стол</span>
    </label>

    <label class="reserve__check check check--red">
      <input
        type="checkbox"
        name="table_7"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">7 стол</span>
    </label>

    <label class="reserve__check check check--red">
      <input
        type="checkbox"
        name="table_8"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">8 стол</span>
    </label>

    <label class="reserve__check check check--red">
      <input
        type="checkbox"
        name="table_9"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">9 стол</span>
    </label>

    <label class="reserve__check check">
      <input
        type="checkbox"
        name="table_10"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">10 стол</span>
    </label>

    <label class="reserve__check check">
      <input
        type="checkbox"
        name="table_11"
        class="check__input"
      />
      <span class="check__mark"></span>
      <span class="check__label">11 стол</span>
    </label>
   
    
    </div>
  </div>
</template>

<script setup></script>

<style lang="less">
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
  }

  &__reserve>div {
    box-sizing: border-box;
    padding: 10px;
    background-color: coral;
    text-align: center;
  }
}


</style>