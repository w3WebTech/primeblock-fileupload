<template>
    <div class="container">
      <div class="demo-section">
        <div class="icon-container" ref="interactiveIcon" @mouseenter="animateInteractiveIcon" @click="animateInteractiveIcon">
         
          <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" class="chat-icon">
            <mask id="chatMask3">
              <g fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
                <path fill="#fff" fill-opacity="0" stroke-dasharray="72" stroke-dashoffset="0" d="M3 19.5v-15.5c0 -0.55 0.45 -1 1 -1h16c0.55 0 1 0.45 1 1v12c0 0.55 -0.45 1 -1 1h-14.5Z"></path>
                <path stroke="#000" stroke-dasharray="10" stroke-dashoffset="0" d="M8 7h8"></path>
                <path stroke="#000" stroke-dasharray="10" stroke-dashoffset="0" d="M8 10h8"></path>
                <path stroke="#000" stroke-dasharray="6" stroke-dashoffset="0" d="M8 13h4"></path>
              </g>
            </mask>
            <rect width="24" height="24" fill="currentColor" mask="url(#chatMask3)"/>
          </svg>
        </div>
  
        <!-- <div class="icon-container" ref="interactiveIcon2" @mouseenter="animateInteractiveIcon2" @click="animateInteractiveIcon2">
          
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
            <path fill="currentColor" fill-opacity="0" d="M5 8.5l7 -5.5l7 5.5v12.5h-4v-8l-1 -1h-4l-1 1v8h-4v-12.5Z">
              <animate fill="freeze" attributeName="fill-opacity" begin="1.1s" dur="0.15s" values="0;0.3"/>
            </path>
            <g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
              <path stroke-dasharray="16" stroke-dashoffset="16" d="M4.5 21.5h15">
                <animate fill="freeze" attributeName="stroke-dashoffset" dur="0.2s" values="16;0"/>
              </path>
              <path stroke-dasharray="16" stroke-dashoffset="16" d="M4.5 21.5v-13.5M19.5 21.5v-13.5">
                <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.2s" dur="0.2s" values="16;0"/>
              </path>
              <path stroke-dasharray="28" stroke-dashoffset="28" d="M2 10l10 -8l10 8">
                <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.4s" dur="0.4s" values="28;0"/>
              </path>
              <path stroke-dasharray="24" stroke-dashoffset="24" d="M9.5 21.5v-9h5v9">
                <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.7s" dur="0.4s" values="24;0"/>
              </path>
            </g>
          </svg>
        </div> -->
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
      paths[0].setAttribute('fill-opacity', '0');
      paths[0].setAttribute('stroke-dashoffset', '72');
      paths[1].setAttribute('stroke-dashoffset', '10');
      paths[2].setAttribute('stroke-dashoffset', '10');
      paths[3].setAttribute('stroke-dashoffset', '6');
  
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
  
      for (let i = 1; i < 4; i++) {
        const lineAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
        lineAnimation.setAttribute('fill', 'freeze');
        lineAnimation.setAttribute('attributeName', 'stroke-dashoffset');
        lineAnimation.setAttribute('begin', `${0.66 + (i-1)*0.22}s`);
        lineAnimation.setAttribute('dur', '0.22s');
        lineAnimation.setAttribute('values', i < 3 ? '10;0' : '6;0');
  
        paths[i].appendChild(lineAnimation);
      }
  
      interactiveIcon.parentNode.replaceChild(newIcon, interactiveIcon);
    },

    animateInteractiveIcon2() {
      const interactiveIcon2 = this.$refs.interactiveIcon2.querySelector('svg');
      const newIcon2 = interactiveIcon2.cloneNode(true);
      const paths = newIcon2.querySelectorAll('path');
      
      // Reset path animation settings
      paths[0].setAttribute('fill-opacity', '0');
      paths[0].setAttribute('stroke-dashoffset', '16');
      paths[1].setAttribute('stroke-dashoffset', '16');
      paths[2].setAttribute('stroke-dashoffset', '28');
      paths[3].setAttribute('stroke-dashoffset', '24');
  
      // Path fill-opacity animation
      const fillAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      fillAnimation.setAttribute('fill', 'freeze');
      fillAnimation.setAttribute('attributeName', 'fill-opacity');
      fillAnimation.setAttribute('begin', '1.1s');
      fillAnimation.setAttribute('dur', '0.15s');
      fillAnimation.setAttribute('values', '0;0.3');
  
      paths[0].appendChild(fillAnimation);

      // Path stroke-dashoffset animation
      const strokeAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation.setAttribute('fill', 'freeze');
      strokeAnimation.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation.setAttribute('begin', '0.2s');
      strokeAnimation.setAttribute('dur', '0.2s');
      strokeAnimation.setAttribute('values', '16;0');
  
      paths[1].appendChild(strokeAnimation);

      const strokeAnimation2 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation2.setAttribute('fill', 'freeze');
      strokeAnimation2.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation2.setAttribute('begin', '0.2s');
      strokeAnimation2.setAttribute('dur', '0.2s');
      strokeAnimation2.setAttribute('values', '16;0');
  
      paths[2].appendChild(strokeAnimation2);

      const strokeAnimation3 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation3.setAttribute('fill', 'freeze');
      strokeAnimation3.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation3.setAttribute('begin', '0.4s');
      strokeAnimation3.setAttribute('dur', '0.4s');
      strokeAnimation3.setAttribute('values', '28;0');
  
      paths[3].appendChild(strokeAnimation3);

      interactiveIcon2.parentNode.replaceChild(newIcon2, interactiveIcon2);
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
    width: 32px;
    height: 32px;
    color: #eaf0ed;
}

.icon-container:hover svg {
    color: #fff;
}
</style>

  