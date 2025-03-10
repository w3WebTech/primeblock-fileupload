<template>
  <div class="container">
    <!-- Existing icons -->
    <div class="demo-section">
      <!-- New third icon -->
      <div class="icon-container" ref="interactiveIcon3" @click="animateInteractiveIcon3">
        <!-- New SVG with animation -->
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
          <g fill="#fff" stroke="#2f449d" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
            <path stroke-dasharray="72" stroke-dashoffset="72" d="M12 3h7v18h-14v-18h7Z">
              <animate fill="freeze" attributeName="stroke-dashoffset" dur="0.6s" values="72;0"/>
            </path>
            <path stroke-dasharray="12" stroke-dashoffset="12" stroke-width="1" d="M14.5 3.5v3h-5v-3">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.7s" dur="0.2s" values="12;0"/>
            </path>
            <path stroke-dasharray="10" stroke-dashoffset="10" d="M9 13l2 2l4 -4">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.9s" dur="0.2s" values="10;0"/>
            </path>
          </g>
          <path fill="currentColor" fill-opacity="0" d="M6 4H10V6H14V4H18V20H6V4Z">
            <animate fill="freeze" attributeName="fill-opacity" begin="1.2s" dur="0.15s" values="0;0.3"/>
          </path>
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
      // Existing method for the first icon
    },

    animateInteractiveIcon2() {
      // Existing method for the second icon
    },

    animateInteractiveIcon3() {
      const interactiveIcon3 = this.$refs.interactiveIcon3.querySelector('svg');
      const newIcon3 = interactiveIcon3.cloneNode(true);
      const paths = newIcon3.querySelectorAll('path');

      // Reset path animation settings
      paths[0].setAttribute('stroke-dashoffset', '72');
      paths[1].setAttribute('stroke-dashoffset', '12');
      paths[2].setAttribute('stroke-dashoffset', '10');

      // Path stroke-dashoffset animation
      const strokeAnimation1 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation1.setAttribute('fill', 'freeze');
      strokeAnimation1.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation1.setAttribute('begin', '0s');
      strokeAnimation1.setAttribute('dur', '0.6s');
      strokeAnimation1.setAttribute('values', '72;0');

      paths[0].appendChild(strokeAnimation1);

      const strokeAnimation2 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation2.setAttribute('fill', 'freeze');
      strokeAnimation2.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation2.setAttribute('begin', '0.7s');
      strokeAnimation2.setAttribute('dur', '0.2s');
      strokeAnimation2.setAttribute('values', '12;0');

      paths[1].appendChild(strokeAnimation2);

      const strokeAnimation3 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation3.setAttribute('fill', 'freeze');
      strokeAnimation3.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation3.setAttribute('begin', '0.9s');
      strokeAnimation3.setAttribute('dur', '0.2s');
      strokeAnimation3.setAttribute('values', '10;0');

      paths[2].appendChild(strokeAnimation3);

      const fillAnimation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      fillAnimation.setAttribute('fill', 'freeze');
      fillAnimation.setAttribute('attributeName', 'fill-opacity');
      fillAnimation.setAttribute('begin', '1.2s');
      fillAnimation.setAttribute('dur', '0.15s');
      fillAnimation.setAttribute('values', '0;0.3');

      paths[3].appendChild(fillAnimation);

      interactiveIcon3.parentNode.replaceChild(newIcon3, interactiveIcon3);
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
  color: #B29AFD;
}

.icon-container:hover svg {
  color: #B29AFD;
}
</style>
