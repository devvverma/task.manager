<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Devartsx - 3D Ultra Graphics Studio</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800;900&family=Poppins:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
            scroll-behavior: smooth;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            --bg-black: #050507;
            --bg-card: rgba(18, 18, 22, 0.75);
            --neon-yellow: #ffee00;
            --gold-yellow: #ffd700;
            --glow-yellow: rgba(255, 238, 0, 0.4);
            --text-white: #ffffff;
            --text-dim: #b0b0ba;
            --glass-border: rgba(255, 238, 0, 0.25);
        }

        body {
            background-color: var(--bg-black);
            color: var(--text-white);
            overflow-x: hidden;
            perspective: 1000px;
        }

        /* 3D Ambient Glowing Background Particles */
        .ambient-glow {
            position: fixed;
            width: 350px;
            height: 350px;
            background: radial-gradient(circle, var(--glow-yellow) 0%, rgba(0,0,0,0) 70%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 0;
            filter: blur(50px);
            animation: floatGlow 12s infinite alternate ease-in-out;
        }

        .glow-1 { top: -50px; left: -50px; }
        .glow-2 { bottom: 10%; right: -50px; animation-delay: -6s; }

        @keyframes floatGlow {
            0% { transform: translate(0, 0) scale(1); }
            50% { transform: translate(80px, 50px) scale(1.2); }
            100% { transform: translate(-40px, 100px) scale(0.9); }
        }

        /* Glassmorphism Navbar */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px 7%;
            background: rgba(8, 8, 10, 0.85);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid var(--glass-border);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.8);
        }

        .logo-box {
            display: flex;
            align-items: center;
            gap: 12px;
            text-decoration: none;
        }

        .logo-img {
            width: 48px;
            height: 48px;
            object-fit: cover;
            border-radius: 12px;
            border: 2px solid var(--neon-yellow);
            box-shadow: 0 0 15px var(--glow-yellow);
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .logo-box:hover .logo-img {
            transform: rotate(10deg) scale(1.1);
        }

        .brand-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.6rem;
            font-weight: 900;
            color: var(--text-white);
            letter-spacing: 1.5px;
            text-transform: uppercase;
        }

        .brand-title span {
            color: var(--neon-yellow);
            text-shadow: 0 0 12px var(--glow-yellow);
        }

        .nav-links {
            display: flex;
            gap: 25px;
            list-style: none;
        }

        .nav-links a {
            color: var(--text-white);
            text-decoration: none;
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.3s;
            position: relative;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0%;
            height: 2px;
            background: var(--neon-yellow);
            box-shadow: 0 0 8px var(--neon-yellow);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after { width: 100%; }
        .nav-links a:hover { color: var(--neon-yellow); }

        /* Hero 3D Section */
        .hero {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 130px 20px 80px;
            position: relative;
            z-index: 1;
        }

        .hero-badge {
            background: rgba(255, 238, 0, 0.1);
            border: 1px solid var(--neon-yellow);
            color: var(--neon-yellow);
            padding: 6px 18px;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 700;
            letter-spacing: 2px;
            text-transform: uppercase;
            margin-bottom: 25px;
            box-shadow: 0 0 15px rgba(255, 238, 0, 0.2);
            animation: pulseGlow 2s infinite alternate;
        }

        @keyframes pulseGlow {
            0% { box-shadow: 0 0 10px rgba(255, 238, 0, 0.2); }
            100% { box-shadow: 0 0 25px rgba(255, 238, 0, 0.6); }
        }

        .hero h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 3.5rem;
            font-weight: 900;
            line-height: 1.2;
            margin-bottom: 20px;
            text-transform: uppercase;
            background: linear-gradient(180deg, #ffffff 30%, var(--neon-yellow) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 25px rgba(255, 238, 0, 0.3));
        }

        .hero p {
            font-size: 1.15rem;
            color: var(--text-dim);
            max-width: 680px;
            margin-bottom: 40px;
            line-height: 1.7;
        }

        /* 3D High Graphics Animated Yellow Buttons */
        .btn-container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn-3d {
            position: relative;
            background: linear-gradient(135deg, #ffee00 0%, #ffd700 100%);
            color: #000000;
            padding: 16px 36px;
            font-size: 1rem;
            font-weight: 800;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 10px 25px rgba(255, 238, 0, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.8);
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            transform-style: preserve-3d;
        }

        .btn-3d:hover {
            transform: translateY(-5px) scale(1.05) rotateX(8deg);
            box-shadow: 0 20px 35px rgba(255, 238, 0, 0.7);
            background: linear-gradient(135deg, #ffffff 0%, #ffee00 100%);
        }

        .btn-outline-3d {
            background: transparent;
            color: var(--neon-yellow);
            border: 2px solid var(--neon-yellow);
            box-shadow: 0 0 15px rgba(255, 238, 0, 0.2);
        }

        .btn-outline-3d:hover {
            background: var(--neon-yellow);
            color: #000;
        }

        /* Titles */
        .section-title {
            text-align: center;
            margin-bottom: 60px;
            position: relative;
            z-index: 1;
        }

        .section-title h2 {
            font-family: 'Orbitron', sans-serif;
            font-size: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .section-title h2 span { color: var(--neon-yellow); }

        .title-line {
            width: 80px;
            height: 4px;
            background: var(--neon-yellow);
            margin: 12px auto 0;
            border-radius: 2px;
            box-shadow: 0 0 12px var(--neon-yellow);
        }

        /* 3D Tilt Portfolio Section */
        .portfolio-section {
            padding: 90px 7%;
            position: relative;
            z-index: 1;
        }

        .portfolio-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 35px;
        }

        .tilt-card {
            background: var(--bg-card);
            border-radius: 20px;
            border: 1px solid var(--glass-border);
            overflow: hidden;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(10px);
            transition: transform 0.1s ease, box-shadow 0.3s ease, border-color 0.3s ease;
            transform-style: preserve-3d;
            cursor: pointer;
        }

        .tilt-card:hover {
            border-color: var(--neon-yellow);
            box-shadow: 0 20px 40px rgba(255, 238, 0, 0.3);
        }

        .card-img-wrap {
            width: 100%;
            height: 340px;
            overflow: hidden;
            background: #101014;
        }

        .card-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.6s ease;
        }

        .tilt-card:hover .card-img-wrap img {
            transform: scale(1.1);
        }

        .card-body {
            padding: 24px;
            text-align: center;
        }

        .card-body h3 {
            font-size: 1.25rem;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .card-tag {
            display: inline-block;
            background: rgba(255, 238, 0, 0.12);
            color: var(--neon-yellow);
            padding: 4px 14px;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 18px;
            border: 1px solid rgba(255, 238, 0, 0.3);
        }

        /* Pricing Section */
        .pricing-section {
            padding: 90px 7%;
            position: relative;
            z-index: 1;
        }

        .pricing-container {
            display: flex;
            justify-content: center;
            gap: 40px;
            flex-wrap: wrap;
        }

        .price-card-3d {
            background: var(--bg-card);
            border: 2px solid var(--glass-border);
            border-radius: 24px;
            padding: 45px 35px;
            width: 340px;
            text-align: center;
            position: relative;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(12px);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            transform-style: preserve-3d;
        }

        .price-card-3d.popular {
            border-color: var(--neon-yellow);
            box-shadow: 0 0 35px rgba(255, 238, 0, 0.25);
            transform: scale(1.05);
        }

        .price-card-3d:hover {
            transform: translateY(-10px) scale(1.06) rotateY(4deg);
            border-color: var(--neon-yellow);
            box-shadow: 0 25px 50px rgba(255, 238, 0, 0.4);
        }

        .badge-vip {
            position: absolute;
            top: -16px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(90deg, #ffee00, #ffd700);
            color: #000;
            font-weight: 800;
            padding: 5px 20px;
            border-radius: 20px;
            font-size: 0.8rem;
            text-transform: uppercase;
            box-shadow: 0 0 15px var(--glow-yellow);
        }

        .price-size {
            font-family: 'Orbitron', sans-serif;
            font-size: 2.2rem;
            color: var(--neon-yellow);
            margin-bottom: 10px;
        }

        .price-amount {
            font-size: 2.8rem;
            font-weight: 900;
            margin-bottom: 25px;
        }

        .price-amount span {
            font-size: 1rem;
            color: var(--text-dim);
            font-weight: 400;
        }

        .price-list {
            list-style: none;
            margin-bottom: 35px;
            text-align: left;
        }

        .price-list li {
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
            color: var(--text-dim);
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .price-list li i { color: var(--neon-yellow); }

        /* Order Form Section */
        .order-section {
            padding: 90px 7%;
            position: relative;
            z-index: 1;
        }

        .form-card-3d {
            max-width: 680px;
            margin: 0 auto;
            background: var(--bg-card);
            border: 2px solid var(--glass-border);
            border-radius: 24px;
            padding: 45px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8), 0 0 30px rgba(255, 238, 0, 0.1);
            backdrop-filter: blur(15px);
        }

        .input-group { margin-bottom: 22px; }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            font-size: 0.95rem;
        }

        .form-input {
            width: 100%;
            padding: 15px 20px;
            background: rgba(5, 5, 7, 0.9);
            border: 1.5px solid rgba(255, 238, 0, 0.25);
            border-radius: 12px;
            color: var(--text-white);
            font-size: 1rem;
            outline: none;
            transition: all 0.3s ease;
        }

        .form-input:focus {
            border-color: var(--neon-yellow);
            box-shadow: 0 0 15px var(--glow-yellow);
        }

        textarea.form-input {
            resize: vertical;
            min-height: 110px;
        }

        footer {
            text-align: center;
            padding: 35px 20px;
            background: #020203;
            border-top: 1px solid var(--glass-border);
            color: var(--text-dim);
            position: relative;
            z-index: 1;
        }

        footer span { color: var(--neon-yellow); font-weight: 700; }

        @media (max-width: 900px) {
            nav { padding: 14px 5%; }
            .nav-links { display: none; }
            .hero h1 { font-size: 2.3rem; }
            .hero p { font-size: 1rem; }
            .portfolio-grid { grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); }
            .price-card-3d.popular { transform: scale(1); }
            .form-card-3d { padding: 25px; }
        }
    </style>
</head>
<body>

    <div class="ambient-glow glow-1"></div>
    <div class="ambient-glow glow-2"></div>

    <!-- Navbar -->
    <nav>
        <a href="#home" class="logo-box">
            <img src="logo.png" alt="Devartsx Logo" class="logo-img" onerror="this.src='https://via.placeholder.com/100/121216/ffee00?text=LOGO'">
            <span class="brand-title">Devarts<span>x</span></span>
        </a>
        <ul class="nav-links">
            <li><a href="#home">होम</a></li>
            <li><a href="#portfolio">पोर्टफोलियो</a></li>
            <li><a href="#pricing">प्राइस</a></li>
            <li><a href="#order">ऑर्डर इनबॉक्स</a></li>
        </ul>
    </nav>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="hero-badge">🎨 3D Ultra Graphics Sketch Studio</div>
        <h1>Devarts<span>x</span> Studio</h1>
        <p>चारकोल एवं ग्रेफाइट पेंसिल स्केच मेकिंग। प्रीमियम और हाई-ग्राफिक रियलिस्टिक स्केच जो आपकी यादों को हमेशा के लिए जीवंत बना दें!</p>
        
        <div class="btn-container">
            <a href="#portfolio" class="btn-3d"><i class="fas fa-layer-group"></i> पोर्टफोलियो देखें</a>
            <a href="#order" class="btn-3d btn-outline-3d"><i class="fab fa-whatsapp"></i> आर्डर भेजें</a>
        </div>
    </section>

    <!-- Portfolio 3D Section -->
    <section class="portfolio-section" id="portfolio">
        <div class="section-title">
            <h2>मेरा <span>पोर्टफोलियो</span></h2>
            <div class="title-line"></div>
        </div>

        <div class="portfolio-grid">
            <div class="tilt-card" onclick="selectSketch('शिव जी और पार्वती जी स्केच')">
                <div class="card-img-wrap">
                    <img src="shiv_parvati.png" alt="शिव जी और पार्वती जी स्केच">
                </div>
                <div class="card-body">
                    <h3>शिव जी और पार्वती जी स्केच</h3>
                    <span class="card-tag">चारकोल व ग्रेफाइट</span><br>
                    <a href="#order" class="btn-3d" style="padding: 8px 20px; font-size: 0.85rem;">आर्डर करें</a>
                </div>
            </div>

            <div class="tilt-card" onclick="selectSketch('एनिमे स्केच')">
                <div class="card-img-wrap">
                    <img src="anime.png" alt="एनिमे स्केच">
                </div>
                <div class="card-body">
                    <h3>एनिमे स्केच</h3>
                    <span class="card-tag">एनिमे आर्ट</span><br>
                    <a href="#order" class="btn-3d" style="padding: 8px 20px; font-size: 0.85rem;">आर्डर करें</a>
                </div>
            </div>

            <div class="tilt-card" onclick="selectSketch('रियलिस्टिक आई स्केच')">
                <div class="card-img-wrap">
                    <img src="realistic_eye.png" alt="रियलिस्टिक आई स्केच">
                </div>
                <div class="card-body">
                    <h3>रियलिस्टिक आई स्केच</h3>
                    <span class="card-tag">अल्ट्रा रियलिस्टिक</span><br>
                    <a href="#order" class="btn-3d" style="padding: 8px 20px; font-size: 0.85rem;">आर्डर करें</a>
                </div>
            </div>

            <div class="tilt-card" onclick="selectSketch('जो जो सातो स्केच')">
                <div class="card-img-wrap">
                    <img src="gojo_satoru.png" alt="जो जो सातो स्केच">
                </div>
                <div class="card-body">
                    <h3>जो जो सातो स्केच</h3>
                    <span class="card-tag">गोझो सातोरू स्केच</span><br>
                    <a href="#order" class="btn-3d" style="padding: 8px 20px; font-size: 0.85rem;">आर्डर करें</a>
                </div>
            </div>

            <div class="tilt-card" onclick="selectSketch('गणपति जी स्केच')">
                <div class="card-img-wrap">
                    <img src="ganpati.png" alt="गणपति जी स्केच">
                </div>
                <div class="card-body">
                    <h3>गणपति जी स्केच</h3>
                    <span class="card-tag">चारकोल व ग्रेफाइट</span><br>
                    <a href="#order" class="btn-3d" style="padding: 8px 20px; font-size: 0.85rem;">आर्डर करें</a>
                </div>
            </div>
        </div>
    </section>

    <!-- Pricing Section -->
    <section class="pricing-section" id="pricing">
        <div class="section-title">
            <h2>प्राइस <span>रेट कार्ड</span></h2>
            <div class="title-line"></div>
        </div>

        <div class="pricing-container">
            <div class="price-card-3d">
                <div class="price-size">A4 Size</div>
                <div class="price-amount">₹599 <span>only</span></div>
                <ul class="price-list">
                    <li><i class="fas fa-check-circle"></i> चारकोल & ग्रेफाइट स्केच</li>
                    <li><i class="fas fa-check-circle"></i> 100% हैंडमेड आर्टवर्क</li>
                    <li><i class="fas fa-check-circle"></i> सिंगल / कपल्स पोर्ट्रेट</li>
                    <li><i class="fas fa-check-circle"></i> सेफ पैकेजिंग & डिलीवरी</li>
                </ul>
                <a href="#order" class="btn-3d" onclick="selectSize('A4 Size (₹599)')">यह साइज़ चुनें</a>
            </div>

            <div class="price-card-3d popular">
                <div class="badge-vip">★ बेस्ट सेलिंग ★</div>
                <div class="price-size">A3 Size</div>
                <div class="price-amount">₹999 <span>only</span></div>
                <ul class="price-list">
                    <li><i class="fas fa-check-circle"></i> लार्ज A3 साइज़ (डबल A4)</li>
                    <li><i class="fas fa-check-circle"></i> प्रीमियम चारकोल शैडिंग</li>
                    <li><i class="fas fa-check-circle"></i> अल्ट्रा रियलिस्टिक डिटेलिंग</li>
                    <li><i class="fas fa-check-circle"></i> स्प्रे फिक्सेटिव प्रोटेक्टेड</li>
                    <li><i class="fas fa-check-circle"></i> सेफ पैकेजिंग & डिलीवरी</li>
                </ul>
                <a href="#order" class="btn-3d" onclick="selectSize('A3 Size (₹999)')">यह साइज़ चुनें</a>
            </div>
        </div>
    </section>

    <!-- WhatsApp Order Inbox Section -->
    <section class="order-section" id="order">
        <div class="section-title">
            <h2>डायरेक्ट <span>व्हाट्सएप इनबॉक्स</span></h2>
            <div class="title-line"></div>
        </div>

        <div class="form-card-3d">
            <form id="orderForm" onsubmit="sendWhatsAppOrder(event)">
                <div class="input-group">
                    <label for="name"><i class="fas fa-user-circle"></i> आपका नाम</label>
                    <input type="text" id="name" class="form-input" placeholder="अपना नाम लिखें" required>
                </div>

                <div class="input-group">
                    <label for="phone"><i class="fas fa-phone"></i> मोबाइल नंबर</label>
                    <input type="tel" id="phone" class="form-input" placeholder="फ़ोन नंबर दर्ज करें" required>
                </div>

                <div class="input-group">
                    <label for="size"><i class="fas fa-ruler-combined"></i> स्केच साइज़ चुनें</label>
                    <select id="size" class="form-input" required>
                        <option value="A4 Size - ₹599">A4 Size (₹599)</option>
                        <option value="A3 Size - ₹999">A3 Size (₹999)</option>
                    </select>
                </div>

                <div class="input-group">
                    <label for="sketchType"><i class="fas fa-palette"></i> स्केच का नाम / फोटो विवरण</label>
                    <input type="text" id="sketchType" class="form-input" placeholder="उदा. शिव पार्वती स्केच या अपनी फोटो" required>
                </div>

                <div class="input-group">
                    <label for="details"><i class="fas fa-comment-dots"></i> अतिरिक्त जानकारी</label>
                    <textarea id="details" class="form-input" placeholder="यदि कोई खास सवाल या मैसेज हो तो यहाँ लिखें..."></textarea>
                </div>

                <button type="submit" class="btn-3d" style="width: 100%; justify-content: center; font-size: 1.1rem;">
                    <i class="fab fa-whatsapp"></i> व्हाट्सएप पर मैसेज भेजें
                </button>
            </form>
        </div>
    </section>

    <footer>
        <p>© 2026 <span>Devartsx Studio</span> | व्हाट्सएप ऑर्डर: +91 7827417956</p>
    </footer>

    <!-- Interactive 3D JavaScript Animations -->
    <script>
        const cards = document.querySelectorAll('.tilt-card, .price-card-3d');

        cards.forEach(card => {
            card.addEventListener('mousemove', handleMove);
            card.addEventListener('mouseleave', handleLeave);
        });

        function handleMove(e) {
            const rect = this.getBoundingClientRect();
            const x = e.clientX - rect.left - rect.width / 2;
            const y = e.clientY - rect.top - rect.height / 2;
            const rotateX = (-y / rect.height) * 20;
            const rotateY = (x / rect.width) * 20;

            this.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateZ(10px)`;
        }

        function handleLeave() {
            this.style.transform = `perspective(1000px) rotateX(0deg) rotateY(0deg) translateZ(0px)`;
        }

        function selectSketch(name) {
            document.getElementById('sketchType').value = name;
        }

        function selectSize(val) {
            const selectEl = document.getElementById('size');
            if (val.includes('A4')) {
                selectEl.value = 'A4 Size - ₹599';
            } else if (val.includes('A3')) {
                selectEl.value = 'A3 Size - ₹999';
            }
        }

        function sendWhatsAppOrder(e) {
            e.preventDefault();

            const name = document.getElementById('name').value;
            const phone = document.getElementById('phone').value;
            const size = document.getElementById('size').value;
            const sketchType = document.getElementById('sketchType').value;
            const details = document.getElementById('details').value;

            const targetNum = "917827417956";

            let message = `*🎨 नया स्केच ऑर्डर - Devartsx Studio* %0A%0A`;
            message += `*नाम:* ${encodeURIComponent(name)}%0A`;
            message += `*मोबाइल:* ${encodeURIComponent(phone)}%0A`;
            message += `*साइज़:* ${encodeURIComponent(size)}%0A`;
            message += `*स्केच विवरण:* ${encodeURIComponent(sketchType)}%0A`;
            if (details) {
                message += `*अतिरिक्त संदेश:* ${encodeURIComponent(details)}%0A`;
            }

            const waLink = `https://wa.me/${targetNum}?text=${message}`;
            window.open(waLink, '_blank');
        }
    </script>
</body>
</html>
