---
title: "Multi Armed Bandit"
date: 2025-01-13T20:05:52+01:00
draft: true
---
<link rel="stylesheet" href="style.css">
<script src="https://d3js.org/d3.v6.min.js"></script>
<div id="container_bandit">
    <div>
      <h2>Arms and expected reward</h2>
      <svg id="paths"></svg>
      <br>
      <div id="buttons_bandit">
        <button onclick="reset()">Reset</button>
        <div>
          <label>Number of steps:</label>
          <input id="steps" type="number"></button>
          <button onclick="n_steps(steps.value);disable()">Run steps</button>
        </div>
        <button onclick="step();disable()">Next Step</button>
      </div>
    </div>
    <div>
      <h2 id="mean_reward">True mean reward</h2>
      <div id="means"></div>
    </div>
  </div>
    <div>
      <h2>Expected reward over time</h2>
      <svg id="scatter"></svg>
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

This visualisation represents an agent learning which is the best path to take to maximize his reward.
Each path gives a random reward following a normal distribution of a fixed mean given by the table.
To make sure the agent don't always try the same path it will try a sub optimal path 10% of the time in order to explore other paths
You can also notice that each path starts with an expected reward of 5 to force the agent to try every path during the first 10 steps.