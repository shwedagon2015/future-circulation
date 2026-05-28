!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Future Circulation - 一杯のコーヒーから、未来の循環を。</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400&family=Noto+Sans+JP:wght@300;400;500&display=swap" rel="stylesheet">
    
    <style>
        /* CSS Variables */
        :root {
            --bg-color: #1a1614; /* 深いコーヒーブラウン */
            --text-color: #e6dfd5; /* 温かみのあるオフホワイト */
            --accent-color: #b56b50; /* 落ち着いたテラコッタ（赤茶） */
            --border-color: rgba(230, 223, 213, 0.15);
            --font-en: 'Cormorant Garamond', serif;
            --font-jp: 'Noto Sans JP', sans-serif;
        }

        /* Reset & Base */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body, html {
            width: 100%;
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: var(--font-jp);
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
            font-feature-settings: "palt"; /* 文字詰め */
        }
        
        /* Typography */
        h1, h2, h3, h4, .en { font-family: var(--font-en); letter-spacing: 0.05em; font-weight: 400; }
        .jp-title { font-family: var(--font-jp); font-weight: 400; letter-spacing: 0.1em; line-height: 1.6; }
        p { line-height: 2.2; letter-spacing: 0.05em; font-weight: 300; color: #c4beb6; }
        
        .text-reveal { overflow: hidden; display: inline-block; }
        .text-reveal > span { display: inline-block; transform: translateY(110%); transition: transform 1.2s cubic-bezier(0.25, 1, 0.5, 1); }
        .text-reveal.active > span { transform: translateY(0); }

        /* Loader */
        .loader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100vh;
            background: var(--bg-color); z-index: 9999;
            display: flex; justify-content: center; align-items: center;
            flex-direction: column; gap: 1rem;
            transition: transform 1s cubic-bezier(0.7, 0, 0.3, 1);
        }
        .loader-text {
            font-family: var(--font-en); font-size: 2.5rem; font-weight: 400;
            letter-spacing: 0.1em; overflow: hidden;
        }
        .loader-text span {
            display: inline-block; animation: revealUp 1s cubic-bezier(0.25, 1, 0.5, 1) forwards;
        }
        @keyframes revealUp { from { transform: translateY(100%); } to { transform: translateY(0); } }

        /* WebGL Background */
        #webgl-canvas {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
            z-index: 0; pointer-events: none; opacity: 0.8;
        }

        /* Layout */
        #smooth-wrapper { width: 100%; overflow: hidden; position: relative; z-index: 10; }
        #smooth-content { will-change: transform; }

        header {
            position: fixed; top: 0; left: 0; width: 100%; padding: 2rem 4vw;
            display: flex; justify-content: space-between; align-items: center;
            z-index: 100; mix-blend-mode: difference;
        }
        .logo { font-family: var(--font-en); font-weight: 600; font-size: 1.2rem; letter-spacing: 0.1em; text-transform: uppercase; }
        .menu-btn { font-size: 0.9rem; letter-spacing: 0.1em; cursor: pointer; }

        section { padding: 8rem 4vw; position: relative; }
        .pt-0 { padding-top: 0; }
        .pb-0 { padding-bottom: 0; }

        /* Hero */
        .hero { height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; }
        .hero-title {
            font-size: clamp(2rem, 5vw, 4rem);
            margin-bottom: 2rem; mix-blend-mode: normal;
        }
        .hero-title .en { font-size: clamp(3rem, 8vw, 6rem); display: block; margin-bottom: 1rem; color: var(--accent-color);}
        .hero-desc { font-size: 1rem; max-width: 600px; margin: 0 auto; }

        /* General Image Wrapper for Parallax */
        .img-wrapper {
            position: relative; width: 100%; overflow: hidden; border-radius: 4px;
        }
        .img-parallax {
            width: 100%; height: 130%; object-fit: cover;
            position: absolute; top: -15%; left: 0;
            filter: brightness(0.85);
        }

        /* Section Layouts */
        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 6vw; align-items: center; }
        .grid-2.reverse { direction: rtl; }
        .grid-2.reverse > * { direction: ltr; }
        
        .section-header { margin-bottom: 3rem; }
        .section-header .en-label { display: block; font-family: var(--font-en); color: var(--accent-color); font-size: 1.2rem; margin-bottom: 1rem; letter-spacing: 0.1em;}
        .section-header h2 { font-size: clamp(2rem, 4vw, 3rem); }

        .text-block { margin-bottom: 2.5rem; }
        .text-block h3 { font-family: var(--font-jp); font-size: 1.2rem; margin-bottom: 1rem; color: var(--text-color); font-weight: 400;}

        /* List styling */
        .custom-list { list-style: none; margin-top: 1rem; }
        .custom-list li { position: relative; padding-left: 1.5rem; margin-bottom: 0.5rem; font-weight: 300; color: #c4beb6;}
        .custom-list li::before { content: ''; position: absolute; left: 0; top: 0.6em; width: 6px; height: 1px; background-color: var(--accent-color); }

        /* Products (Accordion Style) */
        .products-container { margin-top: 4rem; border-top: 1px solid var(--border-color); }
        .product-item {
            border-bottom: 1px solid var(--border-color);
            overflow: hidden; cursor: pointer;
            transition: background-color 0.4s ease;
        }
        .product-item:hover { background-color: rgba(255,255,255,0.02); }
        .product-header {
            padding: 3rem 0; display: flex; justify-content: space-between; align-items: center;
        }
        .product-header h3 { font-size: clamp(1.5rem, 3vw, 2.5rem); transition: color 0.4s; }
        .product-header .subtitle { font-size: 1rem; color: #8a8279; font-family: var(--font-jp); }
        .product-item:hover h3 { color: var(--accent-color); }
        
        .product-body {
            max-height: 0; opacity: 0; transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
            padding: 0 0; display: grid; grid-template-columns: 1fr 1fr; gap: 4vw;
        }
        .product-item.active .product-body {
            max-height: 500px; opacity: 1; padding: 0 0 3rem 0;
        }
        
        /* Message Area */
        .message-section { text-align: center; padding: 12rem 4vw; }
        .message-section h2 { font-size: clamp(2rem, 5vw, 4rem); margin-bottom: 2rem; line-height: 1.4; }

        /* Footer */
        footer {
            padding: 6rem 4vw 2rem; border-top: 1px solid var(--border-color);
            display: grid; grid-template-columns: 1fr 1fr; gap: 4vw;
        }
        .footer-logo { font-family: var(--font-en); font-size: 2rem; margin-bottom: 1rem; color: var(--accent-color);}
        .footer-links { display: flex; gap: 2rem; margin-top: 2rem;}
        .footer-links a {
            color: var(--text-color); text-decoration: none; font-size: 0.9rem; transition: color 0.3s;
        }
        .footer-links a:hover { color: var(--accent-color); }
        .footer-right { display: flex; flex-direction: column; justify-content: flex-end; align-items: flex-end; }
        .copyright { font-size: 0.8rem; color: #666; margin-top: 4rem;}

        /* Responsive */
        @media (max-width: 768px) {
            .grid-2 { grid-template-columns: 1fr; gap: 3rem; }
            .grid-2.reverse > * { direction: ltr; }
            .product-body { grid-template-columns: 1fr; }
            .product-header { flex-direction: column; align-items: flex-start; gap: 1rem; padding: 2rem 0;}
            footer { grid-template-columns: 1fr; text-align: center; }
            .footer-links { justify-content: center; }
            .footer-right { align-items: center; margin-top: 3rem;}
        }
    </style>

    <!-- 外部ライブラリ -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/studio-freight/lenis@1.0.29/bundled/lenis.min.js"></script>
</head>
<body>

    <!-- Loader -->
    <div class="loader">
        <div class="loader-text"><span>Future</span></div>
        <div class="loader-text"><span>Circulation</span></div>
    </div>

    <!-- WebGL Background -->
    <canvas id="webgl-canvas"></canvas>

    <!-- Header -->
    <header>
        <div class="logo">Future Circulation</div>
        <div class="menu-btn">MENU</div>
    </header>

    <!-- Smooth Scroll Container -->
    <div id="smooth-wrapper">
        <div id="smooth-content">
            
            <!-- 1. TOP (HERO) -->
            <section class="hero">
                <h1 class="hero-title jp-title">
                    <span class="text-reveal en"><span>Future Circulation</span></span>
                    <span class="text-reveal"><span>一杯のコーヒーから、</span></span><br>
                    <span class="text-reveal"><span>未来の循環を。</span></span>
                </h1>
                <div class="hero-desc gsap-fade mt-8">
                    <p>Future Circulationは、<br>ミャンマー山岳地域のコーヒーと日常文化を通して、<br>文化・ストーリー・循環を届けるブランドです。</p>
                    <p style="margin-top: 1rem;">単なるコーヒーではなく、<br>その背景にある人々の暮らしや文化を、<br>現代ギフトとして再編集しています。</p>
                </div>
            </section>

            <!-- 2. ABOUT -->
            <section>
                <div class="grid-2">
