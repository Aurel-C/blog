---
title: "Multi Armed Bandit"
date: 2025-01-13T20:05:52+01:00
---
<link rel="stylesheet" href="style.css">
<script src="https://d3js.org/d3.v6.min.js"></script>

- This is a visualisation representing an agent learning which is the best path to take to maximize his reward.<br>
- Each path gives a random reward following a normal distribution of a fixed mean given by the table on the right.<br>
- To make sure the agent finds the best path, it will try a sub optimal path 10% of the time.<br>
- Each path starts with an expected reward of 5 to force the agent to try every path during the first 10 steps.

<div id="full_bandit">
  <div id="container_bandit">
    <div>
      <h2>Arms and expected reward<br><br></h2>
      <svg id="paths"></svg>
      <br>
    </div>
    <div id="mean_reward">
      <h2 style="text-align: center;">True mean reward</h2>
      <div id="means"></div>
    </div>
  </div>
  <div id="buttons_bandit">
    <button onclick="reset()">Reset</button>
    <div>
      <input id="steps" type="number" value="10"></button>
      <button onclick="n_steps(steps.value);disable()">Run N steps</button>
    </div>
    <button onclick="step();disable()">Single Step</button>
  </div>
  <div>
    <h2>Expected reward over time</h2>
    <svg id="scatter"></svg>
  </div>
</div>
<script src="js/tree.js"></script>
<script src="js/scatter.js"></script>
<script src="js/bandit.js"></script>
<script>
  function disable() {
    let b = document.getElementsByTagName('button');
    for (let i = 0; i < b.length; i++) {
      b[i].setAttribute('disabled', 'disabled');
      setTimeout(() => {
        b[i].removeAttribute('disabled');
      }, 1500);
    }
  }
</script>
    
