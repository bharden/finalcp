<template>
<div id="app">
  <div class="header">
    <div class="title">
      <h1>Ben's Music Box</h1>
      <div class="pages1">
        <router-link to="/fun">Fun</router-link>
      </div>
      <div class="pages2">
        <router-link to="/">Home</router-link>
      </div>
    </div>
  </div>
  <div class="content">
    <router-view />
  </div>
  <div class="footer">
    <p></p>
    <a href="https://github.com/bharden/finalcp.git">clickable repo link</a>
  </div>
</div>
</template>

<style>
html {
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  background: #fff;
  padding: 0px;
  margin: 0px;
  text-align: center;
}

/* Header */
.header {
  text-align: center;
  padding: 10px 100px 50px 100px;
  background: linear-gradient(-90deg, #809fff, #f2e6ff);
  color: #1C454F;
}
.pages1 {
  float: left;
  background-color: #b3ccff;
  padding: 5px;
  border-radius: 15%;
}
.pages1 a {
  text-decoration: none;
}
.pages2 {
  float: right;
  background-color: #b3ccff;
  padding: 5px;
  border-radius: 15%;
}
.pages2 a {
  text-decoration: none;
}

.title h1 {
  font-size: 30px;
}

.content {
  padding: 20px 100px;
  min-height: 500px;
}

/* Footer */
.footer {
  height: 50px;
  padding: 20px 100px 0px 100px;
  background: #e3e3e3;
  font-size: 12px;
  background: linear-gradient(-90deg, #f2e6ff, #809fff);
}

.footer a {
  color: #000;
  text-decoration: none;
  border-radius: 15%;
  background-color: #b3ccff;
  padding: 5px;
}

h1 {
  font-size: 20px;
}

h2 {
  font-size: 14px;
}
</style>
