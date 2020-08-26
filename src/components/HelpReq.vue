<template>
  <div>
    <h2>Required settings</h2>
    <div id="contents">
      <h3>1. laptop setting</h3>
      <p>pcを充電状態、または十分な充電残量にすること。</p>
      <h3>2. zoom setting</h3>
      <p>デフォルトのブラウザをchromeに設定。一度zoomリンクをchromeで開き、「このタイプのリンクは常に関連づけられたアプリで開く」にチェック。</p>
      <img src="img/zoom.jpg" alt="zoom" />
      <h3>3. audio setting</h3>
      <p>zoomアプリケーションの「設定/オーディオ」から、「会議に参加する時にオーディオをコンピュータで作動させる」にチェック。</p>
      <img src="img/audio.png" alt="audio" />
      <h3>4. sleep setting</h3>
      <p>「システム環境設定/省エネルギー」で、ディスプレイのスリープを「しない」もしくは授業開始よりも長い時間に設定。（ディスプレイをスリープ状態にしないと、ディスプレイの寿命が短くなる場合があります。）</p>
      <img src="img/sleep.png" alt="sleep" />
      <h3>5. screen setting</h3>
      <p>「システム環境設定/デスクトップとスクリーンセーバ」で、開始までの時間を「開始しない」に設定。</p>
      <img src="img/screen.png" alt="screen" />

      <p>
        その他不具合等ありましたら
        <a href="mailto:info@aratius.site">こちら</a>まで。
      </p>
      <h3>免責事項</h3>
      <p>
        当コンテンツは、製作者が夏休みの片手間に制作したものであり、
        絶対的な機能性を保証するものではありません。
        ご利用いただく際は必ず試験的利用を経て、
        <span
          class="bold"
        >ご自身の責任の範囲内で</span>ご利用ください。
        <br />また製作者といたしましては、寝坊時の保険としての利用を想定しておりますので、
        ご自身で起きて授業に参加されるに越したことはないと考えております。
      </p>
    </div>
  </div>
</template>
<script>
export default {};
</script>

<style scoped>
#contents {
  width: 90%;
  max-width: 600px;
  margin: auto;
}
img {
  width: 100%;
  border: 2px solid black;
}
.bold {
  font-weight: bold;
}
</style>
