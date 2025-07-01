# gorakhpur-glass--dashboard<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gorakhpur Glass & Arts - Product Dashboard</title>
  <style>
    body { font-family: sans-serif; padding: 2rem; background: #f4f4f4; }
    input, textarea { width: 100%; padding: 0.5rem; margin-bottom: 1rem; }
    button { padding: 0.6rem 1.2rem; margin-right: 0.5rem; background: #007bff; color: white; border: none; cursor: pointer; }
    label { font-weight: bold; margin-top: 1rem; display: block; }
    .product-card { background: white; padding: 1rem; margin: 1rem 0; border-radius: 8px; box-shadow: 0 0 10px #ccc; }
    .product-card img { max-width: 100%; border-radius: 8px; }
    .actions button { background: #dc3545; }
    pre { background: #222; color: #0f0; padding: 1rem; overflow-x: auto; margin-top: 2rem; }
    #loginPanel { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: #0009; display: flex; justify-content: center; align-items: center; z-index: 9999; }
    #loginPanel div { background: white; padding: 2rem; border-radius: 10px; box-shadow: 0 0 20px #000; }
  </style>
</head>
<body>
  <div id="loginPanel">
    <div>
      <h2>🔒 Admin Login</h2>
      <input type="password" id="password" placeholder="Enter password" />
      <button onclick="checkLogin()">Login</button>
    </div>
  </div>

  <h1>📋 Gorakhpur Glass & Arts - Product Dashboard</h1>

  <label>Product Name</label>
  <input type="text" id="name" />

  <label>Image URL</label>
  <input type="text" id="image" />

  <label>Description</label>
  <textarea id="description"></textarea>

  <label>Category</label>
  <input type="text" id="category" />

  <label>WhatsApp Message</label>
  <input type="text" id="whatsapp" />

  <button onclick="addProduct()">Add Product</button>
  <button onclick="clearAll()">Clear All</button>

  <h2>📦 Preview</h2>
  <div id="productList"></div>

  <h2>🧾 HTML Code to Copy</h2>
  <pre id="output"></pre>

  <script>
    const ADMIN_PASSWORD = "glass123"; // You can change this password

    function checkLogin() {
      const input = document.getElementById("password").value;
      if (input === ADMIN_PASSWORD) {
        document.getElementById("loginPanel").style.display = "none";
      } else {
        alert("Incorrect password");
      }
    }

    let products = JSON.parse(localStorage.getItem('products') || '[]');

    function renderProducts() {
      const list = document.getElementById('productList');
      const output = document.getElementById('output');
      list.innerHTML = '';
      let htmlOutput = '';

      products.forEach((p, i) => {
        const card = `
<div class="product-card">
  <img src="${p.image}" alt="${p.name}">
  <h3>${p.name}</h3>
  <p>${p.description}</p>
  <p><strong>Category:</strong> ${p.category}</p>
  <a href="${p.whatsapp}" target="_blank">Get Quote</a>
  <div class="actions">
    <button onclick="deleteProduct(${i})">Delete</button>
  </div>
</div>
`;
        list.innerHTML += card;

        htmlOutput += `
<div class="bg-white rounded-xl shadow p-4">
  <img src="${p.image}" alt="${p.name}" class="rounded-lg mb-4">
  <h4 class="text-xl font-bold">${p.name}</h4>
  <p>${p.description}</p>
  <a href="${p.whatsapp}" target="_blank" class="mt-4 inline-block bg-green-500 text-white py-1 px-4 rounded hover:bg-green-600">Get Quote</a>
</div>
`;
      });

      output.textContent = htmlOutput.trim();
    }

    function addProduct() {
      const product = {
        name: document.getElementById('name').value,
        image: document.getElementById('image').value,
        description: document.getElementById('description').value,
        category: document.getElementById('category').value,
        whatsapp: 'https://wa.me/919696957914?text=' + encodeURIComponent(document.getElementById('whatsapp').value)
      };
      products.push(product);
      localStorage.setItem('products', JSON.stringify(products));
      renderProducts();
    }

    function deleteProduct(index) {
      products.splice(index, 1);
      localStorage.setItem('products', JSON.stringify(products));
      renderProducts();
    }

    function clearAll() {
      if (confirm('Are you sure you want to delete all products?')) {
        products = [];
        localStorage.removeItem('products');
        renderProducts();
      }
    }

    renderProducts();
  </script>
</body>
</html>
 Product-entry-form.html
</index.html>
