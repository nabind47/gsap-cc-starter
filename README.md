```sh
npm i gsap @gsap/react
```

```tsx
useGSAP(() => {
  gsap.to("#id", {
    x: 250,
    repeat: -1,
    yoyo: true,
    rotation: 360,
    duration: 2,
    ease: "elastic",
  });
}, []);
```

```tsx
useGSAP(() => {
  gsap.from("#id", {
    x: 250,
    repeat: -1,
    yoyo: true,
    rotation: 360,
    duration: 2,
    ease: "power1.inOut",
  });
}, []);
```

```tsx
useGSAP(() => {
  gsap.fromTo(
    "#id",
    {
      x: 0,
      rotation: 0,
      borderRadius: "0%",
    },

    {
      x: 250,
      rotation: 360,
      borderRadius: "100%",
      repeat: -1,
      yoyo: true,
      duration: 2,
      ease: "bounce.out",
    }
  );
}, []);
```

## Timeline

```tsx
const timeline = gsap.timeline({
  repeat: -1,
  repeatDelay: 1,
  yoyo: true,
});

useGSAP(() => {
  timeline.to("#yellow-box", {
    x: 250,
    rotation: 360,
    borderRadius: "100%",
    duration: 2,
    ease: "back.inOut",
  });

  timeline.to("#yellow-box", {
    y: 150,
    scale: 2,
    rotation: 360,
    borderRadius: "100%",
    duration: 2,
    ease: "back.in",
  });

  timeline.to("#yellow-box", {
    x: 500,
    scale: 1,
    rotation: 360,
    borderRadius: "8px",
    duration: 2,
    ease: "elastic.inOut",
  });
}, []);
```

```tsx
<button
  onClick={() => {
    if (timeline.paused()) {
      timeline.play();
    } else {
      timeline.pause();
    }
  }}
>
  Play/Pause
</button>
```

## Staggers

```tsx
useGSAP(() => {
  gsap.to(".stagger-box", {
    y: 250,
    rotation: 360,
    borderRadius: "100%",
    repeat: -1,
    yoyo: true,
    stagger: {
      amount: 1.5,
      grid: [2, 1],
      axis: "y",
      ease: "circ.inOut",
      from: "center",
    },
  });
}, []);
```

## ScrollTrigger

```tsx
import { useGSAP } from "@gsap/react";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/all";

gsap.registerPlugin(ScrollTrigger);
```

```tsx
const scrollRef = useRef();

useGSAP(
  () => {
    const boxes = gsap.utils.toArray(scrollRef.current.children);
    boxes.forEach((box) => {
      gsap.to(box, {
        x: 150 * boxes.indexOf(box),
        rotation: 360,
        borderRadius: "100%",
        scale: 1.5,
        scrollTrigger: {
          trigger: box,
          start: "bottom bottom",
          end: "top 20%",
          scrub: true,
        },
        ease: "power1.inOut",
      });
    });
  },
  { scope: scrollRef }
);
```

## Animating Text

```tsx
useGSAP(() => {
  gsap.to("#text", {
    ease: "power1.inOut",
    opacity: "1",
    y: 0,
  });

  gsap.fromTo(
    ".para",
    {
      opacity: 0,
      y: 20,
    },
    { opacity: 1, y: 0, delay: 1, stagger: 0.1 }
  );
}, []);
```
