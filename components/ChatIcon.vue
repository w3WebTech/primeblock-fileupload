<template>
  <div class="container">
    <div class="demo-section">
      <div class="icon-container" ref="interactiveIcon2" @click="animateInteractiveIcon2">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
          <path fill="currentColor" fill-opacity="0" d="M5 8.5l7 -5.5l7 5.5v12.5h-4v-8l-1 -1h-4l-1 1v8h-4v-12.5Z">
            <animate fill="freeze" attributeName="fill-opacity" begin="1.1s" dur="0.15s" values="0;0.3"/>
          </path>
          <g fill="#fff" stroke="#2f449d" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
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
    animateInteractiveIcon2() {
      const interactiveIcon2 = this.$refs.interactiveIcon2.querySelector('svg');
      const newIcon2 = interactiveIcon2.cloneNode(true);
      const paths = newIcon2.querySelectorAll('path');
      
      paths[0].setAttribute('fill-opacity', '0');
      paths[0].setAttribute('stroke-dashoffset', '16');
      paths[1].setAttribute('stroke-dashoffset', '16');
      paths[2].setAttribute('stroke-dashoffset', '28');
      paths[3].setAttribute('stroke-dashoffset', '24');
  
      const fillAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      fillAnimation.setAttribute('fill', 'freeze');
      fillAnimation.setAttribute('attributeName', 'fill-opacity');
      fillAnimation.setAttribute('begin', '1.1s');
      fillAnimation.setAttribute('dur', '0.15s');
      fillAnimation.setAttribute('values', '0;0.3');
  
      paths[0].appendChild(fillAnimation);

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
  width: 24px;
  height: 24px;
  color: #eaf0ed;
}

.icon-container:hover svg {
  color: #fff;
}
</style>
