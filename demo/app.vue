<template>
   <section class="signaturesec">
      <div class="signatureBox">
         <div class="canvasBox" ref="canvasHW">
            <canvas  @touchstart='touchStart'
                  @touchmove='touchMove'
                  @touchend='touchEnd'
                  ref="canvasF"
                  @mousedown="mouseDown"
                  @mousemove="mouseMove"
                  @mouseup="mouseUp"></canvas>
            <div class="btnBox">
              <button @click="overwrite">重写</button>
              <button @click="commit">提交签名</button>
            </div>   
         </div>
      </div>
   </section>   
</template>

<script>
export default {
  name: 'signature',
  data() {
   return {
     client: {},
     points: [],
     canvasTxt: null,
     startX: 0,
     startY: 0,
     moveY: 0,
     moveX: 0,
     endY: 0,
     endX: 0,
     w: null,
     h: null,
     isDown: false
   }
  },
  created() {},
  mounted() {
    let canvas = this.$refs.canvasF
    console.log(this.$refs.canvasHW.offsetWidth)
    canvas.height = this.$refs.canvasHW.offsetHeight - 160
    canvas.width = this.$refs.canvasHW.offsetWidth - 20
    this.canvasTxt = canvas.getContext('2d')
  },
  methods: {
   //电脑设备事件
   mouseDown(ev) {
     ev = ev || event
     ev.preventDefault()
     console.log(ev)
     if (1) {
      let obj = {
        x: ev.offsetX,
        y: ev.offsetY
      }
      console.log(obj)
      this.startX = obj.x
      this.startY = obj.y
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.points.push(obj)
      this.isDown = true
//       debugger
      this.imgUrl =
        (this.$refs.canvasF && this.$refs.canvasF.toDataURL()) || ''
     }
   },
   //移动设备事件
   touchStart(ev) {
     ev = ev || event
     ev.preventDefault()
      console.log(ev)
     if (ev.touches.length == 1) {
      let obj = {
        x: ev.targetTouches[0].clientX,
        y: ev.targetTouches[0].clientY - 48
      }
      console.log(obj)
      this.startX = obj.x
      this.startY = obj.y
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.points.push(obj)
     }
   },
   //电脑设备事件
   mouseMove(ev) {
     ev = ev || event
     ev.preventDefault()
     if (this.isDown) {
      let obj = {
        x: ev.offsetX,
        y: ev.offsetY
      }
      this.moveY = obj.y
      this.moveX = obj.x
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.strokeStyle = "#FFAA25"
      this.canvasTxt.lineWidth = 3
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.startY = obj.y
      this.startX = obj.x
      this.points.push(obj)
     }
   },
   //移动设备事件
   touchMove(ev) {
     ev = ev || event
     ev.preventDefault()
     if (ev.touches.length == 1) {
      let obj = {
        x: ev.targetTouches[0].clientX,
        y: ev.targetTouches[0].clientY - 48
      }
      this.moveY = obj.y
      this.moveX = obj.x
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.strokeStyle = "#FFAA25"
      this.canvasTxt.lineWidth = 5
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.startY = obj.y
      this.startX = obj.x
      this.points.push(obj)
     }
   },
   //电脑设备事件
   mouseUp(ev) {
     ev = ev || event
     ev.preventDefault()
     if (1) {
      let obj = {
        x: ev.offsetX,
        y: ev.offsetY
      }
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.points.push(obj)
      this.points.push({x: -1, y: -1})
      this.isDown = false
     }
   },
   //移动设备事件
   touchEnd(ev) {
     ev = ev || event
     ev.preventDefault()
     if (ev.touches.length == 1) {
      let obj = {
        x: ev.targetTouches[0].clientX,
        y: ev.targetTouches[0].clientY - 48
      }
      this.canvasTxt.beginPath()
      this.canvasTxt.moveTo(this.startX, this.startY)
      this.canvasTxt.lineTo(obj.x, obj.y)
      this.canvasTxt.stroke()
      this.canvasTxt.closePath()
      this.points.push(obj)
      this.points.push({x: -1, y: -1})
      debugger
      this.imgUrl =
        (this.$refs.canvasF && this.$refs.canvasF.toDataURL()) || ''
     }
   },
   //重写
   overwrite() {
     this.canvasTxt.clearRect(
      0,
      0,
      this.$refs.canvasF.width,
      this.$refs.canvasF.height
     )
     this.points = []
   },
   //提交签名
   commit() {

     console.log(this.$refs.canvasF.toDataURL()) //签名
   }
  }
}
</script>

<style>
.signatureBox{
  top: 50px;
  left: 0px;
  width: 100%;
  height: 80vh;
  box-sizing: border-box;
  overflow: hidden;
  background: #fff;
  z-index: 100;
  display: flex;
  flex-direction: column;
}
.visaDetailTop {
  width: 100%;
  padding: 5px;
  box-sizing: border-box;
  z-index: 2;
}
.visaDetailTop p {
  margin: 0px;
  text-align: center;
  color: #000;
  font-size: 1em;
  position: relative;
}
p.visaTitle {
  width: 100%;
  position: absolute;
  top: 5px;
  left: 0px;
  text-align: center;
  font-size: 1.2em;
}
.btnBack {
  display: block;
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  z-index: 1;
  background: transparent;
  border-color: transparent;
  outline: none;
}
.btnDaoHang {
  display: block;
  position: absolute;
  left: 0px;
  top: 0px;
  height: 2.2em;
  width: 2em;
  z-index: 1;
  background: transparent;
  border-color: transparent;
  outline: none;
}
.visaDetailTop p span {
  color: #fff;
  font-size: 1.2em;
}
.visaDetailTop p:first-of-type {
  float: left;
}
.visaDetailTop p:nth-of-type(2) {
  float: right;
}
.canvasBox {
  padding: 10px 5px;
  box-sizing: border-box;
  flex: 1;
}
canvas {
  border: 1px solid #e3e3e3;
}
.btnBox {
  padding: 5px;
  text-align: right;
}
.btnBox button:first-of-type {
  background: transparent;
  border-radius: 4px;
  height: 40px;
  width: 80px;
  font-size: 14px;
}
.btnBox button:last-of-type {
  background: #71b900;
  color: #fff;
  border-radius: 4px;
  height: 40px;
  width: 80px;
  font-size: 14px;
}
@media only screen and (min-width: 750px) {
  .signatureBox {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    min-height: 100%;
    box-sizing: border-box;
    overflow: visible;
  }
}
</style>