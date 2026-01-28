#---HTML--- 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Live Character Counter</title>
  <link rel="stylesheet" href="Exp2.1.css">
</head>
<body>

  <section class="card">
    <textarea id="message" maxlength="150" placeholder="Type your message..."></textarea>
    <div class="counter" id="counter">0/150</div>
  </section>

  <script src="Exp2.1.js"></script>
</body>
</html>

#---CSS---
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  background: black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

.card {
  width: 600px;
  height: 200px;
  padding: 20px;
  background: #8086f7;
  border-radius: 12px;
  position: relative;
}

textarea {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  resize: none;
  padding: 15px;
  font-size: 28px;
  border-radius: 10px;
  background: black;
  color: white;
}

textarea::placeholder {
  color: #f0e7e7;
}

.counter {
  position: absolute;
  bottom: 10px;
  right: 15px;
  font-size: 20px;
  color: #ddd;
}

/* warning colors */
.counter.warn {
  color: orange;
}

.counter.danger {
  color: red;
}
#---JS---
const textarea = document.getElementById("message");
const counter = document.getElementById("counter");
const max = 150;

textarea.addEventListener("input", () => {
  const len = textarea.value.length;
  counter.textContent = `${len}/${max}`;

  counter.classList.remove("warn", "danger");

  if (len >= max - 20 && len < max) {
    counter.classList.add("warn");
  }

  if (len === max) {
    counter.classList.add("danger");
  }
});

