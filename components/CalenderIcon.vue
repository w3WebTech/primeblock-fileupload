<template>
  <div class="container">
    <!-- Existing icons -->
    <div class="demo-section">
      <!-- Fifth New Icon -->
      <div class="icon-container " ref="interactiveIcon5" @click="animateInteractiveIcon5">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" class="">
          <g fill="#fff" stroke="#2f449d" stroke-linecap="round" stroke-linejoin="round" stroke-width="2">
            <path stroke-dasharray="64" stroke-dashoffset="64" d="M22 3v14c0 0.55 -0.45 1 -1 1h-14c-0.55 0 -1 -0.45 -1 -1v-14c0 -0.55 0.45 -1 1 -1h14c0.55 0 1 0.45 1 1Z">
              <animate fill="freeze" attributeName="stroke-dashoffset" dur="0.6s" values="64;0"/>
            </path>
            <path stroke-dasharray="10" stroke-dashoffset="10" d="M10 6h8">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.7s" dur="0.2s" values="10;0"/>
            </path>
            <path stroke-dasharray="10" stroke-dashoffset="10" d="M10 10h8">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="0.9s" dur="0.2s" values="10;0"/>
            </path>
            <path stroke-dasharray="6" stroke-dashoffset="6" d="M10 14h5">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="1.1s" dur="0.2s" values="6;0"/>
            </path>
            <path stroke-dasharray="36" stroke-dashoffset="36" d="M2 6v15c0 0.55 0.45 1 1 1h15">
              <animate fill="freeze" attributeName="stroke-dashoffset" begin="1.4s" dur="0.5s" values="36;0"/>
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
    animateInteractiveIcon() {
      // Existing method for the first icon
    },

    animateInteractiveIcon2() {
      // Existing method for the second icon
    },

    animateInteractiveIcon3() {
      // Existing method for the third icon
    },

    animateInteractiveIcon4() {
      // Existing method for the fourth icon
    },

    animateInteractiveIcon5() {
      const interactiveIcon5 = this.$refs.interactiveIcon5.querySelector('svg');
      const newIcon5 = interactiveIcon5.cloneNode(true);
      const paths = newIcon5.querySelectorAll('path');

      // Reset path animation settings
      paths.forEach(path => path.setAttribute('stroke-dashoffset', path.getAttribute('stroke-dasharray')));

      // Add animations for each path in the new icon
      paths.forEach((path, index) => {
        const animation = document.createElementNS('http://www.w3.org/2000/svg', 'animate');
        animation.setAttribute('fill', 'freeze');
        animation.setAttribute('attributeName', 'stroke-dashoffset');
        animation.setAttribute('begin', `${index * 0.2}s`);
        animation.setAttribute('dur', '0.2s');
        animation.setAttribute('values', `${path.getAttribute('stroke-dasharray')};0`);
        path.appendChild(animation);
      });

      interactiveIcon5.parentNode.replaceChild(newIcon5, interactiveIcon5);
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
