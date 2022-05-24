<script>
  import NoteSelector from "../lib/NoteSelector.svelte"; 
  import QualitySelector from "../lib/QualitySelector.svelte";
  import ChordPosition from "../lib/ChordPosition.svelte";
  import InversionSelector from "../lib/InversionSelector.svelte";
  import TuningSelector from '../lib/TuningSelector.svelte';
  import TailwindCSS from '../lib/TailwindCSS.svelte';
  import { chordQualities as qualities, chromaticScale, applyInversion } from '../lib/_util'

  
  let tuning;
  let qualityIdx = 0;
  let rootIdx = 0;
  let inversionIdx = 0;

  $: selectedQuality = qualities[qualityIdx]
  $: selectedRoot = chromaticScale[rootIdx]
  $: intervals = applyInversion(selectedQuality.intervals, inversionIdx)
</script>

<TailwindCSS />

<div class="p-4 mx-auto lg:my-8 lg:flex max-w-7xl justify-evenly">

  <!-- Controls -->
  <div class="max-w-xl w-full mx-auto">
    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">Root Note</div> 
      <NoteSelector bind:selectedIdx={rootIdx} />
    </div>

    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">Chord Quality</div> 
      <QualitySelector {qualities} bind:selectedIdx={qualityIdx}/>
    </div>

    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">Inversion</div> 
      <InversionSelector bind:selectedIdx={inversionIdx}/>
    </div>

    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">Tuning</div> 
      <TuningSelector bind:tuning={tuning}/>
    </div>

  </div>

  <!-- Results -->
  <div class="max-w-xl w-full mx-auto">
    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">6th String</div> 
      <ChordPosition {tuning} {intervals} root={selectedRoot}/>
    </div>

    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">5th String</div> 
      <ChordPosition {tuning} {intervals} root={selectedRoot} lowestString={1}/>
    </div>

    <div class="mb-6">
      <div class="text-2xl font-bold text-gray-800 mb-2">4th String</div> 
      <ChordPosition {tuning} {intervals} root={selectedRoot} lowestString={2}/>
    </div>
  </div>
</div>

