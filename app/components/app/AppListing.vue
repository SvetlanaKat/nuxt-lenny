<template>
  <section class="app-listing">
    <h2 class="app-listing__title section-title">{{ title }}</h2>

    <div class="app-listing__list">
      <slot />
    </div>

<footer class="swiper-footer">
          <button type="button" class="swiper-arrow-prev arrow arrow--left">
            <SvgIcon
        class="more-btn__arrow arrow__icon"
        name="arrow"
        width="91"
        height="60"
      />
  
          </button>

          <div class="swiper-pagination"></div>

          <button type="button" class="swiper-arrow-next arrow">

            <SvgIcon
        class="more-btn__arrow"
        name="arrow"
        width="91"
        height="60"
      />

          </button>
        </footer>

  </section>
</template>

<script setup>
  const props = defineProps({
    title: {
      type: String,
      default: "",
    },
  });
</script>

<style lang="less">
.arrow {
  flex-shrink: 0;
  position: relative;
  display: inline-block;
  width: 92px;
  height: 60px;
  padding: 0;
  border: none;
  background: none;
  color: @black;
  font-size: 0;
  text-decoration: none;
  transition: color 0.2s;
  cursor: pointer;
  @media @bw1340 {
    width: 67px;
    height: 40px;
  }
  &:active {
    color: @red;
  }
  &:hover {
    @media (hover: hover) {
      color: @red;
    }
  }
  
  &--left {
    .arrow__icon {
      transform: rotate(180deg);
    }
  }
}

  .app-listing {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;

   @media @bw650 {
    width: 100%;
    mmin-width: 280px;
   }

    &__more-btn {
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
      align-items: center;
      max-width: 1334px;
      width: 100%;
      margin-right: auto;
      margin-left: auto;
      border-width: 0;
      // @media @bw370 {
      //   max-width: 370px;
      // }
    }

  // .container();

  &__list {
    display: flex;
    flex-wrap: wrap;
    gap: 115px 58px;

    @media @bw1660 {
      justify-content: center;
      gap: 90px 40px;
      margin: 0 -20px -100px;
    }

    @media @bw1340 {
      justify-content: center;
      margin: 0 -15px -100px;
    }

    @media @bw1020 {
      justify-content: center;
      gap: 80px 30px;
    }

    @media @bw768 {
      margin: 0 -10px -80px;
    }

    // @media @bw370 {
    //   gap: 60px 0;
    //   margin: 0 auto 0 auto;
    //   width: 280px;
    //   max-width: 100%;
    // }
  }

   

  // &__event-card {
  //   width: calc(33.3333% - 38.666px);
 
  //   &:nth-child(3n) {
  //     margin-right: 0;
  //   }

  //   @media @bw1660 {
  //     width: calc(33.3333% - 26.666px);
  //     margin: 0 20px 100px;
  //   }

  //   @media @bw1340 {
  //     width: calc(33.3333% - 26px);
  //     margin: 0 15px 100px;
  //   }

  //   @media @bw1020 {
  //     width: calc(50% - 15px);
  //     max-width: 405px;
  //     margin: 0 15px 80px;
  //   }

  //   @media @bw768 {
  //     margin: 0 10px 80px;
  //   }

  //   @media @bw650 {
  //     width: 100%;
  //     margin: 0;
  //   }
  // }

  // &__arrows {
  //   display: grid;
  //   grid-template-columns: 497px 324px 497px 1fr;
  //   grid-template-areas:
  //     "arrow-left arrow-centr arrow-right";
  //   margin-top: 70px;
  //   align-items: center;
  //   justify-items: center;
  // }

  // &__arrow-left {
  //   grid-area: arrow-left;
  //   transform: translateX(162px);

  //   &:hover {
  //     color: @red;
  //     text-decoration-color: @red;
  //   }
  // }

  // &__arrow-centr {
  //   grid-area: arrow-centr;
  // }

  // &__arrow-right {
  //   grid-area: arrow-right;
  //   transform: translateX(-162px);

  //   &:hover {
  //     color: @red;
  //     text-decoration-color: @red;
  //   }
  // }

  // &__icon-centr {
  //   outline: none;
  //   border: none;
  //   padding: 0;
  //   width: 15px;
  //   height: 2px;
  //   background-color: @black;
  // }

  // &__link {
  //   display: inline-flex;
  //   align-self: flex-end;
  //   // width: 100%;
  //   float: right;
  //   // margin-top: 15px;
  //   margin-top: 15px;
  //   font-size: 16px;
  //   font-weight: 600;
  //   color: @black;
  //   line-height: 22px;
  //   font-family: @font1;
  //   text-decoration: none;
  //   transition: color 0.2s;
  //   @media @bw768 {
  //     font-size: 14px;
  //   }
  //    @media @bw370 {
  //     font-size: 14px;
  //     width: 100px;
  //     margin-top: 35px;
  //   }

  //   &:hover {
  //     color: @red;
  //     text-decoration-color: @red;
  //   }

  
  // }
  }
</style>