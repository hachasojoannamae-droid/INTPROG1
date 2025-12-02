<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>GlamourGlow - Premium Makeup Products</title>
        <!--
                Welcome to GlamourGlow: A demo landing page showcasing featured makeup items.
                Use this file for the public homepage: it contains
                    - the hero banner and primary CTA
                    - featured product cards (click to open images)
                    - Login / Sign Up - UI forms (demo-only: stored in localStorage)
        -->
    <style>
        /*
            Large banner area with an attention-grabbing gradient and product image.
            Contains a call-to-action sign-up button that opens the sign-up UI.
        */
        /*
            The :root CSS variable block makes it easy to change the hero circle size
            across the page. The large hero circle can be adjusted for desktop & mobile
            by changing --hero-circle-size and --hero-circle-mobile-size.
        */
        :root{
            --hero-circle-size: 400px;
            --hero-circle-mobile-size: 300px;
        }

       
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
            padding-top: 80px; /* leave space for fixed nav */
        }
        

        .hero {
            background: linear-gradient(135deg, rgba(255, 20, 147, 0.1), rgba(102, 126, 234, 0.1)),
                        url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 600"><defs><linearGradient id="grad1" x1="0%25" y1="0%25" x2="100%25" y2="100%25"><stop offset="0%25" style="stop-color:rgb(255,105,180);stop-opacity:0.1" /><stop offset="100%25" style="stop-color:rgb(102,126,234);stop-opacity:0.1" /></linearGradient></linearGradient></defs><rect width="1200" height="600" fill="url(%23grad1)"/></svg>');
            background-size: cover;
            background-position: center;
            height: calc(100vh - 80px);
            display: flex;
            align-items: center;
            justify-content: center;
            /* margin-top removed; top padding on body handles nav spacing */
            flex-direction: row;
            gap: 4rem;
        }

        .hero-content {
            max-width: 500px;
            color: white;
        }

        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            line-height: 1.6;
        }

        .hero-image {
            width: var(--hero-circle-size);
            height: var(--hero-circle-size);
            background: linear-gradient(135deg, #ff69b4, #764ba2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            font-size: 120px;
            overflow: hidden; /* make sure inner image respects the circle mask */
        }

        /* Make hero inner images fill the circular area */
        .hero-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
            border-radius: 50%;
        }

        /* Products Section */
        /*
            The product grid below shows a small selection of featured products.
            On this homepage the 'Add to Cart' buttons prompt login (openLoginUI)
            because we require users to sign in first.
        */
        .products {
            padding: 4rem 2rem;             
            background: white;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 3rem;
            color: #333;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            max-width: 1200px;
            margin: 0 auto;
        }

        .product-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
        }

        .product-image {
            width: 100%;
            height: 250px;
            background: linear-gradient(135deg, #ff69b4, #ffa6d1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 80px;
            color: white;
            object-fit: cover;
        }

        .product-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block; /* prevent inline image gap */
            cursor: zoom-in; /* indicate the image can be viewed */
        }

        /* Specific smaller size for one product image (Velvet Lipstick) */
        .product-image.small-product {
            width: var(--hero-circle-size); /* match hero circle size */
            height: var(--hero-circle-size); /* same as width for perfect circle */
            max-width: var(--hero-circle-size); /* limit width to hero circle size */
            margin: 0.6rem auto; /* center within the card */
            border-radius: 50%; /* circle */
            background: radial-gradient(circle at 30% 20%, rgba(255,105,180,0.18), rgba(118,75,162,0.18));
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden; /* clip image to circle */
            box-shadow: 0 8px 30px rgba(118,75,162,0.12);
            transition: transform 0.18s ease, box-shadow 0.18s ease;
        }

        .product-image.small-product img{
            width: 100%;
            height: 100%;
            object-fit: cover; /* fill the circular area */
            display: block;
            border-radius: 0; /* parent handles the circular mask */
        }

        .product-image.small-product:hover {
            transform: translateY(-6px) scale(1.04);
            box-shadow: 0 16px 40px rgba(118,75,162,0.14);
        }

        /* Primary Call-To-Action (CTA) button styling
           Targets the hero 'Shop Now' button which uses class .btn-signup.
           Provides a prominent gradient, padding, shadow and interactive states.
        */
        .btn {
            padding: 0.6rem 1rem;
            border-radius: 8px;
            border: 2px solid transparent;
            cursor: pointer;
            font-family: inherit;
            transition: transform 0.2s ease, box-shadow 0.2s ease, opacity 0.2s ease;
        }

        .btn-signup {
            padding: 0.9rem 1.6rem;
            font-size: 1.05rem;
            border-radius: 12px;
            background: linear-gradient(90deg,#ff8ab8 0%, #ff1493 100%);
            color: #fff;
            border: none;
            box-shadow: 0 8px 20px rgba(255, 20, 147, 0.18);
            font-weight: 700;
        }

        .hero .btn-signup {
            margin-top: 1rem;
        }

        .btn-signup:hover {
            transform: translateY(-4px);
            box-shadow: 0 14px 30px rgba(255, 20, 147, 0.28);
            opacity: 0.98;
        }

        .btn-signup:active {
            transform: translateY(-1px);
        }

        /* Make nav buttons slightly more subtle on the colorful hero background */
        nav .btn {
            background: rgba(255,255,255,0.06);
            color: white;
            border: 1px solid rgba(255,255,255,0.12);
        }

        /* Login button (outline style) - more visible and accessible */
        .btn-login {
            background: transparent; /* transparent over hero gradient */
            color: white;
            border: 1px solid rgba(255,255,255,0.9);
            padding: 0.55rem 1rem;
            border-radius: 10px;
            font-weight: 700;
            transition: background 0.15s ease, color 0.15s ease, transform 0.12s ease;
        }

        .btn-login:hover, .btn-login:focus {
            background: rgba(255,255,255,0.95);
            color: #ff1493;
            transform: translateY(-2px);
            outline: none;
        }

        /* Logo styling - stylize the brand text and make visible on hero */
        .logo {
            font-weight: 800;
            font-size: 1.2rem;
            color: white;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 0.4rem;
            letter-spacing: 0.3px;
            text-shadow: 0 2px 8px rgba(0,0,0,0.25);
        }

        .logo::before {
            content: '✨';
            margin-right: 0.25rem;
        }

        /* Navigation layout - logo on the left, nav buttons on the right */
        nav {
            display: flex;
            align-items: center;
            justify-content: space-between; /* pushes nav buttons to the right */
            gap: 0.75rem;
            padding: 1rem 2rem;
            position: sticky;
            top: 0;
            z-index: 150;
            background: transparent; /* keep hero background visible */
        }

        .nav-buttons {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-left: auto; /* ensure buttons stay on the right of the nav */
        }

        /* Ensure login and sign-up buttons look consistent and the same size */
        .nav-buttons .btn {
            padding: 0.8rem 1.2rem;
            min-width: 96px;
            border-radius: 10px;
            font-size: 0.95rem;
            font-weight: 700;
            text-align: center;
        }

        /* Make nav buttons slightly more subtle on the colorful hero background */
        
        
.project-card {
    background: rgba(255,255,255,0.06);
    color: white;
    border: 1px solid rgba(255,255,255,0.2);

    
}

        .nav-buttons .btn-signup {
            padding: 0.8rem 1.2rem; /* match nav button sizing */
            font-size: 0.95rem;
            border-radius: 10px;
        }

        /* Focus outlines for keyboard users */
        .btn:focus, .btn-submit:focus, .btn-add-cart:focus, .quantity-btn:focus {
            outline: 3px solid rgba(255,105,180,0.25);
            outline-offset: 2px;
        }

        /* Make interactive images show a focus outline for keyboard users */
        img[role="button"]:focus {
            outline: 3px solid rgba(255,105,180,0.25);
            outline-offset: 2px;
        }

        .product-info {
            padding: 1.5rem;
        }

        .product-name {
            font-size: 1.3rem;
            font-weight: bold;
            color: #333;
            margin-bottom: 0.5rem;
        }

        .product-description {
            color: #666;
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }

        .price-section {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .product-price {
            font-size: 1.5rem;
            font-weight: bold;
            color: #ff69b4;
        }

        .product-rating {
            color: #ff9800;
            font-size: 0.9rem;
        }

        .btn-add-cart {
            width: 100%;
            padding: 0.8rem;
            background: linear-gradient(135deg, #ff69b4, #ff1493);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .btn-add-cart:hover {
            transform: scale(1.02);
            box-shadow: 0 5px 15px rgba(255, 20, 147, 0.4);
        }

        /* Modal Styles */
        /*
            Styles used by both Login and Sign Up modals. These modals are positioned
            fixed and centered; they use subtle animations for appear/disappear.
        */
        .modal {
            display: none;
            position: fixed;
            z-index: 200;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: white;
            margin: 5% auto;
            padding: 2rem;
            border-radius: 15px;
            max-width: 450px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            animation: slideDown 0.3s ease;
        }

        /* Image modal content: larger, centered and transparent */
        .image-modal-content {
            background: transparent;
            margin: 3% auto;
            padding: 1rem;
            border-radius: 12px;
            max-width: 90%;
            animation: slideDown 0.25s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            box-shadow: none;
        }

        .image-modal-content .close {
            color: white;
            font-size: 2.2rem;
            position: absolute;
            right: 16px;
            top: 10px;
            background: rgba(0,0,0,0.35);
            padding: 6px 10px;
            border-radius: 6px;
        }

        @keyframes slideDown {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .close {
            float: right;
            font-size: 2rem;
            font-weight: bold;
            color: #999;
            cursor: pointer;
        }

        .close:hover {
            color: #000;
        }

        .modal h2 {
            margin-bottom: 1.5rem;
            color: #333;
        }

        .form-group {
            margin-bottom: 1.2rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: #333;
            font-weight: 600;
        }

        .form-group input {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus {
            outline: none;
            border-color: #ff69b4;
            box-shadow: 0 0 10px rgba(255, 105, 180, 0.2);
        }

        .btn-submit {
            width: 100%;
            padding: 0.8rem;
            background: linear-gradient(135deg, #ff69b4, #ff1493);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .btn-submit:hover {
            transform: scale(1.02);
            box-shadow: 0 5px 15px rgba(255, 20, 147, 0.4);
        }

        .toggle-form {
            text-align: center;
            margin-top: 1rem;
            color: #666;
        }

        .toggle-form a {
            color: #ff69b4;
            cursor: pointer;
            font-weight: 600;
            text-decoration: none;
        }

        .toggle-form a:hover {
            text-decoration: underline;
        }

        /* Footer */
        footer {
            background: #333;
            color: white;
            text-align: center;
            padding: 2rem;
        }

        @media (max-width: 768px) {
            :root{ --hero-circle-size: var(--hero-circle-mobile-size); }
            .hero {
                flex-direction: column;
                padding: 2rem;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .hero-image {
                width: var(--hero-circle-size);
                height: var(--hero-circle-size);
            }

            .nav-buttons {
                gap: 0.5rem;
            }

            .btn {
                padding: 0.5rem 1rem;
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GlamourGlow - Shop</title>
    <!--
        Project: GlamourGlow - Shop Page
        This file code contains the logged-in shopping experience: product listing, search
        and a full cart/checkout flow implemented in client-side JavaScript. Data is
        kept in `localStorage` for demo purposes (cart and orders).
    -->
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f5f5f5;
            color: #333;
            padding-top: 80px; /* avoid overlap with sticky nav */
        }

          /* Navigation Bar */
          /* Navigation contains the logo, a welcome label and a cart indicator. The
              `cartCount` is clickable and opens the cart modal. */
        nav {
            background: rgba(0, 0, 0, 0.8);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #ff69b4;
            text-decoration: none;
            cursor: pointer;
        }

        .nav-info {
            display: flex;
            align-items: center;
            gap: 2rem;
            color: white;
        }

        .user-name {
            font-weight: 600;
        }

        .btn {
            padding: 0.6rem 1.5rem;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            text-decoration: none;
        }

        .btn-logout {
            background: #ff69b4;
            color: white;
        }

        .btn-logout:hover {
            background: #ff1493;
            transform: scale(1.05);
        }

        /* Search Section */
        /*
            Search area includes a free-text search input and simple filters for
            category and price. The search hooks into `filterProducts()` to update
            the product grid in real time.
        */
        .search-section {
            background: white;
            padding: 2rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 2rem;
        }

        .search-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            align-items: center;
        }

        .search-input {
            flex: 1;
            min-width: 250px;
            padding: 0.8rem 1rem;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .search-input:focus {
            outline: none;
            border-color: #ff69b4;
        }

        .filter-group {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .filter-select {
            padding: 0.8rem 1rem;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            transition: border-color 0.3s ease;
        }

        .filter-select:focus {
            outline: none;
            border-color: #ff69b4;
        }

        .btn-search {
            padding: 0.8rem 2rem;
            background: linear-gradient(135deg, #ff69b4, #ff1493);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .btn-search:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(255, 20, 147, 0.4);
        }

        /* Main Content */
        /*
            The main content area contains the product listing grid. The products
            are generated dynamically by JavaScript (see `loadProducts`).
        */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        .products-section {
            margin-top: 2rem;
        }

        .section-title {
            font-size: 2rem;
            margin-bottom: 2rem;
            color: #333;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 2rem;
        }

        .product-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
         
</head>
<body>
    <!-- Navigation Bar -->
    <nav>
        <div class="logo" onclick="goHome()" title="GlamourGlow - Home" aria-label="GlamourGlow Home">GlamourGlow</div>
        <div class="nav-info">
            <span class="user-name" id="userDisplay">Welcome, User!</span>
            <span class="cart-indicator" id="cartCount" onclick="openCartModal()" style="cursor:pointer;">Cart: 0</span>
            <button class="btn" onclick="openOrdersModal()" title="View your orders">My Orders <span id="ordersCount" class="orders-badge">0</span></button>
            <button type="button" class="btn btn-logout" onclick="logout()">Logout</button>
        </div>
    </nav>

    <!-- Search Section -->
    <div class="search-section">
        <div class="search-container">
            <input 
                type="text" 
                class="search-input" 
                id="searchInput" 
                placeholder="Search products (e.g., lipstick, foundation, palette...)"
                onkeyup="filterProducts()"
            >
            <div class="filter-group">
                <select class="filter-select" id="categoryFilter" onchange="filterProducts()">
                    <option value="">All Categories</option>
                    <option value="lipstick">Lipstick</option>
                    <option value="highlighter">Highlighter</option>
                    <option value="palette">Palette</option>
                    <option value="foundation">Foundation</option>
                    <option value="blush">Blush</option>
                    <option value="eyeliner">Eyeliner</option>
                </select>
                <select class="filter-select" id="priceFilter" onchange="filterProducts()">
                    <option value="">All Prices</option>
                    <option value="0-200">Under ₱200</option>
                    <option value="200-3000">₱200 - ₱3000</option>
                    <option value="3000-5000">₱3000 - ₱5000</option>
                    <option value="5000+">₱5000+</option>
                </select>
                <button class="btn-search" onclick="filterProducts()">Search</button>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <div class="container">
        <h2 class="section-title">All Products</h2>
        <div class="products-grid" id="productsGrid">
            <!-- Products will be dynamically loaded here -->
        </div>
        <div id="noResults" class="no-results" style="display: none;">
            No products found. Try adjusting your search filters.
        </div>
    </div>

    <!-- Cart Modal -->
    <!--
        The cart modal displays items added by the user. It supports quantity
        editing, removing items and a simple checkout which saves orders to
        `localStorage` under the `orders` key (demo purpose only).
    -->
    <div id="cartModal" class="cart-modal">
        <div class="cart-modal-content">
            <div class="cart-header">
                <h2>Your Cart</h2>
                <button class="btn" onclick="closeCartModal()">Close</button>
            </div>
            <div class="cart-items" id="cartItemsContainer">
                <!-- Items loaded dynamically -->
            </div>
            <div class="cart-total">
                <div>Total</div>
                <div id="cartTotal">₱0.00</div>
            </div>
            <div style="margin-top:1rem; display:flex; gap:0.5rem; justify-content:flex-end;">
                <button class="btn" onclick="closeCartModal()">Continue Shopping</button>
                <button class="btn btn-logout" onclick="checkout()">Buy / Checkout</button>
            </div>
        </div>
    </div>

    <!-- Orders Modal -->
    <div id="ordersModal" class="cart-modal">
        <div class="cart-modal-content">
            <div class="cart-header">
                <h2>Your Orders</h2>
                <button class="btn" onclick="closeOrdersModal()">Close</button>
            </div>
            <div id="ordersContainer">
                <!-- Orders loaded dynamically -->
            </div>
            <div style="margin-top:1rem; display:flex; gap:0.5rem; justify-content:flex-end;">
                <button class="btn" onclick="closeOrdersModal()">Done</button>
            </div>
        </div>
    </div>

    <!-- Order Details Modal -->
    <div id="orderDetailsModal" class="cart-modal">
        <div class="cart-modal-content">
            <div class="cart-header">
                <h2>Order Details</h2>
                <button class="btn" onclick="closeOrderDetailsModal()">Close</button>
            </div>
            <div id="orderDetailsContainer">
                <!-- Detailed order content will be injected here -->
            </div>
            <div style="margin-top:1rem; display:flex; gap:0.5rem; justify-content:flex-end;">
                <button class="btn" onclick="closeOrderDetailsModal()">Done</button>
            </div>
        </div>
    </div>
/ Cart (kept in JS runtime and persisted to localStorage when changed)
        let cart = [];
        // currentUser is read from localStorage which is set during login/signup in `project.html`.
        let currentUser = localStorage.getItem('currentUser') || 'Guest';

        
        /*
            init()
            - Guard: if no `currentUser` is set, treat the page as protected and
              redirect back to the public `project.html`.
            - Otherwise set the welcome text and load products + cart from storage.
        */
        function init() {
            if (!localStorage.getItem('currentUser')) {
                window.location.href = 'project.html';
                return;
            }
            document.getElementById('userDisplay').textContent = `Welcome, ${currentUser}!`;
            loadProducts(products);
            loadCart();
            updateOrdersCount();
            // close details modal if open
            try { closeOrderDetailsModal(); } catch(err) { /* ignore */ }
        }

    
                /*
                        loadProducts(productsToLoad)
                        - Renders a list of product cards into `#productsGrid`.
                        - Each card contains image, description, price, quantity controls and
                            an "Add to Cart" button that calls `addToCart(productId)`.
                */
                function loadProducts(productsToLoad) {
            const grid = document.getElementById('productsGrid');
            const noResults = document.getElementById('noResults');
            
            if (productsToLoad.length === 0) {
                grid.style.display = 'none';
                noResults.style.display = 'block';
                return;
            }
            
            grid.style.display = 'grid';
            noResults.style.display = 'none';
            grid.innerHTML = '';

            productsToLoad.forEach(product => {
                const card = document.createElement('div');
                card.className = 'product-card';
                card.innerHTML = `
                    <div class="product-image">
                        <img src="${product.image}" alt="${product.name}">
                    </div>
                    <div class="product-info">
                        <div class="product-name">${product.name}</div>
                        <p class="product-description">${product.description}</p>
                        <div class="price-section">
                            <span class="product-price">₱${product.price.toFixed(2)}</span>
                            <span class="product-rating">⭐⭐⭐⭐⭐ (${product.reviews})</span>
                        </div>
                        <div class="product-quantity">
                            <button class="quantity-btn" onclick="decreaseQty(${product.id})">-</button>
                            <input type="number" class="quantity-input" id="qty-${product.id}" value="1" min="1">
                            <button class="quantity-btn" onclick="increaseQty(${product.id})">+</button>
                        </div>
                        <button class="btn-add-cart" onclick="addToCart(${product.id})">Add to Cart</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        
        /*
            filterProducts()
            - Reads search input and filter selects, filters the `products` array
            - Calls `loadProducts` with the filtered results.
        */
        function filterProducts() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const categoryFilter = document.getElementById('categoryFilter').value;
            const priceFilter = document.getElementById('priceFilter').value;

            let filtered = products.filter(product => {
                const matchesSearch = product.name.toLowerCase().includes(searchTerm) || 
                                    product.description.toLowerCase().includes(searchTerm) ||
                                    product.category.toLowerCase().includes(searchTerm);
                
                const matchesCategory = !categoryFilter || product.category === categoryFilter;
                
                let matchesPrice = true;
                if (priceFilter) {
                    if (priceFilter === '0-100') matchesPrice = product.price < 100;
                    else if (priceFilter === '100-300') matchesPrice = product.price >= 20 && product.price < 30;
                    else if (priceFilter === '300-600') matchesPrice = product.price >= 30 && product.price < 50;
                    else if (priceFilter === '600+') matchesPrice = product.price >= 50;
                }

                return matchesSearch && matchesCategory && matchesPrice;
            });

            loadProducts(filtered);
        }

        
        // increaseQty / decreaseQty: change the quantity input value on product cards
        function increaseQty(id) {
            const input = document.getElementById(`qty-${id}`);
            input.value = parseInt(input.value) + 1;
        }

        function decreaseQty(id) {
            const input = document.getElementById(`qty-${id}`);
            if (parseInt(input.value) > 1) {
                input.value = parseInt(input.value) - 1;
            }
        }

        
                /*
                        addToCart(productId)
                        - Adds the selected product and quantity to the in-memory `cart` array.
                        - Persists the cart using `saveCart()` and opens the cart modal to
                            allow review before final checkout.
                */
                function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const quantity = parseInt(document.getElementById(`qty-${productId}`).value);
            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({
                    ...product,
                    quantity: quantity
                });
            }

            saveCart();
            // Update cart UI and open cart modal so user can review
            renderCart();
            openCartModal();
            document.getElementById(`qty-${productId}`).value = 1;
        }

        
        // saveCart/loadCart/updateCartCount: helper functions to persist and show cart state
        function saveCart() {
            localStorage.setItem('cart', JSON.stringify(cart));
            updateCartCount();
        }

        function loadCart() {
            const savedCart = localStorage.getItem('cart');
            if (savedCart) {
                cart = JSON.parse(savedCart);
            }
            updateCartCount();
        }

        function updateCartCount() {
            const count = cart.reduce((total, item) => total + item.quantity, 0);
            document.getElementById('cartCount').textContent = `Cart: ${count}`;
        }

        // Cart UI functions
        /*
            Cart modal controls and utilities
            - openCartModal / closeCartModal: show or hide the cart modal
            - renderCart: populate the cart modal with items, calculate total
            - removeFromCart: remove a specific item by id
            - changeCartQty: handle quantity edits made inside the cart modal
            - checkout: create a simple order object, persist it to localStorage,
              clear the cart and confirm to the user
        */
        function openCartModal() {
            document.getElementById('cartModal').style.display = 'flex';
            renderCart();
        }

        function closeCartModal() {
            document.getElementById('cartModal').style.display = 'none';
        }

        // Orders view & cancel flow
        function openOrdersModal() {
            document.getElementById('ordersModal').style.display = 'flex';
            renderOrders();
        }

        function closeOrdersModal() {
            document.getElementById('ordersModal').style.display = 'none';
        }

        function renderOrders() {
            const container = document.getElementById('ordersContainer');
            const allOrders = JSON.parse(localStorage.getItem('orders') || '[]');
            const orders = allOrders.filter(o => o.user === currentUser);
            container.innerHTML = '';
            if (!orders || orders.length === 0) {
                container.innerHTML = '<p style="color:#666; padding:1rem 0">You have no orders yet.</p>';
                return;
            }

            orders.slice().reverse().forEach(order => {
                const el = document.createElement('div');
                el.style.borderBottom = '1px solid #eee';
                el.style.padding = '0.75rem 0';
                const itemsList = order.items.map(it => `${it.name} x ${it.quantity}`).join(', ');
                el.innerHTML = `
                    <div style="display:flex; justify-content:space-between; align-items:center; gap:1rem;">
                        <div style="flex:1">
                            <div style="font-weight:700">Order #${order.id}</div>
                            <div style="color:#666; font-size:0.9rem">${new Date(order.createdAt).toLocaleString()}</div>
                            <div style="margin-top:0.5rem; color:#333">${itemsList}</div>
                        </div>
                        <div style="text-align:right; min-width:150px;">
                            <div style="font-weight:700">₱${order.total.toFixed(2)}</div>
                            <div style="color:#666; font-size:0.9rem; margin-bottom:0.4rem">Status: <span id="status-${order.id}">${order.status || 'processing'}</span></div>
                            <div style="display:flex;gap:6px;justify-content:flex-end"><button class="btn btn-logout" onclick="cancelOrder(${order.id})">Cancel Order</button><button class="btn" onclick="openOrderDetails(${order.id})">View Details</button></div>
                        </div>
                    </div>
                `;
                container.appendChild(el);
            });
        }

        function cancelOrder(id) {
            if (!confirm('Cancel order? This will permanently remove this order.')) return;
            const orders = JSON.parse(localStorage.getItem('orders') || '[]');
            const idx = orders.findIndex(o => o.id === id);
            if (idx === -1) {
                alert('Order not found');
                return;
            }
            if (orders[idx].user !== currentUser) {
                alert('You can only cancel your own orders.');
                return;
            }
            // Remove the order entirely from storage
            orders.splice(idx, 1);
            localStorage.setItem('orders', JSON.stringify(orders));
            renderOrders();
            updateOrdersCount();
            alert('Order canceled and removed.');
        }

        function renderCart() {
            const container = document.getElementById('cartItemsContainer');
            const totalEl = document.getElementById('cartTotal');
            container.innerHTML = '';
            if (!cart || cart.length === 0) {
                // Show an empty-cart placeholder
                container.innerHTML = '<p style="color:#666; padding:1rem 0">Your cart is empty.</p>';
                totalEl.textContent = '₱0.00';
                updateCartCount();
                return;
            }

            let total = 0;
            cart.forEach(item => {
                const el = document.createElement('div');
                el.className = 'cart-item';
                el.innerHTML = `
                    <img src="${item.image}" alt="${item.name}">
                    <div style="flex:1">
                        <div class="cart-item-name">${item.name}</div>
                        <div style="color:#666">₱${item.price.toFixed(2)} x ${item.quantity}</div>
                    </div>
                    <div class="cart-actions">
                        <input type="number" min="1" value="${item.quantity}" onchange="changeCartQty(${item.id}, this.value)" style="width:60px;padding:6px;border-radius:6px;border:1px solid #ddd">
                        <button class="btn" onclick="removeFromCart(${item.id})" style="background:#ff69b4;color:white;border:none;padding:6px;border-radius:6px;cursor:pointer">Remove</button>
                    </div>
                `;
                container.appendChild(el);
                total += item.price * item.quantity;
            });

            totalEl.textContent = `₱${total.toFixed(2)}`;
            updateCartCount();
            // update orders button if we want to show new count or status followup
        }

        function removeFromCart(id) {
            cart = cart.filter(i => i.id !== id);
            saveCart();
            renderCart();
        }

        function changeCartQty(id, value) {
            const qty = parseInt(value);
            if (isNaN(qty) || qty < 1) return;
            const item = cart.find(i => i.id === id);
            if (!item) return;
            item.quantity = qty;
            saveCart();
            renderCart();
        }

        function checkout() {
            if (!cart || cart.length === 0) {
                alert('Your cart is empty.');
                return;
            }
            const total = cart.reduce((s, it) => s + it.price * it.quantity, 0);
            // Save order to localStorage (simple mock order)
            const orders = JSON.parse(localStorage.getItem('orders') || '[]');
            const order = {
                id: Date.now(),
                user: currentUser,
                items: cart,
                total: total,
                status: 'processing', // processing by default
                createdAt: new Date().toISOString()
            };
            orders.push(order);
            localStorage.setItem('orders', JSON.stringify(orders));

            // Clear cart and show confirmation
            cart = [];
            saveCart();
            renderCart();
            closeCartModal();
            alert('Thank you! Your order has been placed.');
            // Optional: show orders modal or update UI
            // openOrdersModal();
            updateOrdersCount();
        }

    
        // logout: clear user session and cart then redirect to public homepage
        function logout() {
            localStorage.removeItem('currentUser');
            localStorage.removeItem('cart');
            window.location.href = 'project.html';
        }

        
        function goHome() {
            window.location.reload();
        }

        function updateOrdersCount() {
            const allOrders = JSON.parse(localStorage.getItem('orders') || '[]');
            const count = allOrders.filter(o => o.user === currentUser).length;
            const el = document.getElementById('ordersCount');
            if (el) el.textContent = count;
        }

        function openOrderDetails(orderId) {
            const allOrders = JSON.parse(localStorage.getItem('orders') || '[]');
            const order = allOrders.find(o => o.id === orderId);
            if (!order) {
                alert('Order not found');
                return;
            }
            const container = document.getElementById('orderDetailsContainer');
            container.innerHTML = '';
            // build order detail lines
            const header = document.createElement('div');
            header.style.marginBottom = '0.75rem';
            header.innerHTML = `<div style="font-weight:700">Order #${order.id} - ${new Date(order.createdAt).toLocaleString()}</div><div style="color:#666">Status: ${order.status}</div>`;
            container.appendChild(header);
            order.items.forEach(it => {
                const row = document.createElement('div');
                row.style.display = 'flex';
                row.style.gap = '1rem';
                row.style.alignItems = 'center';
                row.style.padding = '0.4rem 0';
                row.innerHTML = `
                    <img src="${it.image}" alt="${it.name}" style="width:60px;height:60px;object-fit:cover;border-radius:6px">
                    <div style="flex:1;">
                        <div style="font-weight:600">${it.name}</div>
                        <div style="color:#666; font-size:0.9rem">${it.quantity} x ₱${it.price.toFixed(2)}</div>
                    </div>
                    <div style="font-weight:700">₱${(it.price * it.quantity).toFixed(2)}</div>
                `;
                container.appendChild(row);
            });
            const total = document.createElement('div');
            total.style.marginTop = '0.9rem';
            total.style.fontWeight = '700';
            total.style.textAlign = 'right';
            total.textContent = `Total: ₱${order.total.toFixed(2)}`;
            container.appendChild(total);
            // Add a cancel button if allowed
            const actionRow = document.createElement('div');
            actionRow.style.marginTop = '0.6rem';
            actionRow.style.textAlign = 'right';
            actionRow.innerHTML = `<button class="btn btn-logout" onclick="cancelOrder(${order.id})">Cancel Order</button>`;
            container.appendChild(actionRow);
            document.getElementById('orderDetailsModal').style.display = 'flex';
        }

        function closeOrderDetailsModal() {
            document.getElementById('orderDetailsModal').style.display = 'none';
            document.getElementById('orderDetailsContainer').innerHTML = '';
        }

        
        window.onload = init;
    </script>
</body>
</html>
   
