<script lang="ts">
  import { onMount } from 'svelte';

  export let text = '';
  export let intervalMinMs = 3000;
  export let intervalMaxMs = 30000;
  export let rapidChance = 0.12;
  export let twoLetterChance = 0.25;
  export let normalDurationMinMs = 80;
  export let normalDurationMaxMs = 220;
  export let rapidDurationMinMs = 120;
  export let rapidDurationMaxMs = 220;

  let flickerIndices: number[] = [];
  let flickerDuration = 120;
  let isRapidFlicker = false;

  const getFlickerCandidates = () =>
    [...text]
      .map((char, index) => ({ char, index }))
      .filter(({ char }) => char !== ' ')
      .map(({ index }) => index);

  onMount(() => {
    let flickerTimeout: number;
    let flickerResetTimeout: number;

    const randomBetween = (min: number, max: number) =>
      Math.floor(Math.random() * (max - min + 1)) + min;

    const scheduleFlicker = () => {
      const delay = randomBetween(intervalMinMs, intervalMaxMs);

      flickerTimeout = window.setTimeout(() => {
        const flickerCandidates = getFlickerCandidates();
        if (flickerCandidates.length === 0) {
          scheduleFlicker();
          return;
        }

        const shouldDoubleFlicker = Math.random() < twoLetterChance;
        const firstIndex = Math.floor(Math.random() * flickerCandidates.length);
        let activeIndices = [flickerCandidates[firstIndex]];

        if (shouldDoubleFlicker && flickerCandidates.length > 1) {
          let secondIndex = firstIndex;
          while (secondIndex === firstIndex) {
            secondIndex = Math.floor(Math.random() * flickerCandidates.length);
          }

          activeIndices = [
            flickerCandidates[firstIndex],
            flickerCandidates[secondIndex]
          ];
        }

        const rapid = Math.random() < rapidChance;
        const duration = rapid
          ? randomBetween(rapidDurationMinMs, rapidDurationMaxMs)
          : randomBetween(normalDurationMinMs, normalDurationMaxMs);

        isRapidFlicker = rapid;
        flickerDuration = duration;
        flickerIndices = activeIndices;

        window.clearTimeout(flickerResetTimeout);
        flickerResetTimeout = window.setTimeout(() => {
          flickerIndices = [];
          isRapidFlicker = false;
        }, duration);

        scheduleFlicker();
      }, delay);
    };

    scheduleFlicker();

    return () => {
      window.clearTimeout(flickerTimeout);
      window.clearTimeout(flickerResetTimeout);
    };
  });
</script>

<h1 class="title" aria-label={text}>
  {#each [...text] as letter, index}
    <span
      class:letter
      class:flicker={flickerIndices.includes(index)}
      class:rapid={flickerIndices.includes(index) && isRapidFlicker}
      style={`--flicker-duration: ${flickerDuration}ms;`}
    >
      {letter === ' ' ? '\u00A0' : letter}
    </span>
  {/each}
</h1>

<style>
  .title {
    display: inline-block;
    color: #fff;
    text-shadow: 0 0 5px white;
  }

  .letter {
    display: inline-block;
    transition: opacity 0.08s linear;
  }

  .flicker {
    animation: neon-flicker var(--flicker-duration, 120ms) steps(1, end);
  }

  .rapid {
    animation-name: neon-flicker-rapid;
  }

  @keyframes neon-flicker {
    0% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
    30% {
      opacity: 0.2;
      text-shadow: none;
    }
    60% {
      opacity: 0.75;
      text-shadow: 0 0 3px white;
    }
    100% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
  }

  @keyframes neon-flicker-rapid {
    0% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
    10% {
      opacity: 0;
      text-shadow: none;
    }
    20% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
    30% {
      opacity: 0.15;
      text-shadow: none;
    }
    40% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
    50% {
      opacity: 0;
      text-shadow: none;
    }
    60% {
      opacity: 1;
      text-shadow: 0 0 4px white;
    }
    70% {
      opacity: 0.1;
      text-shadow: none;
    }
    80% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
    90% {
      opacity: 0.35;
      text-shadow: none;
    }
    100% {
      opacity: 1;
      text-shadow: 0 0 5px white;
    }
  }
</style>