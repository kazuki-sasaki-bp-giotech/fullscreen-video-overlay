<template>
  <div class="video-container" ref="container">
    <!-- 動画プレイヤー -->
    <video
      ref="videoElement"
      class="video-player"
      controls
      :src="videoSrc"
    ></video>

    <!-- オーバーレイ (中央の赤い四角) -->
    <div class="overlay">オーバーレイ要素</div>

    <!-- フルスクリーンボタン -->
    <button class="fullscreen-button" @click="toggleFullscreen">
      フルスクリーン切替
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

// 動画ソース
const videoSrc: string = '/video/sample.mp4'; // 動画ファイルのパス

// コンテナと動画要素の参照
const container = ref<HTMLDivElement | null>(null);
const videoElement = ref<HTMLVideoElement | null>(null);

// フルスクリーン切替
const toggleFullscreen = () => {
  if (!container.value) return;

  if (!document.fullscreenElement) {
    container.value.requestFullscreen();
  } else {
    document.exitFullscreen();
  }
};
</script>

<style scoped>
.video-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: auto;
}

.video-player {
  width: 100%;
  display: block;
}

/* オーバーレイ用の赤い四角 */
.overlay {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100px;
  height: 100px;
  background-color: red;
  transform: translate(-50%, -50%);
  pointer-events: none; /* クリックを無効化して動画操作を邪魔しない */
}

/* フルスクリーンボタン */
.fullscreen-button {
  position: absolute;
  bottom: 10px;
  right: 10px;
  padding: 10px 20px;
  background-color: black;
  color: white;
  border: none;
  cursor: pointer;
  z-index: 10; /* オーバーレイや動画の上に表示 */
}
</style>