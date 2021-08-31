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
  <div class="scroll-detecting"></div>
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
    loadItem(10)
    root.appendChild(detector)
  }
},{
  root:document.querySelector('.root'),
  rootMargin: '0px',
  threshold: 0.1
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
</style>
