<template>
<div class="container">
  <div class="status-field">
    <div class="status-item">Loaded Item : 4</div>
  </div>
  <div class="root" style="width:500px; height:500px; overflow:auto;">
    <div class="item">
    Item 1
  </div>
  <div class="item">
    Item 2
  </div>
  <div class="item">
    Item 3
  </div>
  <div class="item">
    Item 4
  </div>
  <div class="scroll-detecting">
    <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
  </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  mounted() {
   // const container = document.querySelector('.container')
    const root = document.querySelector('.root')
    const detector = document.querySelector('.scroll-detecting')
    let currentIndex = document.querySelectorAll('.item').length + 1

  function update() {
    const statusEL = document.querySelector('.status-item')
    const items = document.querySelectorAll('.item')

    statusEL.innerText = `Loaded Item : ${items.length}`
  }

  function loadItem(count) {
    for (let i = 0; i < count; i++) {
      const div = document.createElement('div')

      div.classList.add('item')
      div.innerText = `Item ${currentIndex++}`
      root.appendChild(div)
      console.log(currentIndex);
    }
    update()
  }

const io = new IntersectionObserver(entries => {
  //console.log('',entries.unob);c
  entries.forEach((item) => {
console.log('intersectionRatio : ',item.intersectionRatio);
    console.log('isIntersecting : ', item.isIntersecting);
  });

  if (entries.some(entry => entry.intersectionRatio > 0)) {
    setTimeout(function(){
      loadItem(10)
      root.appendChild(detector)

    },1000)
  }
},{
  root:document.querySelector('.root'),
  rootMargin: '0px',
  threshold: 0.8
})
  io.observe(detector)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.status-field {
  position: fixed;
  top: 0;
  width: 100%;
}
.status-item {
  text-align: right;
  padding: 1rem;
}
.item {
  padding: 10rem 2rem;
  border-top: 2px solid gray;
}
.scroll-detecting {
  width: 5px;
  height: 5px;
}
.lds-ring {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 51px;
  height: 51px;
  margin: 6px;
  border: 6px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #F86C06 transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
