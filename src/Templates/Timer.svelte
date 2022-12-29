<!-- https://eugenkiss.github.io/7guis/tasks#timer -->
<script>
  let waiting = 0;

  const notifyLoaded = () => {
    console.log("loaded!");
  };

  const onload = (el) => {
    waiting++;
    el.addEventListener("load", () => {
      waiting--;
      if (waiting === 0) {
        notifyLoaded();
      }
    });
  };
  import { onDestroy } from "svelte";
  import { beforeUpdate, afterUpdate } from "svelte";
  export let count;
  let elapsed = 0;
  export let duration = 700000;

  let last_time = window.performance.now();
  let frame;

  (function update() {
    frame = requestAnimationFrame(update);

    const time = window.performance.now();
    elapsed += Math.min(time - last_time, duration - elapsed);

    last_time = time;
  })();
  afterUpdate(() => {
    if (duration == elapsed) {
      count += 1;
      elapsed = 0;
    }
  });
  onDestroy(() => {
    cancelAnimationFrame(frame);
  });
</script>

<label>
  <progress value={elapsed / duration} />
</label>
<!--
<div>{(elapsed / 1000).toFixed(1)}s</div>
-->
