<script lang="ts">
  import Clock from "./components/Clock.svelte";
  import Battery from "./components/Battery.svelte";

  if(!localStorage.getItem('background_buffer')) {
    fetch('/1091015.jpg').then(res => {
      return res.blob()
    }).then(blob => {
      const file_reader = new FileReader()
      file_reader.readAsDataURL(blob)
      file_reader.onload = e => {
        localStorage.setItem('background_buffer', String(e.target.result))
      }
    })
  }

  let background_image = localStorage.getItem('background_buffer')

  let lang = 'id'
</script>

<svelte:head>
  <title>NekoYashiki (Nekoder Dashboard)</title>
</svelte:head>

<img class='bg' src={background_image} alt="Gambar Latar">

<main>
  <Clock lang={lang} />
  <Battery />

  <div class="lang-select">
    <button on:click|preventDefault={() => {lang = 'id'}}>ID</button>
    <button on:click|preventDefault={() => {lang = 'en'}}>EN</button>
    <button on:click|preventDefault={() => {lang = 'jp'}}>JP</button>
  </div>
</main>

<style scoped lang="less">
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@200;300&family=Roboto+Mono:wght@100;300&display=swap');

  @color-primary: #c50000;
  @color-background: #272727;
  @color-light: #d8d7d7;

  @font-roboto: 'Roboto Mono', monospace;
  @font-ibm:'IBM Plex Mono', monospace;

  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(body) {
    color: @color-light;
    font-family: @font-roboto;
  }

  main {
    position: relative;
    width: 100%;
    height: 100vh;
    overflow: hidden;
    background: linear-gradient(to right, fade(@color-background, 95%), fade(@color-background, 80%), fade(@color-primary, 30%));
    backdrop-filter: blur(6px);
  }

  .bg {
    width: 100%;
    height: 100vh;
    position: absolute;
    z-index: -2;
    object-fit: cover;
    object-position: top;
  }

  .lang-select {
    position: absolute;
    bottom: 20px;
    right: 20px;

    button {
      padding: 10px 16px;
      border:none;
      background: transparent;
      color: @color-light;
      position: relative;
      cursor: pointer;

      &:before {
        content: '';
        width: 100%;
        height: 2px;
        background: @color-primary;
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.2s;
      }

      &:nth-child(1)::after {
        content: 'ID';
        width: 100%;
        height: 0;
        background: @color-background;
        position: absolute;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.2s;
        display: flex;
        overflow: hidden;
        align-items: center;
        justify-content: center;
      }
      &:nth-child(2)::after {
        content: 'EN';
        width: 100%;
        height: 0;
        background: @color-background;
        position: absolute;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.2s;
        display: flex;
        overflow: hidden;
        align-items: center;
        justify-content: center;
      }
      &:nth-child(3)::after {
        content: 'JP';
        width: 100%;
        height: 0;
        background: @color-background;
        position: absolute;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        transition: 0.2s;
        display: flex;
        overflow: hidden;
        align-items: center;
        justify-content: center;
      }

      &:hover::before {
        height: 100%;
        transition: 0.2s;
      }
      
      &:hover::after {
        height: 100%;
        transition: 0.2s;
        transition-delay: 0.5s;
      }
    }
  }
</style>