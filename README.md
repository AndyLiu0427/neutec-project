Github page: https://andyliu0427.github.io/neutec-project/

1. 請使用兩種以上的動畫執行方式，來繪製動畫<br>
   使用 window.requestAnimationFrame() 或 GSAP<br>
   window.requestAnimationFrame() 透過 timestamp 計算 transform: translateX 移動動畫<br>
   GSAP 可直接輸入變數控制動畫，如： <br>
   gsap.to(ballElement, { <br>
    duration: 2,<br>
    x: 150,<br>
    ease: 'bounce.out',<br>
  });<br>

   
