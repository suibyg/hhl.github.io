<template>
  <view class="qrcode-container">
    <image :src="qrCodeUrl" mode="aspectFit" style="width: 200px; height: 200px;"></image>
    <button @click="generateQrCode">重新生成二维码</button>
  </view>
</template>

<script>
import QRCode from 'qrcode';

export default {
  data() {
    return {
      qrCodeUrl: '' // 用于存储生成的二维码图片路径
    };
  },
  mounted() {
    this.generateQrCode();
  },
  methods: {
    async generateQrCode() {
     try {
       // 生成二维码的 Base64 编码字符串
       const url = await QRCode.toDataURL('http://localhost:5173/#/', {
         width: 200,
         height: 200,
         color: {
           dark: '#000000', // 模块颜色
           light: '#ffffff' // 背景颜色
         }
       });
       this.qrCodeUrl = url;
     } catch (error) {
       console.error('Failed to create QR code:', error);
     }
   }
  }
};
</script>

<style>
.qrcode-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50rpx;
}
</style>