<template>
  <div class="container">
    <div class="demo-section">
      <div class="icon-container" ref="interactiveIcon" @click="animateInteractiveIcon">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" class="chat-icon">
          <mask id="chatMask3">
            <g fill="#fff" stroke="#2f449d" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
              <path fill="#fff" fill-opacity="0" stroke-dasharray="72" stroke-dashoffset="0" d="M3 19.5v-15.5c0 -0.55 0.45 -1 1 -1h16c0.55 0 1 0.45 1 1v12c0 0.55 -0.45 1 -1 1h-14.5Z"></path>
              <path stroke="#000" stroke-dasharray="10" stroke-dashoffset="0" d="M8 7h8"></path>
              <path stroke="#000" stroke-dasharray="10" stroke-dashoffset="0" d="M8 10h8"></path>
              <path stroke="#000" stroke-dasharray="6" stroke-dashoffset="0" d="M8 13h4"></path>
            </g>
          </mask>
          <rect width="24" height="24" fill="currentColor" mask="url(#chatMask3)"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isVisible: false,
    };
  },
  methods: {
    animateInteractiveIcon() {
      const interactiveIcon = this.$refs.interactiveIcon.querySelector('svg');
      const newIcon = interactiveIcon.cloneNode(true);
      const paths = newIcon.querySelectorAll('path');
      
      // Reset initial state of the paths
      paths[0].setAttribute('fill-opacity', '0');
      paths[0].setAttribute('stroke-dashoffset', '72');
      paths[1].setAttribute('stroke-dashoffset', '10');
      paths[2].setAttribute('stroke-dashoffset', '10');
      paths[3].setAttribute('stroke-dashoffset', '6');
  
      // Path fill-opacity animation
      const fillAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      fillAnimation.setAttribute('fill', 'freeze');
      fillAnimation.setAttribute('attributeName', 'fill-opacity');
      fillAnimation.setAttribute('begin', '0s');
      fillAnimation.setAttribute('dur', '0.55s');
      fillAnimation.setAttribute('values', '0;1');
  
      const strokeAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation.setAttribute('fill', 'freeze');
      strokeAnimation.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation.setAttribute('begin', '0s');
      strokeAnimation.setAttribute('dur', '0.66s');
      strokeAnimation.setAttribute('values', '72;0');
  
      paths[0].appendChild(fillAnimation);
      paths[0].appendChild(strokeAnimation);
  
      // Animations for each line of the icon
      for (let i = 1; i < 4; i++) {
        const lineAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
        lineAnimation.setAttribute('fill', 'freeze');
        lineAnimation.setAttribute('attributeName', 'stroke-dashoffset');
        lineAnimation.setAttribute('begin', `${0.66 + (i-1)*0.22}s`);
        lineAnimation.setAttribute('dur', '0.22s');
        lineAnimation.setAttribute('values', i < 3 ? '10;0' : '6;0');
  
        paths[i].appendChild(lineAnimation);
      }
  
      // Replace the old icon with the new animated one
      interactiveIcon.parentNode.replaceChild(newIcon, interactiveIcon);
    }
  }
};
</script>

<style>
.icon-container {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding-top: 0px;
    padding-bottom: 0px;
    padding: 5px;
    cursor: pointer;
}

.icon-container svg {
    width: 24px;
    height: 24px;
    color: #2f449d;
}

.icon-container:hover svg {
    color: #2f449d;
}
</style>
