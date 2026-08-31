<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Devartsx | Premium 3D Art Studio</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.1/vanilla-tilt.min.js"></script>

    <style>
        :root {
            --bg-dark: #08090d;
            --card-bg: rgba(20, 22, 32, 0.75);
            --accent-yellow: #facc15;
            --accent-gold: #eab308;
            --accent-glow: rgba(250, 204, 21, 0.35);
            --text-main: #ffffff;
            --text-muted: #d4d4d8;
            --border-color: rgba(250, 204, 21, 0.25);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; scroll-behavior: smooth; }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            overflow-x: hidden;
            position: relative;
        }

        /* ---------------- Fullscreen Opening Animation Intro ---------------- */
        #intro-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: #050608;
            z-index: 99999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.8s cubic-bezier(0.4, 0, 0.2, 1), visibility 0.8s;
        }

        #intro-screen.hide {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }

        .intro-box {
            text-align: center;
            transform: scale(0.8);
            animation: introPop 1.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        .intro-title {
            font-size: 3.2rem;
            font-weight: 800;
            color: #ffffff;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .intro-title span {
            color: var(--accent-yellow);
            text-shadow: 0 0 25px var(--accent-yellow), 0 0 50px var(--accent-yellow);
        }

        .intro-line {
            width: 0%;
            height: 4px;
            background: linear-gradient(90deg, transparent, var(--accent-yellow), transparent);
            margin: 18px auto 0;
            border-radius: 4px;
            box-shadow: 0 0 15px var(--accent-yellow);
            animation: lineExpand 1.5s ease-in-out forwards 0.3s;
        }

        @keyframes introPop {
            0% { transform: scale(0.7); opacity: 0; filter: blur(10px); }
            100% { transform: scale(1); opacity: 1; filter: blur(0px); }
        }

        @keyframes lineExpand {
            0% { width: 0%; }
            100% { width: 80%; }
        }

        /* ---------------- 3D WebGL Background Canvas ---------------- */
        #webgl-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            pointer-events: none;
        }

        /* ---------------- Glassmorphic Navbar ---------------- */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px 8%;
            background: rgba(8, 9, 13, 0.85);
            backdrop-filter: blur(16px);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid var(--border-color);
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 12px;
            text-decoration: none;
        }

        .logo-icon {
            font-size: 1.8rem;
            color: var(--accent-yellow);
            filter: drop-shadow(0 0 10px var(--accent-yellow));
        }

        .logo-text {
            font-size: 1.7rem;
            font-weight: 800;
            letter-spacing: 1px;
            color: #ffffff;
            text-shadow: 0 0 12px rgba(250, 204, 21, 0.4);
        }

        .logo-text span { color: var(--accent-yellow); }

        .nav-links { display: flex; gap: 28px; list-style: none; }
        .nav-links a { color: #ffffff; text-decoration: none; font-weight: 600; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent-yellow); text-shadow: 0 0 10px var(--accent-yellow); }

        /* ---------------- Hero Section ---------------- */
        .hero {
            padding: 170px 8% 90px;
            text-align: center;
            max-width: 900px;
            margin: 0 auto;
        }

        .badge {
            display: inline-block;
            padding: 8px 20px;
            background: rgba(250, 204, 21, 0.1);
            border: 1px solid var(--accent-yellow);
            border-radius: 30px;
            color: var(--accent-yellow);
            font-size: 0.85rem;
            font-weight: 700;
            margin-bottom: 25px;
            box-shadow: 0 0 20px var(--accent-glow);
        }

        .hero h1 { font-size: 3.6rem; font-weight: 800; line-height: 1.2; margin-bottom: 25px; color: #ffffff; }
        .hero h1 span {
            background: linear-gradient(135deg, #ffffff 20%, #facc15 80%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 35px rgba(250, 204, 21, 0.4);
        }

        .hero p { font-size: 1.15rem; color: var(--text-muted); margin-bottom: 40px; }

        .btn-primary {
            display: inline-flex;
            align-items: center;
            gap: 12px;
            padding: 16px 36px;
            background: linear-gradient(135deg, var(--accent-yellow), var(--accent-gold));
            color: #000000;
            text-decoration: none;
            font-weight: 800;
            border-radius: 50px;
            box-shadow: 0 10px 30px var(--accent-glow);
            transition: all 0.3s ease;
            position: relative;
            z-index: 5;
        }

        .btn-primary:hover { transform: translateY(-4px) scale(1.03); box-shadow: 0 15px 40px rgba(250, 204, 21, 0.6); }

        /* ---------------- Sections ---------------- */
        .section { 
            padding: 90px 8%; 
            max-width: 1200px; 
            margin: 0 auto; 
            scroll-margin-top: 80px; 
        }
        .section-header { text-align: center; margin-bottom: 60px; }
        .section-header h2 { font-size: 2.5rem; font-weight: 800; color: #ffffff; }
        .section-header h2 span { color: var(--accent-yellow); }
        .section-header p { color: var(--text-muted); margin-top: 10px; }

        /* ---------------- 3D Gallery Grid ---------------- */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 30px;
            perspective: 1000px;
        }

        .art-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 20px;
            overflow: hidden;
            backdrop-filter: blur(12px);
            transform-style: preserve-3d;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
            transition: border-color 0.3s ease;
        }

        .art-card:hover { border-color: var(--accent-yellow); box-shadow: 0 0 25px var(--accent-glow); }
        .art-card img { width: 100%; height: 380px; object-fit: cover; display: block; transform: translateZ(20px); }
        
        .art-info {
            padding: 20px;
            background: rgba(12, 14, 22, 0.95);
            border-top: 1px solid var(--border-color);
            transform: translateZ(30px);
        }
        .art-info h4 { font-size: 1.1rem; color: #ffffff; }
        .art-info p { font-size: 0.85rem; color: var(--accent-yellow); margin-top: 4px; font-weight: 600; }

        /* ---------------- 3D Pricing Grid ---------------- */
        .pricing-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); 
            gap: 35px; 
            perspective: 1000px;
        }
        
        .price-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 24px;
            padding: 45px 35px;
            text-align: center;
            backdrop-filter: blur(12px);
            transform-style: preserve-3d;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
            position: relative;
        }

        .price-card.popular {
            border-color: var(--accent-yellow);
            box-shadow: 0 0 35px var(--accent-glow);
        }

        .price-card.popular::before {
            content: 'MOST POPULAR';
            position: absolute;
            top: -14px;
            left: 50%;
            transform: translateX(-50%) translateZ(40px);
            background: linear-gradient(135deg, var(--accent-yellow), var(--accent-gold));
            color: #000;
            font-size: 0.75rem;
            font-weight: 800;
            padding: 6px 16px;
            border-radius: 20px;
        }

        .price-card h3 { font-size: 1.6rem; color: #ffffff; transform: translateZ(25px); }
        .price-card .price { font-size: 3.2rem; font-weight: 800; color: var(--accent-yellow); margin: 15px 0; transform: translateZ(35px); text-shadow: 0 0 20px var(--accent-glow); }
        .price-card ul { list-style: none; margin: 30px 0; text-align: left; transform: translateZ(20px); }
        .price-card ul li { padding: 12px 0; color: var(--text-muted); border-bottom: 1px solid rgba(255,255,255,0.06); }
        .price-card ul li i { color: var(--accent-yellow); margin-right: 12px; }

        /* ---------------- Order Form ---------------- */
        .form-box {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 24px;
            padding: 45px;
            max-width: 650px;
            margin: 0 auto;
            backdrop-filter: blur(12px);
            box-shadow: 0 25px 50px rgba(0,0,0,0.7);
            position: relative;
            z-index: 10;
        }

        .form-group { margin-bottom: 24px; text-align: left; position: relative; z-index: 10; }
        .form-group label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 0.9rem; color: #ffffff; }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 15px 18px;
            background: rgba(10, 11, 16, 0.95);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            color: #ffffff;
            font-size: 1rem;
            outline: none;
            transition: 0.3s;
            position: relative;
            z-index: 10;
        }

        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            border-color: var(--accent-yellow);
            box-shadow: 0 0 15px var(--accent-glow);
        }

        .btn-submit {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #25d366, #128c7e);
            color: #ffffff;
            border: none;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 800;
            cursor: pointer;
            transition: 0.3s;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            box-shadow: 0 10px 25px rgba(37, 211, 102, 0.3);
            position: relative;
            z-index: 10;
        }

        .btn-submit:hover { opacity: 0.95; transform: translateY(-3px); box-shadow: 0 15px 35px rgba(37, 211, 102, 0.5); }

        /* Floating WhatsApp Icon */
        .float-wa {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #25d366;
            color: #fff;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2rem;
            box-shadow: 0 10px 25px rgba(37, 211, 102, 0.5);
            text-decoration: none;
            z-index: 1000;
            transition: 0.3s;
        }
        .float-wa:hover { transform: scale(1.15) rotate(10deg); }

        footer { text-align: center; padding: 40px; border-top: 1px solid var(--border-color); color: var(--text-muted); font-size: 0.9rem; }

        @media (max-width: 768px) {
            .hero h1 { font-size: 2.3rem; }
            .intro-title { font-size: 2.1rem; }
            .nav-links { display: none; }
            .form-box { padding: 25px; }
        }
    </style>
</head>
<body>

    <div id="intro-screen">
        <div class="intro-box">
            <h1 class="intro-title">Welcome to <span>Devartsx</span></h1>
            <div class="intro-line"></div>
        </div>
    </div>

    <canvas id="webgl-bg"></canvas>

    <nav>
        <a href="#" class="logo-container">
            <i class="fa-solid fa-palette logo-icon"></i>
            <span class="logo-text">Devarts<span>x</span></span>
        </a>
        <ul class="nav-links">
            <li><a href="#gallery">Portfolio</a></li>
            <li><a href="#pricing">Pricing</a></li>
            <li><a href="#order">Order Sketch</a></li>
        </ul>
    </nav>

    <section class="hero">
        <span class="badge"><i class="fa-solid fa-gem"></i> Premium Yellow & White 3D Studio</span>
        <h1>Bring Your Favorite Photos To Life With <span>Handmade Art</span></h1>
        <p>Get custom, highly-detailed pencil portraits drawn with premium graphite & charcoal. Perfect for personal keepsakes and memorable gifts.</p>
        <a href="#order" class="btn-primary"><i class="fa-solid fa-paper-plane"></i> Order Your Sketch Now</a>
    </section>

    <section class="section" id="gallery">
        <div class="section-header">
            <h2>Portfolio & <span>Artworks</span></h2>
            <p>100% Hand-drawn with Premium Graphite & Charcoal Pencils</p>
        </div>
        <div class="gallery-grid">
            <div class="art-card" data-tilt data-tilt-max="15" data-tilt-speed="400">
                <img src="https://images.unsplash.com/photo-1579783900882-c0d3dad7b119?w=600" alt="Shiv Parvati Sketch">
                <div class="art-info">
                    <h4>Shiv Parvati Sketch</h4>
                    <p>Charcoal & Graphite Medium</p>
                </div>
            </div>
            <div class="art-card" data-tilt data-tilt-max="15" data-tilt-speed="400">
                <img src="https://images.unsplash.com/photo-1607604276583-eef5d076aa5f?w=600" alt="Anime Art">
                <div class="art-info">
                    <h4>Anime Art (Giyu Tomioka)</h4>
                    <p>Graphite Pencil Artwork</p>
                </div>
            </div>
            <div class="art-card" data-tilt data-tilt-max="15" data-tilt-speed="400">
                <img src="https://images.unsplash.com/photo-1578301978693-85fa9c0320b9?w=600" alt="Lord Ganesha Art">
                <div class="art-info">
                    <h4>Lord Ganesha Portrait</h4>
                    <p>Detailed Charcoal Art</p>
                </div>
            </div>
            <div class="art-card" data-tilt data-tilt-max="15" data-tilt-speed="400">
                <img src="https://images.unsplash.com/photo-1544717305-2782549b5136?w=600" alt="Hyperrealistic Eye Sketch">
                <div class="art-info">
                    <h4>Hyper-Realistic Eye Study</h4>
                    <p>Graphite Pencil Detail</p>
                </div>
            </div>
        </div>
    </section>

    <section class="section" id="pricing">
        <div class="section-header">
            <h2>Commission <span>Pricing</span></h2>
            <p>Choose the size that best fits your room or gift requirements</p>
        </div>
        <div class="pricing-grid">
            <div class="price-card" data-tilt data-tilt-max="10">
                <h3>A4 Portrait</h3>
                <p style="color:var(--text-muted); margin-top:5px;">Ideal for single faces & closeups</p>
                <div class="price">₹599</div>
                <ul>
                    <li><i class="fa-solid fa-check"></i> Size: 8.3 x 11.7 Inches</li>
                    <li><i class="fa-solid fa-check"></i> Premium Heavyweight Paper</li>
                    <li><i class="fa-solid fa-check"></i> Graphite & Charcoal Blend</li>
                    <li><i class="fa-solid fa-check"></i> Fixed Spray Protection Layer</li>
                </ul>
                <a href="#order" class="btn-primary" style="width:100%; justify-content:center;">Book A4 Size</a>
            </div>

            <div class="price-card popular" data-tilt data-tilt-max="12">
                <h3>A3 Portrait</h3>
                <p style="color:var(--text-muted); margin-top:5px;">Best for full detail & couple portraits</p>
                <div class="price">₹999</div>
                <ul>
                    <li><i class="fa-solid fa-check"></i> Size: 11.7 x 16.5 Inches</li>
                    <li><i class="fa-solid fa-check"></i> High-Detail Charcoal Depth</li>
                    <li><i class="fa-solid fa-check"></i> Premium Archival Quality Paper</li>
                    <li><i class="fa-solid fa-check"></i> Fixed Spray Protection Layer</li>
                </ul>
                <a href="#order" class="btn-primary" style="width:100%; justify-content:center;">Book A3 Size</a>
            </div>
        </div>
    </section>

    <section class="section" id="order">
        <div class="section-header">
            <h2>Place Commission <span>Request</span></h2>
            <p>Fill out the details below to initiate your portrait request</p>
        </div>
        <div class="form-box">
            <form onsubmit="sendToWhatsApp(event)">
                <div class="form-group">
                    <label for="name">Your Name</label>
                    <input type="text" id="name" required placeholder="Enter your full name">
                </div>
                <div class="form-group">
                    <label for="phone">WhatsApp Number</label>
                    <input type="tel" id="phone" required placeholder="Enter active mobile number">
                </div>
                <div class="form-group">
                    <label for="size">Artwork Size</label>
                    <select id="size" required>
                        <option value="A4 Size Portrait (₹599)">A4 Size Portrait - ₹599</option>
                        <option value="A3 Size Portrait (₹999)">A3 Size Portrait - ₹999</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="instructions">Custom Notes / Special Instructions</label>
                    <textarea id="instructions" rows="4" placeholder="Mention any extra details..."></textarea>
                </div>
                <button type="submit" class="btn-submit">
                    <i class="fa-brands fa-whatsapp" style="font-size:1.4rem;"></i> Continue Order on WhatsApp
                </button>
            </form>
        </div>
    </section>

    <a href="https://api.whatsapp.com/send?phone=917827417956" target="_blank" class="float-wa" title="Chat on WhatsApp">
        <i class="fa-brands fa-whatsapp"></i>
    </a>

    <footer>
        <p>&copy; 2026 Devartsx. All Rights Reserved. Crafted for Art Lovers.</p>
    </footer>

 </script>
</body>
</html>
