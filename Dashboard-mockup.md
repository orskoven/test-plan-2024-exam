# Cyber Threat Intelligence Dashboard

Welcome to the **Cyber Threat Intelligence Dashboard**, your interactive platform to learn and engage with modern cyber threats.

---

## 🌍 Global Cyber Attack Map

<iframe src="https://cybermap.kaspersky.com/" width="100%" height="500"></iframe>

Use the above map to observe real-time cyberattacks worldwide.

---

## 📊 Threat Trends Over Time

```js
import { Chart } from 'chart.js';

const data = {
  labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May'],
  datasets: [{
    label: 'Phishing Attacks',
    data: [65, 59, 80, 81, 56],
    borderWidth: 1
  }]
};

const config = {
  type: 'line',
  data: data
};

Chart.defaults.color = '#fff';
const myChart = new Chart('myChart', config);
<canvas id="myChart" width="400" height="200"></canvas>
