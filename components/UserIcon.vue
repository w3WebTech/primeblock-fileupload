<template>
  <div class="container">
    <!-- Existing icons -->
    <div class="demo-section">
      <!-- Fourth New Icon -->
      <div class="icon-container" ref="interactiveIcon4" @click="animateInteractiveIcon4">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
          <g fill="#fff" stroke="#2f449d" stroke-dasharray="28" stroke-dashoffset="28" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
            <path d="M4 21v-1c0 -3.31 2.69 -6 6 -6h4c3.31 0 6 2.69 6 6v1">
              <animate fill="freeze" attributeName="stroke-dashoffset" dur="0.4s" values="28;0"/>
            </path>
            <path d="M12 11c-2.21 0 -4 -1.79 -4 -4c0 -2.21 1.79 -4 4 -4c2.21 0 4 1.79 4 4c0 2.21 -1.79 4 -4 4Z">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.4s" dur="0.4s" values="28;0"/>
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
    animateInteractiveIcon4() {
      const interactiveIcon4 = this.$refs.interactiveIcon4.querySelector('svg');
      const newIcon4 = interactiveIcon4.cloneNode(true);
      const paths = newIcon4.querySelectorAll('path');

      // Reset path animation settings
      paths[0].setAttribute('stroke-dashoffset', '28');
      paths[1].setAttribute('stroke-dashoffset', '28');

      // Path stroke-dashoffset animation for the first path
      const strokeAnimation1 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation1.setAttribute('fill', 'freeze');
      strokeAnimation1.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation1.setAttribute('begin', '0s');
      strokeAnimation1.setAttribute('dur', '0.4s');
      strokeAnimation1.setAttribute('values', '28;0');

      paths[0].appendChild(strokeAnimation1);

      // Path stroke-dashoffset animation for the second path
      const strokeAnimation2 = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
      strokeAnimation2.setAttribute('fill', 'freeze');
      strokeAnimation2.setAttribute('attributeName', 'stroke-dashoffset');
      strokeAnimation2.setAttribute('begin', '0.4s');
      strokeAnimation2.setAttribute('dur', '0.4s');
      strokeAnimation2.setAttribute('values', '28;0');

      paths[1].appendChild(strokeAnimation2);

      // Replace the old icon with the new animated one
      interactiveIcon4.parentNode.replaceChild(newIcon4, interactiveIcon4);
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
