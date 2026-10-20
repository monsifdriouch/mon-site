<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SnackZone | متجر الشيبس والشكلاط</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #080808;
  color: white;
  font-family: Arial, sans-serif;
}

header {
  background: #111;
  padding: 18px;
  border-bottom: 2px solid #ed001b;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
}

.logo {
  color: #ff1028;
  font-size: 27px;
  font-weight: bold;
}

.logo span {
  color: white;
}

.search {
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #444;
  background: #222;
  color: white;
  width: 100%;
  max-width: 280px;
}

.hero {
  margin: 20px;
  padding: 35px 20px;
  border-radius: 14px;
  text-align: center;
  background: linear-gradient(135deg, #330009, #101010);
  border: 1px solid #ff1028;
}

.hero h1 {
  font-size: 32px;
}

.hero span {
  color: #ff1028;
}

.hero p {
  color: #ddd;
}

h2 {
  margin: 25px 18px;
}

.categories {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  padding: 0 12px;
}

.category {
  background: #191919;
  border: 1px solid #333;
  padding: 13px 18px;
  border-radius: 10px;
  cursor: pointer;
}

.category:hover {
  border-color: #ff1028;
}

.products {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
  padding: 12px;
}

.card {
  background: #141414;
  border: 1px solid #303030;
  border-radius: 12px;
  padding: 12px 8px;
  text-align: center;
  min-width: 0;
}

.product-image {
  font-size: 48px;
  margin: 8px 0;
}

.card h3 {
  font-size: 15px;
}

.price {
  color: #ff243b;
  font-weight: bold;
}

button {
  background: #ed001b;
  color: white;
  border: none;
  padding: 11px;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background: #b80016;
}

.card button {
  width: 100%;
  font-size: 12px;
}

.cart {
  margin: 15px;
  padding: 18px;
  border: 1px solid #ed001b;
  border-radius: 12px;
  background: #151515;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  gap: 8px;
  align-items: center;
  border-bottom: 1px solid #333;
  padding: 10px 0;
}

.cart-item button {
  padding: 6px 10px;
}

.total {
  font-size: 20px;
  color: #ff243b;
  font-weight: bold;
}

.checkout {
  width: 100%;
  margin-top: 12px;
}

footer {
  text-align: center;
  padding: 25px;
  background: #111;
  color: #aaa;
  margin-top: 25px;
}

@media (max-width: 420px) {
  header {
    padding: 13px;
  }

  .logo {
    font-size: 23px;
  }

  .hero h1 {
    font-size: 25px;
  }

  .products {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 8px;
    padding: 8px;
  }

  .card {
    padding: 10px 6px;
  }

  .product-image {
    font-size: 40px;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">Snack<span>Zone</span> 🔴</div>
  <input class="search" id="search"
    placeholder="ابحث عن شيبس أو شكلاط..."
    oninput="renderProducts()">
  <div>🛒 السلة: <span id="count">0</span></div>
</header>

<section class="hero">
  <h1>مرحبا بك في <span>SnackZone</span></h1>
  <p>🍫 شكلاط • 🥔 شيبس • 🥤 مشروبات</p>
  <p>كل ما تحب في مكان واحد!</p>
  <button onclick="document.getElementById('products').scrollIntoView()">
    تسوق الآن
  </button>
</section>

<h2>🛍️ أقسام المتجر</h2>

<div class="categories">
  <button class="category" onclick="setCategory('الكل')">الكل</button>
  <button class="category" onclick="setCategory('شيبس')">🥔 الشيبس</button>
  <button class="category" onclick="setCategory('شكلاط')">🍫 الشكلاط</button>
  <button class="category" onclick="setCategory('مشروبات')">🥤 المشروبات</button>
  <button class="category" onclick="setCategory('بسكويت')">🍪 البسكويت</button>
</div>

<h2>🔥 منتجاتنا</h2>
<div class="products" id="products"></div>

<section class="cart" id="cart">
  <h2>🛒 سلة المشتريات</h2>
  <div id="cartItems">السلة فارغة حاليا.</div>
  <p>المجموع: <span class="total" id="total">0.00</span> درهم</p>
  <button class="checkout" onclick="checkout()">إتمام الطلب</button>
</section>

<footer>
  <h3>SnackZone</h3>
  <p>متجرك المفضل للشيبس والشكلاط والمشروبات ❤️</p>
  <p>جميع الحقوق محفوظة © 2026</p>
</footer>

<script>
const products = [
  {id:1, name:"شيبس كلاسيك", category:"شيبس", price:12, icon:"🥔"},
  {id:2, name:"شيبس حار", category:"شيبس", price:15, icon:"🌶️"},
  {id:3, name:"شكلاط بالحليب", category:"شكلاط", price:10, icon:"🍫"},
  {id:4, name:"شكلاط بالبندق", category:"شكلاط", price:18, icon:"🍫"},
  {id:5, name:"مشروب غازي", category:"مشروبات", price:8, icon:"🥤"},
  {id:6, name:"مشروب الطاقة", category:"مشروبات", price:20, icon:"⚡"},
  {id:7, name:"بسكويت بالشوكولاتة", category:"بسكويت", price:9, icon:"🍪"},
  {id:8, name:"كوكيز", category:"بسكويت", price:12, icon:"🍪"}
];

let cart = {};
let category = "الكل";

function setCategory(value) {
  category = value;
  renderProducts();
}

function renderProducts() {
  const query = document.getElementById("search").value
    .trim().toLowerCase();

  const filtered = products.filter(p =>
    (category === "الكل" || p.category === category) &&
    p.name.toLowerCase().includes(query)
  );

  document.getElementById("products").innerHTML =
    filtered.map(p => `
      <article class="card">
        <div class="product-image">${p.icon}</div>
        <h3>${p.name}</h3>
        <p class="price">${p.price.toFixed(2)} درهم</p>
        <button onclick="addToCart(${p.id})">
          أضف إلى السلة 🛒
        </button>
      </article>
    `).join("") || "<p>لم يتم العثور على منتجات.</p>";
}

function addToCart(id) {
  cart[id] = (cart[id] || 0) + 1;
  renderCart();
}

function changeQty(id, amount) {
  cart[id] = (cart[id] || 0) + amount;

  if (cart[id] <= 0) delete cart[id];

  renderCart();
}

function renderCart() {
  let count = 0;
  let total = 0;

  document.getElementById("cartItems").innerHTML =
    Object.keys(cart).map(id => {
      const p = products.find(item => item.id === Number(id));
      const qty = cart[id];

      count += qty;
      total += p.price * qty;

      return `
        <div class="cart-item">
          <span>${p.icon} ${p.name}</span>
          <span>${qty} × ${p.price} د.م</span>
          <button onclick="changeQty(${p.id}, -1)">−</button>
          <button onclick="changeQty(${p.id}, 1)">+</button>
        </div>
      `;
    }).join("") || "السلة فارغة حاليا.";

  document.getElementById("count").textContent = count;
  document.getElementById("total").textContent = total.toFixed(2);
}

function checkout() {
  if (Object.keys(cart).length === 0) {
    alert("أضف بعض المنتجات إلى السلة أولا!");
    return;
  }

  const order = Object.keys(cart).map(id => {
    const p = products.find(item => item.id === Number(id));
    return `${p.name} × ${cart[id]} = ${(p.price * cart[id]).toFixed(2)} درهم`;
  }).join("\n");

  const total = Object.keys(cart).reduce((sum, id) => {
    const p = products.find(item => item.id === Number(id));
    return sum + p.price * cart[id];
  }, 0);

  alert("ملخص الطلب:\n" + order +
        "\nالمجموع: " + total.toFixed(2) +
        " درهم\n\nهذا نموذج تجريبي. أضف وسيلة اتصال لاستقبال الطلبات.");
}

renderProducts();
renderCart();
</script>

</body>
</html>
