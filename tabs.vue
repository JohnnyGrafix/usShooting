<template>
  <div>
    <nav>
      <ul>
        <li v-for="item,i in items" v-on:click="switchItem(i)" :class="{active: i==current}" :style="{backgroundColor: item.props.color}">
        {{ item.props.name }}
        </li>
      </ul>
    </nav>
    <main>
      
      <h3>{{ currentItem.props.title }}</h3>
      <h4>{{ currentItem.props.date }}</h4>
      <h2 id="toll">{{ currentItem.props.toll }}</h2>
      <img :src="currentImage" />
	  <p> {{ currentItem.props.description }}</p>


    </main>
    
  </div> 
</template>

<script>
  module.exports = {
    data() {
      return {
        current: 0,
        size: null
      }
    },
    props: ['items'],
    computed: {
      currentItem() {
        return this.items[this.current]
      },
      currentImageSize() {
        return 'image'
      },
      currentImage() {
        return 'assets/' + this.currentItem[this.currentImageSize]
      }
    },
    mounted() {
      this.resize()
      window.onresize = this.resize
    },
    methods: {
      resize() {
        this.size = this.$el.getBoundingClientRect()
      },
      switchItem(i) {
        this.current = i
      }
    }
  }
</script>