<template>
  <div id="app">
    <div class="container">
     <div class="breadcrumbs">
       <ul class="breadcrumbs__list">
         <li class="breadcrumbs__item"><a href="/">Главная</a></li>
         <li class="breadcrumbs__item"><a href="#">Системы хранения</a></li>
         <li class="breadcrumbs__item">Комплекты стеллажных систем</li>
       </ul>
     </div>
     <h1>Комплекты стеллажных систем</h1>
     <AllCards />
    </div>
  </div>
</template>

<script>
import AllCards from './components/AllCards.vue'

export default {
  name: 'app',
  components: {
    AllCards,
  }
}
</script>

<style lang="scss">

@font-face {
    font-family: 'SF_Regular';
    font-style: normal;
    font-weight: normal;
    src: local('./assets/fonts/SFUIText-Regular.woff'), url('./assets/fonts/SFUIText-Regular.woff') format('woff');
    }

    @font-face {
    font-family: 'SF_Light';
    font-style: normal;
    font-weight: normal;
    src: local('./assets/fonts/SFUIText-Light.woff'), url('./assets/fonts/SFUIText-Light.woff') format('woff');
    }

    @font-face {
    font-family: 'SF_Medium';
    font-style: normal;
    font-weight: normal;
    src: local('./assets/fonts/SFUIText-Medium.woff'), url('./assets/fonts/SFUIText-Medium.woff') format('woff');
    }

    @font-face {
    font-family: 'SF_Bold';
    font-style: normal;
    font-weight: normal;
    src: local('./assets/fonts/SFUIText-Bold.woff'), url('./assets/fonts/SFUIText-Bold.woff') format('woff');
    }

  html, body {
    margin: 0;
    padding: 0;
    font-family: 'SF_Regular', sans-serif;
  }

  html {
    font-size: 10px;
    height: 100%;
    width: 100%;
    overflow-x: hidden;

    @media (min-width: 1920px) {
        font-size: .52vw;
    }
}

  #app {
    font-family: 'SF_Regular', sans-serif;
  }

  .container {
      width: 100%;
      padding-left: 10%;
      padding-right: 10%;
      box-sizing: border-box;
      margin: 0 auto;
  }

  h1 {
    font-family: 'SF_Medium', sans-serif;
    font-style: normal;
    font-weight: 600;
    font-size: 3.6rem;
    line-height: 4.8rem;
    color: #000000;
    margin: 0 0 3.2rem 0;
    padding: 0;

    @media (max-width: 767px) {
      font-size: 2.6rem;
      line-height: 2.8rem;
    }
  }

  .breadcrumbs {
    margin-top: 3.2rem;
    margin-bottom: 3.2rem;
    &__list{
      list-style-type: none;
      display: flex;
      margin: 0;
      padding: 0;

    @media (max-width: 767px) {
      flex-wrap: wrap;
    }
  }

    &__item {
      font-style: normal;
      font-weight: normal;
      font-size: 1.6rem;
      line-height: 1.6rem;

    @media (max-width: 767px) {
      line-height: 2.6rem;
    }

      a{
        color: #828282;
        text-decoration: none;
        margin-right: 2rem;
        position: relative;

        &::after {
          content: "/";
          position: absolute;
          right: -1.2rem;

        @media (max-width: 767px) {
          top: 0rem;
        }

        @media (max-width: 767px) {
          top: -0.35rem;
          }
        }
      }
    }
  }
</style>