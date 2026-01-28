#---HTML---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Product Filter</title>

  <!-- CSS FILE -->
  <link rel="stylesheet" href="Exp2.2.css">
</head>
<body>

  <div class="wrap">
    <h1>Product Filter</h1>

    <div class="filter-row">
      <label for="filterSelect">Filter by:</label>
      <select id="filterSelect">
        <option value="all">All Products</option>
        <option value="electronics">electronics</option>
        <option value="clothing">clothing</option>
      </select>
    </div>

    <div id="productGrid" class="grid"></div>
  </div>

  <!-- JS FILE -->
  <script src="Exp2.2.js"></script>
</body>
</html>
#---CSS---
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background: #f7f9fc;
  color: #0f172a;
}

.wrap {
  width: min(900px, 92vw);
  margin: 60px auto;
}

h1 {
  font-size: 64px;
  font-weight: 800;
  margin-bottom: 26px;
}

.filter-row {
  display: flex;
  align-items: center;
  gap: 18px;
  margin-bottom: 32px;
}

label {
  font-size: 30px;
  font-weight: 600;
}

select {
  flex: 1;
  padding: 16px 18px;
  font-size: 26px;
  border: 2px solid #d6dbe8;
  border-radius: 12px;
  background: #fff;
  outline: none;
}

/* Product Grid */
.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 26px;
}

/* Card */
.card {
  background: #fff;
  border: 2px solid #d6dbe8;
  border-radius: 14px;
  padding: 28px;
  min-height: 230px;
}

.title {
  font-size: 44px;
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 12px;
}

.price {
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 18px;
}

.tag {
  display: inline-block;
  padding: 10px 22px;
  border-radius: 999px;
  font-size: 24px;
  color: white;
  text-transform: lowercase;
}

.tag.electronics {
  background: #2f67ff;
}

.tag.clothing {
  background: #9bbcff;
}

/* Mobile */
@media (max-width: 720px) {
  h1 { font-size: 46px; }
  label { font-size: 22px; }
  select { font-size: 20px; }
  .grid { grid-template-columns: 1fr; }
  .title { font-size: 34px; }
}
#---JS---
const products = [
  { name: "Wireless Headphones", price: 129.99, category: "electronics" },
  { name: "Cotton T-Shirt", price: 24.99, category: "clothing" },
  { name: "Bluetooth Speaker", price: 89.99, category: "electronics" },
  { name: "Denim Jeans", price: 59.99, category: "clothing" }
];

const grid = document.getElementById("productGrid");
const filterSelect = document.getElementById("filterSelect");

// Create product card
function createCard(product) {
  const card = document.createElement("div");
  card.className = "card";

  card.innerHTML = `
    <div class="title">${product.name}</div>
    <div class="price">$${product.price.toFixed(2)}</div>
    <span class="tag ${product.category}">${product.category}</span>
  `;

  return card;
}

// Render products
function renderProducts(list) {
  grid.innerHTML = "";
  list.forEach(product => grid.appendChild(createCard(product)));
}

// Filter products
filterSelect.addEventListener("change", () => {
  const selected = filterSelect.value;

  const filtered =
    selected === "all"
      ? products
      : products.filter(p => p.category === selected);

  renderProducts(filtered);
});

// Initial display
renderProducts(products);
