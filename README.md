# Yemi-Threads
 Crotchet website created with HTML, CSS and JavaScript



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yemi Threads - Handmade Crochet Elegance</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-pink: #f8b2d0;
            --secondary-pink: #f4a3c7;
            --accent-pink: #e691b5;
            --light-pink: #fdf2f8;
            --dusty-pink: #d1869b;
            --dark-pink: #be7591;
            --white: #ffffff;
            --text-dark: #2d2d2d;
            --text-light: #666666;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Inter', sans-serif;
            line-height: 1.6;
            color: var(--text-dark);
            overflow-x: hidden;
        }

        /* Header Styles */
        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            z-index: 1000;
            transition: all 0.3s ease;
        }

        .header.scrolled {
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 2rem;
            font-weight: 700;
            color: var(--dark-pink);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .logo:hover {
            color: var(--accent-pink);
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            text-decoration: none;
            color: var(--text-dark);
            font-weight: 500;
            transition: color 0.3s ease;
            position: relative;
        }

        .nav-links a:hover {
            color: var(--dark-pink);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: -5px;
            left: 0;
            background: var(--primary-pink);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .hamburger {
            display: none;
            flex-direction: column;
            cursor: pointer;
            gap: 4px;
        }

        .hamburger span {
            width: 25px;
            height: 3px;
            background: var(--dark-pink);
            transition: all 0.3s ease;
        }

        .mobile-menu {
            position: fixed;
            top: 0;
            right: -100%;
            width: 300px;
            height: 100vh;
            background: var(--white);
            box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
            transition: right 0.3s ease;
            z-index: 999;
            padding: 6rem 2rem 2rem;
        }

        .mobile-menu.active {
            right: 0;
        }

        .mobile-menu ul {
            list-style: none;
        }

        .mobile-menu a {
            display: block;
            padding: 1rem 0;
            color: var(--text-dark);
            text-decoration: none;
            font-size: 1.1rem;
            border-bottom: 1px solid var(--light-pink);
            transition: color 0.3s ease;
        }

        .mobile-menu a:hover {
            color: var(--dark-pink);
        }

        /* Hero Section */
        .hero {
            min-height: 100vh;
            background: linear-gradient(135deg, var(--light-pink) 0%, #fce7f3 50%, var(--primary-pink) 100%);
            display: flex;
            align-items: center;
            padding: 6rem 2rem 2rem;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(248, 178, 208, 0.3) 0%, transparent 70%);
            animation: float 20s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .hero-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
            position: relative;
            z-index: 1;
        }

        .hero-content h1 {
            font-family: 'Playfair Display', serif;
            font-size: 3.5rem;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 1.5rem;
            line-height: 1.2;
            opacity: 0;
            animation: slideInUp 1s ease 0.2s forwards;
        }

        .hero-content p {
            font-size: 1.2rem;
            color: var(--text-light);
            margin-bottom: 2.5rem;
            opacity: 0;
            animation: slideInUp 1s ease 0.4s forwards;
        }

        .cta-button {
            display: inline-block;
            background: linear-gradient(135deg, var(--primary-pink), var(--accent-pink));
            color: var(--white);
            padding: 1rem 2.5rem;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            text-decoration: none;
            cursor: pointer;
            transition: all 0.3s ease;
            opacity: 0;
            animation: slideInUp 1s ease 0.6s forwards;
            box-shadow: 0 4px 15px rgba(248, 178, 208, 0.4);
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(248, 178, 208, 0.6);
        }

        .hero-image {
            text-align: center;
            opacity: 0;
            animation: slideInRight 1s ease 0.8s forwards;
        }

        .hero-image img {
            width: 100%;
            max-width: 500px;
            height: 400px;
            object-fit: cover;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            background: linear-gradient(135deg, var(--light-pink), var(--primary-pink));
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideInRight {
            from {
                opacity: 0;
                transform: translateX(50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        /* Section Styles */
        .section {
            padding: 6rem 2rem;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .section-title {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            font-weight: 600;
            text-align: center;
            margin-bottom: 3rem;
            color: var(--text-dark);
        }

        /* Bestsellers Section */
        .bestsellers {
            background: var(--white);
        }

        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .product-card {
            background: var(--white);
            border-radius: 20px;
            padding: 1.5rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .product-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(248, 178, 208, 0.2), transparent);
            transition: left 0.5s ease;
        }

        .product-card:hover::before {
            left: 100%;
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        .product-image {
            width: 100%;
            height: 250px;
            background: linear-gradient(135deg, var(--light-pink), var(--primary-pink));
            border-radius: 15px;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-light);
            font-size: 1rem;
            text-align: center;
        }

        .product-name {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--text-dark);
        }

        .add-to-cart {
            width: 100%;
            background: linear-gradient(135deg, var(--secondary-pink), var(--accent-pink));
            color: var(--white);
            border: none;
            padding: 0.8rem;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .add-to-cart:hover {
            background: linear-gradient(135deg, var(--accent-pink), var(--dark-pink));
            transform: translateY(-2px);
        }

        /* Sale Banner */
        .sale-banner {
            background: linear-gradient(135deg, var(--light-pink), #fce7f3);
            position: relative;
            overflow: hidden;
        }

        .sale-container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .sale-content h2 {
            font-family: 'Playfair Display', serif;
            font-size: 2.8rem;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 1rem;
            line-height: 1.2;
        }

        .sale-content p {
            font-size: 1.2rem;
            color: var(--text-light);
            margin-bottom: 2rem;
        }

        .sale-image {
            text-align: center;
        }

        .sale-image img {
            width: 100%;
            max-width: 300px;
            height: 300px;
            object-fit: cover;
            border-radius: 20px;
            background: linear-gradient(135deg, var(--primary-pink), var(--accent-pink));
        }

        /* Info Section */
        .info-section {
            background: var(--white);
        }

        .info-container {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 4rem;
            align-items: center;
        }

        .info-text h3 {
            font-family: 'Playfair Display', serif;
            font-size: 1.8rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--text-dark);
        }

        .info-text p {
            color: var(--text-light);
            line-height: 1.7;
        }

        .info-image {
            text-align: center;
        }

        .info-image img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            border-radius: 15px;
            background: linear-gradient(135deg, var(--light-pink), var(--primary-pink));
        }

        /* Footer */
        .footer {
            background: var(--text-dark);
            color: var(--white);
            padding: 3rem 2rem;
            text-align: center;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .footer-links a {
            color: var(--white);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: var(--primary-pink);
        }

        .footer p {
            color: #999;
            font-size: 0.9rem;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .hamburger {
                display: flex;
            }

            .nav-links {
                display: none;
            }

            .hero-container {
                grid-template-columns: 1fr;
                gap: 2rem;
                text-align: center;
            }

            .hero-content h1 {
                font-size: 2.5rem;
            }

            .product-grid {
                grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                gap: 1.5rem;
            }

            .sale-container {
                grid-template-columns: 1fr;
                gap: 2rem;
                text-align: center;
            }

            .sale-content h2 {
                font-size: 2.2rem;
            }

            .info-container {
                grid-template-columns: 1fr;
                gap: 2rem;
                text-align: center;
            }

            .footer-links {
                flex-direction: column;
                gap: 1rem;
            }
        }

        @media (max-width: 480px) {
            .nav-container {
                padding: 1rem;
            }

            .hero {
                padding: 4rem 1rem 2rem;
            }

            .section {
                padding: 4rem 1rem;
            }

            .hero-content h1 {
                font-size: 2rem;
            }

            .section-title {
                font-size: 2rem;
            }
        }

        /* Animation Classes */
        .fade-in-up {
            opacity: 0;
            transform: translateY(50px);
            transition: all 0.6s ease;
        }

        .fade-in-up.visible {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header" id="header">
        <nav class="nav-container">
            <a href="#" class="logo">Yemi Threads</a>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
            <div class="hamburger" id="hamburger">
                <span></span>
                <span></span>
                <span></span>
            </div>
        </nav>
        <div class="mobile-menu" id="mobileMenu">
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="hero-container">
            <div class="hero-content">
                <h1>Handmade Crochet That Speaks Elegance</h1>
                <p>Unique crochet designs crafted with love for every occasion.</p>
                <a href="#bestsellers" class="cta-button">Shop the Collection</a>
            </div>
            <div class="hero-image">
                <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='500' height='400' viewBox='0 0 500 400'%3E%3Crect width='500' height='400' fill='%23f8b2d0'/%3E%3Ctext x='50%25' y='50%25' dominant-baseline='middle' text-anchor='middle' fill='white' font-size='20' font-family='Arial'%3EBeautiful Crochet Accessories%3C/text%3E%3C/svg%3E" alt="Handmade Crochet Accessories">
            </div>
        </div>
    </section>

    <!-- Bestsellers Section -->
    <section class="section bestsellers" id="bestsellers">
        <div class="container">
            <h2 class="section-title fade-in-up">Our Bestsellers</h2>
            <div class="product-grid">
                <div class="product-card fade-in-up">
                    <div class="product-image">Crochet Tote Bag Image Placeholder</div>
                    <h3 class="product-name">Crochet Tote Bag</h3>
                    <button class="add-to-cart">Add to Cart</button>
                </div>
                <div class="product-card fade-in-up">
                    <div class="product-image">Crochet Cat Beanie Image Placeholder</div>
                    <h3 class="product-name">Crochet Cat Beanie</h3>
                    <button class="add-to-cart">Add to Cart</button>
                </div>
                <div class="product-card fade-in-up">
                    <div class="product-image">Crochet Bucket Hat Image Placeholder</div>
                    <h3 class="product-name">Crochet Bucket Hat</h3>
                    <button class="add-to-cart">Add to Cart</button>
                </div>
                <div class="product-card fade-in-up">
                    <div class="product-image">Crochet Phone Pouch Image Placeholder</div>
                    <h3 class="product-name">Crochet Phone Pouch</h3>
                    <button class="add-to-cart">Add to Cart</button>
                </div>
            </div>
        </div>
    </section>

    <!-- Sale Banner Section -->
    <section class="section sale-banner">
        <div class="container">
            <div class="sale-container">
                <div class="sale-content fade-in-up">
                    <h2>End of Summer Sale – Up to 30% OFF</h2>
                    <p>Stylish crochet bags and accessories for your perfect look.</p>
                    <a href="#" class="cta-button">Shop Now</a>
                </div>
                <div class="sale-image fade-in-up">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300' viewBox='0 0 300 300'%3E%3Crect width='300' height='300' fill='%23e691b5'/%3E%3Ctext x='50%25' y='50%25' dominant-baseline='middle' text-anchor='middle' fill='white' font-size='16' font-family='Arial'%3ESale Products%3C/text%3E%3C/svg%3E" alt="Sale Products">
                </div>
            </div>
        </div>
    </section>

    <!-- Info Section -->
    <section class="section info-section" id="about">
        <div class="container">
            <div class="info-container">
                <div class="info-text fade-in-up">
                    <h3>Loved by Crochet Lovers</h3>
                    <p>"The quality and attention to detail in every piece is remarkable. I've never received so many compliments on my accessories before. Yemi Threads has become my go-to for unique, handmade pieces that truly stand out."</p>
                </div>
                <div class="info-image fade-in-up">
                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='250' viewBox='0 0 300 250'%3E%3Crect width='300' height='250' fill='%23f4a3c7'/%3E%3Ctext x='50%25' y='50%25' dominant-baseline='middle' text-anchor='middle' fill='white' font-size='14' font-family='Arial'%3ECrochet Aesthetic%3C/text%3E%3C/svg%3E" alt="Crochet Aesthetic">
                </div>
                <div class="info-text fade-in-up">
                    <h3>Ready to glow like never before?</h3>
                    <p>Each piece is meticulously handcrafted using premium yarns and techniques passed down through generations. Our commitment to excellence ensures that every item you receive is not just beautiful, but built to last and cherish for years to come.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer" id="contact">
        <div class="container">
            <div class="footer-links">
                <a href="#home">Home</a>
                <a href="#about">About</a>
                <a href="#contact">Contact</a>
            </div>
            <p>&copy; 2025 Yemi Threads. All rights reserved. Crafted with love and elegance.</p>
        </div>
    </footer>

    
</body>
</html>