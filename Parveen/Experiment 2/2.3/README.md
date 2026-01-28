#---HTML---
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>SVG Drawing Tool</title>

<style>
  body {
    margin: 0;
    padding: 20px;
    font-family: Arial, sans-serif;
    background: #f5f7fb;
  }

  h2 {
    margin-bottom: 15px;
  }

  .toolbar {
    display: flex;
    gap: 15px;
    align-items: center;
    margin-bottom: 15px;
  }

  button {
    padding: 10px 22px;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    background: #2563eb;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background: #1e40af;
  }

  input[type="color"] {
    width: 50px;
    height: 40px;
    border: none;
    cursor: pointer;
  }

  .canvas {
    border: 2px dashed #cbd5e1;
    border-radius: 14px;
    background: white;
    padding: 10px;
  }

  svg {
    width: 100%;
    height: 70vh;   /* responsive */
    cursor: crosshair;
  }
</style>
</head>

<body>

<h2>SVG Drawing Tool</h2>

<div class="toolbar">
  <label>Select Color:</label>
  <input type="color" id="colorPicker" value="#2563eb">
  <button id="undoBtn">Undo</button>
</div>

<div class="canvas">
  <svg id="svgCanvas" viewBox="0 0 1000 600"></svg>
</div>

<script>
  const svg = document.getElementById("svgCanvas");
  const undoBtn = document.getElementById("undoBtn");
  const colorPicker = document.getElementById("colorPicker");

  let shapes = [];

  // Mouse click event to draw circle
  svg.addEventListener("click", (event) => {
    const rect = svg.getBoundingClientRect();

    const x = ((event.clientX - rect.left) / rect.width) * 1000;
    const y = ((event.clientY - rect.top) / rect.height) * 600;

    const circle = document.createElementNS(
      "http://www.w3.org/2000/svg",
      "circle"
    );

    circle.setAttribute("cx", x);
    circle.setAttribute("cy", y);
    circle.setAttribute("r", 12);
    circle.setAttribute("fill", colorPicker.value);

    svg.appendChild(circle);
    shapes.push(circle);
  });

  // Undo last shape
  undoBtn.addEventListener("click", () => {
    if (shapes.length > 0) {
      const lastShape = shapes.pop();
      svg.removeChild(lastShape);
    }
  });
</script>

</body>
</html>
