<template>
  <transition :name="transitionName">
    <div class="back-to-ceiling totop" @click="backToTop" v-show="visible" :style="customStyle">
     <div class="totop"></div>
    </div>
  </transition>
</template>

<script>
  export default {
    name: 'BackToTop',
    props: {
      visibilityHeight: {
        type: Number,
        default: function () {
          return 400
        }
      },
      backPosition: {
        type: Number,
        default:function() {
          return 0
        }
      },
      customStyle: {
        type: Object,
        default:function () {
          return {
            right: '20px',
            bottom: '50px',
//            width: '40px',
//            height: '40px',
//            'border-radius': '4px',
//            'line-height': '45px',
//            background: '#e7eaf1'
          }
        }
      },
      transitionName: {
        type: String,
        default:function () {
          return 'fade'
        }
      }
    },
    data() {
      return {
        visible: false,
        interval: null
      }
    },
    mounted() {
      window.addEventListener('scroll', this.handleScroll)
    },
    beforeDestroy() {
      window.removeEventListener('scroll', this.handleScroll)
      if (this.interval) {
        clearInterval(this.interval)
      }
    },
    methods: {
      handleScroll() {
        this.visible = window.pageYOffset > this.visibilityHeight
      },
      backToTop() {
        const start = window.pageYOffset
        let i = 0
        this.interval = setInterval(() => {
          const next = Math.floor(this.easeInOutQuad(10 * i, start, -start, 500))
          if (next <= this.backPosition) {
            window.scrollTo(0, this.backPosition)
            clearInterval(this.interval)
          } else {
            window.scrollTo(0, next)
          }
          i++
        }, 16.7)
      },
      easeInOutQuad(t, b, c, d) {
        if ((t /= d / 2) < 1) return c / 2 * t * t + b
        return -c / 2 * (--t * (t - 2) - 1) + b
      }
    }
  }
</script>

<style scoped>
  .back-to-ceiling {
    position: fixed;
    display: inline-block;
    text-align: center;
    cursor: pointer;
    border-radius: 50%!important;
  }

  .back-to-ceiling:hover {
    background: #d5dbe7;
  }
  .totop{
    width: 88px;
    height: 88px;
    background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFgAAABYCAMAAABGS8AGAAAAz1BMVEX///8AAAD09PTi4uL5+fnm5uZubm7o6Oj8/Pzr6+v29vbl5eW1tbXu7u7GxsaIiIjLy8txcXGNjY2dnZ2np6d2dnbY2Njn5+fm5ubj4+N7e3tqamqsrKyEhITU1NT///9zc3Ozs7PQ0NDx8fHq6uq4uLi9vb3c3Nzk5OTj4+Pm5ubl5eXl5eXl5eXm5ubm5ubm5ubm5ubm5ubn5+fm5ubm5ubo6Ojo6Ojr6+vi4uLh4eGXl5eVlZXi4uL///9+fn6RkZGjo6OhoaGwsLBmZmYhzvD5AAAARHRSTlPmAOfm5+j95+bn59/x5+/57f349fT87I5nLPv+8/rsBfzy7efn8fDr5t3U0dDPybq3pZqUh3JjWTEjIfb26gT69/T18gVaONUAAAPwSURBVFjD7dlZV+IwGMbxZ5qUpq0FRFnKToHBBXfFBUYY7ff/TBNSNSPYJMDpGS/mf6E3+jsRqyRv8ENfOLm5HB8T0fH48mYSGnyTDn64PSe227cog4hRq+/a5Pz2YRf4serbgYcv8gLbrz5uCddOScCQGgvIaW1zuHPnOx40eY5/19kMrvkDCoPowK9tAIdnjmR1tHMWGsLP18TCBlnk+tkEfjpxsWHuyZMevlcsV7Hoex1cPaLYInpUVcNXNrbMvlLAnQsHW+dcdFLhCxd/12zEqhqHn2X3Ig2+WllvLlbXWF3z1ddw1Qa2WbHMrn4F3x9h547u1+EnQqHOGlZ0MCVPq/DziQV1bjmOf+pk6+R5Bb52dW49jg1k9/ozHBKD9RrJJPwEn1l610y2zv6Ga47ebfDHumUgOzUJd3yqdyMOBwUuD9Uw9Tsf8N0AqgZLtw0OW56BPLj7gNULdhJXwDCQqf8O1xwTN4ETeU/7Kgv41NO7HzCoVvZOE/iRqNyucCVsIpNHAVcDpGZzN1eBhD/kngIOqgL2mZErYdCSWmb+En6w9a6EzWT7gcO3QepPJF0JS1nx1AW3HD73kFJPuqswGJfLqbB3zmGCtEb75TdXwlKexYdIjfxAaCM1BqzBMor07BATF/okbJg7wU0/C7h/g0srC9i6xJhmAdMxjlkWMDsGQRYwyH/4W8HdOKbm8AaPWy/3Gxs8bmOKDKLj5Z90BlmXy39CGdS/wcRFBrkThDYyyA6Xb00ZRBRvprvkncu3f9NYkUFbcKvYsLSLIq/4XhuieVF8KuaXuWkbFsUWa1oodMuFglPg5eb8wwEwqFQqL6UKD/ul6XTaiBRbLMWm8GAPSeURRMPWWwXs20CQo6pN4SPRwUz+W+uDR9sQ8M+ZYhsrNt4qeFiv1+M6b/lV7TnAwVICl/KKjbc4Kqjg5vSXKFn1vAKgnqy4n6OqowLPpyr4kC8xABI4PwOiFgQ8nCkPN+I4poHrowSeLkqNxaJcXyw8Ds9edcexjk/N4GL+PcZhpxsoD5DyVdbCMvHLGy5SXmHNIV3CXfsN/nmYxASMLlEc0kUhUcE0Zm9wadbjvcZWAh/01GMFMQhRwJU6BPz+5LJ3uHmgGYTI0c063I4wa8LCHluDWWtPPbqRw6Z1mBftW6Myd1bg3jxX8DTDJjkeW4fZ634E5MsjAU/3eD0BB6NgfTxmMND7FUX1PNxmt+WA1+62l3DpN+9FwFjLrpqMIIulUpMiOhghKXoBcBiBx1oe5s6a61wphqY75F5kNubNaDCd7Sg9++F/9tcVss4WFywZXQn9+0usja7dvstFodHV5ve7jN3l+vgPliKdSBMcpI8AAAAASUVORK5CYII=) 50% no-repeat;
    background-size: contain;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter,
  .fade-leave-to {
    opacity: 0
  }

  .back-to-ceiling .Icon {
    fill: #9aaabf;
    background: none;
  }
</style>


