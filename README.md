<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SECRET CLUB® | Not Everyone Gets In</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --black: #000000;
            --white: #FFFFFF;
            --gold: #C9A96E;
            --dark-gray: #111111;
            --suit-spade: #FFFFFF;
            --suit-heart: #C9A96E;
            --suit-diamond: #C9A96E;
            --suit-club: #FFFFFF;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--black);
            color: var(--white);
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        /* Grain overlay */
        .grain-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 9999;
            opacity: 0.04;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='1'/%3E%3C/svg%3E");
            background-repeat: repeat;
        }

        /* Loading screen */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--black);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            transition: opacity 0.8s ease, visibility 0.8s;
        }
        .loading-screen.hidden {
            opacity: 0;
            visibility: hidden;
        }
        .loading-logo {
            font-family: 'Bebas Neue', cursive;
            font-size: 3rem;
            letter-spacing: 0.2em;
            color: var(--gold);
            display: flex;
            gap: 1rem;
        }
        .loading-suits {
            font-size: 2rem;
            display: flex;
            gap: 1.5rem;
            margin-top: 1rem;
        }
        .loading-suits span {
            animation: floatSuit 1.5s infinite alternate;
        }
        .loading-suits span:nth-child(2) { animation-delay: 0.2s; }
        .loading-suits span:nth-child(3) { animation-delay: 0.4s; }
        .loading-suits span:nth-child(4) { animation-delay: 0.6s; }

        @keyframes floatSuit {
            0% { transform: translateY(0); }
            100% { transform: translateY(-10px); }
        }

        h1, h2, h3, .logo, .cta-btn, .section-tag {
            font-family: 'Bebas Neue', cursive;
            font-weight: 400;
            letter-spacing: 0.05em;
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        /* Hero */
        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            position: relative;
            background: radial-gradient(circle at 30% 40%, rgba(201,169,110,0.08) 0%, transparent 60%);
        }
        .hero-content {
            max-width: 800px;
            z-index: 2;
            padding: 2rem;
        }
        .hero h1 {
            font-size: clamp(3rem, 10vw, 7rem);
            line-height: 0.9;
            color: var(--white);
            margin-bottom: 1rem;
            text-shadow: 0 0 30px rgba(255,255,255,0.2);
        }
        .hero p {
            font-size: 1.2rem;
            font-weight: 300;
            color: rgba(255,255,255,0.8);
            margin-bottom: 2rem;
        }
        .cta-btn {
            display: inline-block;
            background: transparent;
            border: 2px solid var(--gold);
            color: var(--gold);
            padding: 1rem 2.5rem;
            font-size: 1.2rem;
            letter-spacing: 0.1em;
            cursor: pointer;
            transition: 0.3s ease;
            text-transform: uppercase;
            text-decoration: none;
        }
        .cta-btn:hover {
            background: var(--gold);
            color: var(--black);
        }
        .card-suit-hero {
            position: absolute;
            font-size: 5rem;
            opacity: 0.05;
            user-select: none;
            pointer-events: none;
        }

        /* Sections */
        section {
            padding: 6rem 0;
        }
        .section-title {
            font-size: 3.5rem;
            text-align: center;
            margin-bottom: 3rem;
            color: var(--gold);
            position: relative;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 3px;
            background: var(--gold);
            margin: 1rem auto 0;
        }

        /* About */
        .about-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }
        .about-text h2 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
        }
        .about-text p {
            color: rgba(255,255,255,0.7);
            line-height: 1.8;
            margin-bottom: 2rem;
        }
        .about-suits {
            display: flex;
            gap: 1rem;
            font-size: 2rem;
            opacity: 0.6;
        }

        /* Countdown */
        .countdown-section {
            background: var(--dark-gray);
            text-align: center;
            padding: 4rem 0;
            border-top: 1px solid var(--gold);
            border-bottom: 1px solid var(--gold);
        }
        .follower-count {
            font-size: 4rem;
            font-weight: 700;
            color: var(--gold);
        }
        .countdown-label {
            font-size: 1rem;
            letter-spacing: 0.1em;
            text-transform: uppercase;
            color: rgba(255,255,255,0.6);
        }

        /* Products */
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 2rem;
        }
        .product-card {
            background: var(--dark-gray);
            border: 1px solid #222;
            transition: 0.3s;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }
        .product-card:hover {
            border-color: var(--gold);
            transform: translateY(-8px);
        }
        .product-img {
            width: 100%;
            height: 320px;
            background: #1a1a1a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            opacity: 0.3;
            color: var(--gold);
            background-size: cover;
            background-position: center;
        }
        .product-info {
            padding: 1.5rem;
        }
        .product-name {
            font-size: 1.4rem;
            font-family: 'Bebas Neue', cursive;
            letter-spacing: 0.05em;
            margin-bottom: 0.5rem;
        }
        .product-price {
            color: var(--gold);
            font-weight: 600;
        }
        .product-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1rem;
        }
        .size-select {
            background: transparent;
            border: 1px solid #444;
            color: white;
            padding: 0.4rem;
            font-size: 0.9rem;
        }
        .add-to-cart {
            background: var(--gold);
            border: none;
            color: black;
            padding: 0.5rem 1.2rem;
            font-weight: 700;
            cursor: pointer;
            transition: 0.2s;
            font-family: 'Inter', sans-serif;
        }
        .wishlist-btn {
            background: none;
            border: none;
            color: var(--gold);
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* Cart Drawer */
        .cart-drawer {
            position: fixed;
            top: 0;
            right: -420px;
            width: 400px;
            max-width: 90vw;
            height: 100%;
            background: #0a0a0a;
            border-left: 1px solid var(--gold);
            z-index: 10001;
            transition: right 0.4s ease;
            padding: 2rem;
            overflow-y: auto;
        }
        .cart-drawer.open {
            right: 0;
        }
        .cart-drawer h2 {
            color: var(--gold);
            margin-bottom: 2rem;
        }
        .cart-item {
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid #222;
            padding: 1rem 0;
        }
        .cart-total {
            font-size: 1.5rem;
            margin: 2rem 0;
            color: var(--gold);
        }
        .checkout-btn {
            width: 100%;
            padding: 1rem;
            background: var(--gold);
            border: none;
            color: black;
            font-weight: 700;
            font-size: 1.2rem;
            cursor: pointer;
        }
        .discount-input {
            background: #111;
            border: 1px solid #333;
            color: white;
            padding: 0.7rem;
            width: 100%;
            margin: 1rem 0;
        }
        .close-cart {
            background: none;
            border: none;
            color: white;
            font-size: 2rem;
            float: right;
            cursor: pointer;
        }

        /* Instagram mock */
        .insta-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1rem;
        }
        .insta-post {
            aspect-ratio: 1;
            background: #1a1a1a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            opacity: 0.5;
        }
        .follow-link {
            text-align: center;
            margin-top: 2rem;
        }

        /* Community */
        .community-number {
            font-size: 6rem;
            text-align: center;
            font-weight: 700;
            color: var(--gold);
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 3rem 1rem;
            border-top: 1px solid #222;
        }
        .footer-logo {
            font-size: 2rem;
            font-family: 'Bebas Neue', cursive;
            color: var(--gold);
        }
        .footer-suits {
            font-size: 1.5rem;
            margin: 1rem 0;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .about-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading-screen" id="loadingScreen">
        <div class="loading-logo">SECRET CLUB</div>
        <div class="loading-suits">
            <span>♠</span><span>♦</span><span>♣</span><span>♥</span>
        </div>
    </div>

    <!-- Grain overlay -->
    <div class="grain-overlay"></div>

    <!-- Cart Drawer -->
    <div class="cart-drawer" id="cartDrawer">
        <button class="close-cart" onclick="toggleCart()">&times;</button>
        <h2>YOUR CART</h2>
        <div id="cartItems"></div>
        <div class="cart-total" id="cartTotal">$0.00</div>
        <input type="text" class="discount-input" id="discountCode" placeholder="DISCOUNT CODE">
        <button class="checkout-btn" onclick="applyDiscount()">CHECKOUT</button>
    </div>

    <!-- Hero -->
    <section class="hero" id="hero">
        <div class="hero-content">
            <h1>NOT EVERYONE<br>GETS IN.</h1>
            <p>Streetwear from Chile. Built for those who move differently.</p>
            <a href="#join" class="cta-btn">Join The Club</a>
        </div>
        <div class="card-suit-hero" style="top:10%;left:10%">♠</div>
        <div class="card-suit-hero" style="bottom:15%;right:8%">♦</div>
    </section>

    <!-- About -->
    <section id="about">
        <div class="container">
            <h2 class="section-title">About Secret Club</h2>
            <div class="about-grid">
                <div class="about-text">
                    <h2>Born in the Shadows of Santiago</h2>
                    <p>SECRET CLUB is not a brand. It’s a membership. Every piece is limited, every drop is earned. We don’t follow trends — we create the silence before the storm. If you know, you know. If you don’t, you’re not ready.</p>
                    <div class="about-suits">♠ ♦ ♣ ♥</div>
                </div>
                <div style="background:#1a1a1a; height:350px; display:flex; align-items:center; justify-content:center; font-size:4rem; opacity:0.3;">♠</div>
            </div>
        </div>
    </section>

    <!-- Upcoming Drop / Countdown -->
    <div class="countdown-section" id="countdown">
        <div class="container">
            <h2 class="section-title" style="margin-bottom:1rem;">Upcoming Drop</h2>
            <div class="countdown-label">First drops unlock at 1,000 followers</div>
            <div class="follower-count" id="followerDisplay">847</div>
            <div class="countdown-label">Instagram Followers</div>
            <p style="margin-top:1.5rem; opacity:0.7;">We're close. Follow <strong>@secretclub_cl</strong> to unlock.</p>
        </div>
    </div>

    <!-- Featured Collection -->
    <section id="collection">
        <div class="container">
            <h2 class="section-title">Featured Collection</h2>
            <div class="product-grid" id="productGrid"></div>
        </div>
    </section>

    <!-- Join The Club -->
    <section id="join" style="background:var(--dark-gray);">
        <div class="container" style="text-align:center;">
            <h2 class="section-title">Join The Club</h2>
            <p style="max-width:500px; margin:0 auto 2rem; opacity:0.8;">Be the first to know about drops, events, and secret access. No spam, only the clandestine.</p>
            <form id="emailForm" style="display:flex; gap:1rem; justify-content:center; flex-wrap:wrap;">
                <input type="email" placeholder="your@email.com" required style="padding:1rem; width:300px; background:#111; border:1px solid #333; color:white;">
                <button type="submit" class="cta-btn">GET ACCESS</button>
            </form>
            <p id="emailMessage" style="margin-top:1rem; color:var(--gold);"></p>
        </div>
    </section>

    <!-- Instagram Integration -->
    <section id="instagram">
        <div class="container">
            <h2 class="section-title">@secretclub_cl</h2>
            <div class="insta-grid">
                <div class="insta-post">♠</div>
                <div class="insta-post">♦</div>
                <div class="insta-post">♣</div>
                <div class="insta-post">♥</div>
            </div>
            <div class="follow-link">
                <a href="#" class="cta-btn">Follow on Instagram</a>
            </div>
        </div>
    </section>

    <!-- Community -->
    <section id="community">
        <div class="container" style="text-align:center;">
            <h2 class="section-title">The Inner Circle</h2>
            <div class="community-number">2,418</div>
            <p style="opacity:0.7;">Members worldwide</p>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="footer-logo">SECRET CLUB®</div>
        <div class="footer-suits">♠ ♦ ♣ ♥</div>
        <p>"Not Everyone Gets In."</p>
        <p><a href="#" style="color:var(--gold); text-decoration:none;">Instagram</a> | <a href="mailto:info@secretclub.cl" style="color:var(--gold);">info@secretclub.cl</a></p>
        <p style="font-size:0.8rem; opacity:0.5;">© 2026 SECRET CLUB®. All rights reserved.</p>
    </footer>

    <script>
        // Loading screen
        window.addEventListener('load', () => {
            setTimeout(() => {
                document.getElementById('loadingScreen').classList.add('hidden');
            }, 2000);
        });

        // Simulated follower count (gradually increases until 1000 unlock)
        let followers = 847;
        const followerDisplay = document.getElementById('followerDisplay');
        setInterval(() => {
            if (followers < 1000) {
                followers += Math.floor(Math.random() * 3) + 1;
                if (followers > 1000) followers = 1000;
                followerDisplay.textContent = followers;
            }
        }, 5000);

        // Product data
        const products = [
            { id: 1, name: "Oversized Hoodie", price: 89.99, img: "♠", sizes: ["S","M","L","XL"] },
            { id: 2, name: "Essential Tee", price: 44.99, img: "♦", sizes: ["S","M","L","XL"] },
            { id: 3, name: "Club Cap", price: 34.99, img: "♣", sizes: ["One Size"] },
            { id: 4, name: "Card Holder", price: 29.99, img: "♥", sizes: ["One Size"] }
        ];

        let cart = [];
        let wishlist = JSON.parse(localStorage.getItem('secretclub_wishlist')) || [];

        function renderProducts() {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = products.map(p => `
                <div class="product-card">
                    <div class="product-img">${p.img}</div>
                    <div class="product-info">
                        <div class="product-name">${p.name}</div>
                        <div class="product-price">$${p.price.toFixed(2)}</div>
                        <div class="product-actions">
                            <select class="size-select" id="size-${p.id}">
                                ${p.sizes.map(s => `<option>${s}</option>`).join('')}
                            </select>
                            <button class="add-to-cart" onclick="addToCart(${p.id})">ADD</button>
                            <button class="wishlist-btn" onclick="toggleWishlist(${p.id})">${wishlist.includes(p.id) ? '♥' : '♡'}</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const sizeSelect = document.getElementById(`size-${productId}`);
            const size = sizeSelect ? sizeSelect.value : 'M';
            cart.push({ ...product, size });
            updateCartUI();
        }

        function updateCartUI() {
            const cartItems = document.getElementById('cartItems');
            const totalEl = document.getElementById('cartTotal');
            cartItems.innerHTML = cart.map((item, index) => `
                <div class="cart-item">
                    <div><strong>${item.name}</strong> (${item.size})</div>
                    <div>$${item.price.toFixed(2)} <span onclick="removeFromCart(${index})" style="cursor:pointer; color:red;">&times;</span></div>
                </div>
            `).join('');
            const total = cart.reduce((sum, item) => sum + item.price, 0);
            totalEl.textContent = `$${total.toFixed(2)}`;
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function toggleCart() {
            document.getElementById('cartDrawer').classList.toggle('open');
        }

        function applyDiscount() {
            const code = document.getElementById('discountCode').value.trim();
            if (code === 'SECRET10') {
                alert('10% discount applied! (Demo: total reduced)');
            } else {
                alert('Invalid code');
            }
        }

        function toggleWishlist(productId) {
            if (wishlist.includes(productId)) {
                wishlist = wishlist.filter(id => id !== productId);
            } else {
                wishlist.push(productId);
            }
            localStorage.setItem('secretclub_wishlist', JSON.stringify(wishlist));
            renderProducts();
        }

        // Email capture
        document.getElementById('emailForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const email = e.target.querySelector('input').value;
            document.getElementById('emailMessage').textContent = 'Welcome to the club. Check your inbox.';
            e.target.reset();
        });

        // Cart icon in hero? We'll add a floating cart button
        const cartButton = document.createElement('div');
        cartButton.innerHTML = '🛒';
        cartButton.style.cssText = 'position:fixed; top:20px; right:20px; font-size:2rem; cursor:pointer; z-index:10001; background:#000; border:1px solid var(--gold); padding:0.5rem; border-radius:50%;';
        cartButton.onclick = toggleCart;
        document.body.appendChild(cartButton);

        // Init
        renderProducts();
        updateCartUI();
    </script>
</body>
</html>
