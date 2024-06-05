<template>
  <div class="container-xxl bd-gutter mt-3 my-md-4 bd-layout">
    <h2>Genshin Impact Party Builder</h2>
    <p>I hate vue.js, react is better! but I bet you like vue more...</p>

    <div class="container text-center">
      <div class="row">
        <div class="col" id="div1" @drop.prevent="dropHandler('div1')" @dragover.prevent="allowDrop"></div>
        <div class="col" id="div2" @drop.prevent="dropHandler('div2')" @dragover.prevent="allowDrop"></div>
        <div class="col" id="div3" @drop.prevent="dropHandler('div3')" @dragover.prevent="allowDrop"></div>
        <div class="col" id="div4" @drop.prevent="dropHandler('div4')" @dragover.prevent="allowDrop"></div>
      </div>
    </div>

    <div id="teamSelect" @drop.prevent="dropHandler('teamSelect')" @dragover.prevent="allowDrop">
      <img v-for="user in users" :key="user.id" :src="user.imageUrl" draggable="true" @dragstart="dragStartHandler(user.id)" :id="user.id" :alt="`${user.name} Character Avatar`">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        { name: 'Kokomi', imageUrl: require('@/assets/ui-avataricon-kokomi.png'), id: 'drag1' },
        { name: 'Yae', imageUrl: require('@/assets/ui-avataricon-yae.png'), id: 'drag2' },
        { name: 'Nahida', imageUrl: require('@/assets/ui-avataricon-nahida.png'), id: 'drag3' },
        { name: 'Neuvillette', imageUrl: require('@/assets/ui-avataricon-neuvillette.png'), id: 'drag4' },
        { name: 'HuTao', imageUrl: require('@/assets/ui-avataricon-hutao.png'), id: 'drag5' },
        { name: 'zhongli', imageUrl: require('@/assets/ui-avataricon-zhongli.png'), id: 'drag6' },
        { name: 'shougun', imageUrl: require('@/assets/ui-avataricon-shougun.png'), id: 'drag7' },
        { name: 'ganyu', imageUrl: require('@/assets/ui-avataricon-ganyu.png'), id: 'drag8' },
        { name: 'furina', imageUrl: require('@/assets/ui-avataricon-furina.png'), id: 'drag9' },
        { name: 'kazuha', imageUrl: require('@/assets/ui-avataricon-kazuha.png'), id: 'drag10' },
        { name: 'ayaka', imageUrl: require('@/assets/ui-avataricon-ayaka.png'), id: 'drag11' }
        // Add other user objects here...
      ]
    };
  },
  methods: {
    allowDrop(ev) {
      ev.preventDefault();
    },
    dragStartHandler(id) {
      event.dataTransfer.setData("text", id);
    },
    dropHandler(targetId) {
      event.preventDefault();
      const data = event.dataTransfer.getData("text");
      const draggedElement = document.getElementById(data);
      const target = document.getElementById(targetId);

      if (draggedElement && target) {
        if (target.id === "teamSelect" || target.tagName === "IMG") {
          if (target.tagName === "IMG" && target.previousElementSibling) {
            target.parentNode.insertBefore(draggedElement, target);
          } else {
            target.appendChild(draggedElement);
          }
        } else if (target.children.length === 0) {
          target.appendChild(draggedElement);
        }
      }
    }
  }
}
</script>

<style>
@import '~bootstrap/dist/css/bootstrap.min.css';
</style>

<style>
/* Add your CSS styles here */
#div1, #div2, #div3, #div4 {
  width: 200px;
  height: 200px;
  border: 1px solid black;
  border-right: none;
}

#div4 {
  border-right: 1px solid black;
}

#div1, #div2, #div3, #div4 {
  display: inline-block;
  vertical-align: middle; /* Aligns the image vertically in the middle */
}

#div1 img, #div2 img, #div3 img, #div4 img {
  max-height: 100%;
  max-width: 100%;
}

#teamSelect {
  background-color: #8a8a8a;
}

#teamSelect img {
  max-width: 100px;
}

</style>
