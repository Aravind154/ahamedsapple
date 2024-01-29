<template >
  <div class="topnav">
  <div class="Header">
    <div class="logo">
    <img src="~/assets/inner-logo.png" alt="Company Logo" >
  </div>
  <div class="paragraph">
    <p>Ahamed's Apple</p>
  </div>
  <div class="nav">
<nav>
 <ul>
  <NuxtLink to="Home" class="nav-item ">
  <li>HOME</li>
</NuxtLink >
<NuxtLink to="chatbotreport" class="nav-item chatbot-report">
  <li >CHAT BOT REPORT</li>
</NuxtLink >  
<NuxtLink to ="profile" class="nav-item">
  <li>PROFILE</li>
</NuxtLink >
</ul>
</nav>
</div>

<div class="topnav">
<nuxt-link to="/login">
<button type="submit" class="back-button">
  <svg width="60" height="0" viewBox="0 0 90 90" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<rect width="90" height="90" fill="url(#pattern0)"/>
<defs>
<pattern id="pattern0" patternContentUnits="objectBoundingBox" width="1" height="1">
<use xlink:href="#image0_762_77" transform="scale(0.0111111)"/>
</pattern>
<image id="image0_762_77" width="70" height="90" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFoAAABaCAYAAAA4qEECAAAACXBIWXMAAAsTAAALEwEAmpwYAAACJklEQVR4nO3dvW4TQRTF8ROKABIvQHjD8FGSNwCJhoKKinegQDxBIAWEl0BCogIHRVR/tNJECijYa2dnfXxyf/2O5x6tZm3P1axUSimllFJKKQmA28AT4CNwxu44a3N+BOzLGfAA+MLuOx1qkfGdnBDyhc+Wd3ZbLtI8lBvghDwf5AZYkGchN4SSG0LJDaHkhlByQyi5IZTcEEpuCCU3hJIbQskNoeSGUHJDKLkhlNwQSm4IpXG13wVetw3e78CLYWuvgp4+6CHkf73rEjahtLruvSW7S9OHTSiNq/3nkiGmDZtQGlf7yxXDTBc2oTS+p2UIs3/YhNL4+veBtyuGew/cqaCvsObN1j9sQmn9HPqGTShtlkW/sAmlDXULm1C6hi5hM6/fwFPg4DpBGNU1/qsf8zrqHfAW6nruNqHB/e4Jz1/XN7cJMceSsYW6vrpNKHXpeOY2oYuH4VE9DIPohn+9m41VyBX03+on+Aa0pvpTaUNWIbcPiSSnkG960NRW1mxBv1oxTG3OrjIi5FvAryVDVLvBhEGf/+fyaqCZeOl4c8Wl1RLWIeh7Lezz1h42NNRUk+PUQV8KfE+9EUpuCCU3hJIbQskNoeSGUHJDKLkhlNwQSm4IJTeEkhtCyQ2h5IZQchN6COwPuWnHtqc5lhvgMXkO5ab1Ngxn46f4ZHn0/KWXKZyGhHwgZ601anjFxvGOPSAXbc6HtndyKaWUUkoppWhL/gA8W92XIF47ywAAAABJRU5ErkJggg=="/>
</defs>
</svg>

</button>

</nuxt-link>
</div>

</div>
<nuxt/>
</div>
<div class="header-line"></div>
</template>

<style scoped>
.Header{
overflow: hidden;
display: flex;
align-items: center;
justify-content: center;
/* width:100%; */
}
.paragraph{
  margin-right: 320px;
  font-weight: bolder;
}
.Header img {
  width: 70px; 
  height: 60px; 
  padding-left: 30px;
}
ul{
  display: flex;
  gap: 40px;
}
.header-line {
  border-bottom: 3px solid #8db600;
  width: 100%;
}
.topnav{
gap: 2%;
}
.back-button {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: transparent;
  border: none;
  padding-left: 10px;
  cursor: pointer;
}

.back-button svg {
  width: 90%;
  height: 80%;
  fill: #43d735;
  background-color: #8db600;
} 
.nav-item{
list-style: none;
text-decoration: none;
color: #000;
font-family: "Open Sans",sans-serif;
font-size: 1.2rem;
font-style: normal;
font-weight: bold;
line-height: normal; 
margin-right: 15px;
}

.chatbot-report {
  display: flex; /* Make it flex */
  /* align-items: center; */
}

.chatbot-report:hover {
  background-color: #8db600;
  border-radius: 3px;
  color: hsl(0, 0%, 100%);
}
.nav{
  margin-right: 350px;
  display:flex ;
  align-items: center;
}
.nav-item:hover {
  background-color: #8db600;
  border-radius: 3px;
  color: hsl(0, 0%, 100%); /* Change this to the desired hover color */
}
@media screen and (max-width: 320px) {
  .Header {
    flex-direction: column;
    text-align: center;
    align-items: center;
  }

  .paragraph {
    margin-left: 10px;
    font-size: 1px;
    font-weight: bolder;
  }

  .Header img {
    width: 90px;
    height: 50px;
    padding-left: 0;
  }

  ul {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 3px;
    padding-left: 10px;
  }
  .nav-item {
    font-size: 2px;
    margin: 5px 0;
    font-weight: bolder;
  }

  .back-button {
    width: fit-content;
    margin-right: 30%;
    padding-right: 10px;
    font-weight: bolder;
    font-size:1px;
  }

  .nav {
    margin-right: 50%;
  }
}


@media screen and (max-width: 850px) {
  .Header {
    flex-direction: column;
    text-align: center;
    align-items: center;
  }

  .paragraph {
    margin-left: 50px;
    font-size: 1.5rem;
    font-weight: bolder;
  }

  .Header img {
    width: 120px;
    height: 32px;
    padding-left: 0;
  }

  ul {
    /* display: flex; */
    flex-direction: row; 
    align-items: center; 
    gap: 15px;
    padding-left: 375px;
  }
  .topnav {
    gap: 1px;
  }

}

@media screen and (max-width: 480px) {
  .Header img {
    width: 80px;
    /* height: 50px;
    padding-left: 0; */
  }
  .nav-item {
    font-size: 1.7rem;
    margin: 5px 0;
    /* font-weight: bolder; */
  }

}

@media screen and (max-width: 1280px) {
  .nav-item{
    width: 100%;
    margin: 5px auto;
  }

  .paragraph {
    margin-right: 50px;
    font-weight: bolder;
    font-size: 1rem;
  }
}
</style><script>
export default {
data() {
  return {
    deferredPrompt: true,
  };
},
mounted() {
  window.addEventListener('beforeinstallprompt', (event) => {
    event.preventDefault();
    this.deferredPrompt = event;
  });
},
methods: {
  installApp() {
    if (this.deferredPrompt) {
      this.deferredPrompt.prompt();
      this.deferredPrompt.userChoice.then((choiceResult) => {
        if (choiceResult.outcome === 'accepted') {
          console.log('User accepted the install prompt');
        }
        this.deferredPrompt = false;
      });
    }
  },
},
};
</script>