# lab7
[lab7.html](https://github.com/user-attachments/files/28592743/lab7.html)
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Лабораторна робота №7 — JS Types & Operators</title>
<style>
body { font-family: 'Segoe UI', Arial, sans-serif; max-width: 900px; margin: 30px auto; padding: 0 20px; background: #f4f6f8; color: #222; }
h1 { color: #1565c0; border-bottom: 3px solid #1565c0; padding-bottom: 10px; }
h2 { color: #1976d2; margin-top: 30px; }
.card { background: #fff; border-radius: 8px; padding: 20px 24px; margin: 14px 0; box-shadow: 0 2px 8px rgba(0,0,0,.1); }
label { display: block; margin-bottom: 6px; font-weight: 600; color: #333; }
input { padding: 8px 12px; border: 1px solid #ccc; border-radius: 5px; font-size: 14px; width: 220px; }
button { margin-left: 10px; padding: 8px 18px; background: #1565c0; color: #fff; border: none; border-radius: 5px; cursor: pointer; font-size: 14px; }
button:hover { background: #1976d2; }
.result { background: #e8f5e9; border-left: 4px solid #43a047; padding: 12px 16px; border-radius: 4px; margin-top: 12px; font-family: monospace; white-space: pre-wrap; min-height: 40px; }
.result.error { background: #ffebee; border-color: #e53935; }
.tag-info { font-size: 12px; color: #777; margin-top: 4px; }
table { border-collapse: collapse; width: 100%; margin-top: 10px; }
th, td { border: 1px solid #ddd; padding: 8px 12px; font-family: monospace; font-size: 13px; }
th { background: #e3f2fd; font-weight: 700; }
tr:nth-child(even) { background: #f9f9f9; }
</style>
</head>
<body>

<h1>Лабораторна робота №7</h1>
<p>Тема: Типи даних, оператори та регулярні вирази у JavaScript</p>

<h2>Завдання 1 — isInteger(num)</h2>
<div class="card">
  <label>Введіть число:</label>
  <input type="text" id="intInput" placeholder="напр. 5 або 3.14">
  <button onclick="checkInt()">Перевірити</button>
  <div class="result" id="intResult"></div>
</div>

<h2>Завдання 1 — findPrimes(a, b)</h2>
<div class="card">
  <label>Введіть діапазон [a, b]:</label>
  <input type="number" id="primeA" placeholder="a" style="width:80px"> —
  <input type="number" id="primeB" placeholder="b" style="width:80px">
  <button onclick="runPrimes()">Знайти прості</button>
  <div class="result" id="primesResult"></div>
</div>

<h2>Завдання 2 — isIPAddress(ip)</h2>
<div class="card">
  <label>Введіть рядок для перевірки:</label>
  <input type="text" id="ipInput" placeholder="напр. 192.168.0.1">
  <button onclick="checkIP()">Перевірити</button>
  <div class="result" id="ipResult"></div>
</div>

<h2>Завдання 2 — findRGBA / findHexColor</h2>
<div class="card">
  <label>Введіть текст з кольором:</label>
  <input type="text" id="colorText" placeholder="напр. color: rgba(255,0,0,1) #ff0000" style="width:400px">
  <button onclick="findColors()">Знайти</button>
  <div class="result" id="colorResult"></div>
</div>

<h2>Завдання 2 — findEmail</h2>
<div class="card">
  <label>Введіть текст:</label>
  <input type="text" id="emailText" placeholder="напр. send to user@mail.com or admin@site.org" style="width:400px">
  <button onclick="findEmails()">Знайти email</button>
  <div class="result" id="emailResult"></div>
</div>

<h2>Завдання 2 — findDates</h2>
<div class="card">
  <label>Введіть текст:</label>
  <input type="text" id="dateText" placeholder="напр. events on 2024-03-15 and 2023-11-01" style="width:400px">
  <button onclick="findDts()">Знайти дати</button>
  <div class="result" id="dateResult"></div>
</div>
<script src="lab7-1.js"></script>
<script src="lab7-2.js"></script>
<script>
  'use strict';

  function checkInt() {
      let value = document.getElementById('intInput').value;
      let num = Number(value);

      document.getElementById('intResult').textContent =
          `isInteger(${value}) = ${isInteger(num)}`;
  }

  function runPrimes() {
      let a = Number(document.getElementById('primeA').value);
      let b = Number(document.getElementById('primeB').value);

      if (isNaN(a) || isNaN(b)) {
          document.getElementById('primesResult').textContent = 'Введіть числа';
          return;
      }

      let primes = findPrimes(a, b);

      document.getElementById('primesResult').textContent =
          `Прості числа [${a}, ${b}]: ${primes.length ? primes.join(', ') : 'немає'}`;
  }

  function checkIP() {
      let ip = document.getElementById('ipInput').value;

      document.getElementById('ipResult').textContent =
          `isIPAddress("${ip}") = ${isIPAddress(ip)}`;
  }

  function findColors() {
      let text = document.getElementById('colorText').value;

      let rgba = findRGBA(text);
      let hex = findHexColor(text);

      document.getElementById('colorResult').textContent =
          `RGBA: ${rgba || 'не знайдено'}\nHEX: ${hex || 'не знайдено'}`;
  }

  function findEmails() {
      let text = document.getElementById('emailText').value;
      let emails = findEmail(text);

      document.getElementById('emailResult').textContent =
          `Знайдено email (${emails.length}): ${emails.join(', ') || 'немає'}`;
  }

  function findDts() {
      let text = document.getElementById('dateText').value;
      let dates = findDates(text);

      document.getElementById('dateResult').textContent =
          `Знайдено дат (${dates.length}): ${dates.join(', ') || 'немає'}`;
  }

  function isInteger(num) {
      return Number.isInteger(num);
  }

  function findPrimes(a, b) {
      let result = [];

      for (let n = Math.max(2, Math.ceil(a)); n <= b; n++) {
          let prime = true;

          for (let i = 2; i * i <= n; i++) {
              if (n % i === 0) {
                  prime = false;
                  break;
              }
          }

          if (prime) {
              result.push(n);
          }
      }

      return result;
  }

  function isIPAddress(ip) {
      let parts = String(ip).split('.');

      if (parts.length !== 4) {
          return false;
      }

      return parts.every(part => {
          let num = Number(part);

          return part !== '' &&
                 !isNaN(num) &&
                 num >= 0 &&
                 num <= 255;
      });
  }

  function findRGBA(text) {
      let match = text.match(
          /rgba\(\s*\d+\s*,\s*\d+\s*,\s*\d+\s*,\s*[\d.]+\s*\)/
      );

      return match ? match[0] : null;
  }

  function findHexColor(text) {
      let match = text.match(
          /#(?:[0-9a-fA-F]{3}|[0-9a-fA-F]{6})\b/
      );

      return match ? match[0] : null;
  }

  function findTags(text, tag) {
      let regex = new RegExp(`<${tag}(\\s[^>]*)?>`, 'gi');

      return text.match(regex) || [];
  }

  function findPosNum(text) {
      let numbers =
          text.match(/\b\d+(?:\.\d+)?\b/g) || [];

      return numbers
          .map(Number)
          .filter(num => num > 0);
  }

  function findDates(text) {
      return text.match(
          /\b\d{4}-(?:0[1-9]|1[0-2])-(?:0[1-9]|[12]\d|3[01])\b/g
      ) || [];
  }

  function findEmail(text) {
      return text.match(
          /\b[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}\b/g
      ) || [];
  }
</script>
</body>
</html>
