<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Future Circulation - 一杯のコーヒーから、未来の循環を。</title>
    <!-- Google Fonts: Cormorant Garamond (En Serif) & Noto Sans JP -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,400&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS for modern rapid styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Custom Tailwind Configuration -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        coffeeBg: '#13100e',      /* 極めて深い、高級感あるダークブラウン */
                        coffeeCard: '#1c1815',    /* カードなどの背景色 */
                        coffeeText: '#f4f0ea',    /* 読みやすく温かみのある生成り色 */
                        coffeeMuted: '#a89f95',   /* 落ち着いたニュアンスグレー */
                        coffeeAccent: '#c37e65',  /* 輝きを抑えた上質なテラコッタ */
                        coffeeOlive: '#556653',   /* ミャンマーの豊かな自然を表すオリーブ */
                    },
                    fontFamily: {
                        en: ['Cormorant Garamond', 'serif'],
                        jp: ['Noto Sans JP', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #13100e;
            color: #f4f0ea;
            -webkit-font-smoothing: antialiased;
            font-feature-settings: "palt";
        }
        
        /* Smooth transitions */
        .transition-custom {
            transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
        }

        /* Image Parallax Container */
        .parallax-container {
            position: relative;
            overflow: hidden;
            border-radius: 12px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
        }

        .parallax-img {
            width: 100%;
            height: 135%;
            object-fit: cover;
            position: absolute;
            top: -15%;
            left: 0;
            filter: brightness(0.85) contrast(1.05);
            transition: filter 0.5s ease;
        }

        .parallax-container:hover .parallax-img {
            filter: brightness(0.95) contrast(1.05);
        }

        /* Reveal Animation Styles */
        .reveal-mask {
            overflow: hidden;
            display: inline-block;
        }
        .reveal-text {
            display: inline-block;
            transform: translateY(110%);
            transition: transform 1.2s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-mask.active .reveal-text {
            transform: translateY(0);
        }

        /* Navigation indicator dots */
        .dot-active::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 100%;
            height: 1px;
            background-color: #c37e65;
            transform: scaleX(1);
            transition: transform 0.3s ease;
        }

        /* Hide scrollbars for absolute clean editorial layout */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #13100e;
        }
        ::-webkit-scrollbar-thumb {
            background: #2c2520;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #c37e65;
        }
    </style>

    <!-- External Libraries for Animation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/studio-freight/lenis@1.0.29/bundled/lenis.min.js"></script>
</head>
<body class="font-jp overflow-x-hidden">

    <!-- Elegant Fullscreen Loader -->
    <div id="loader" class="fixed inset-0 bg-coffeeBg z-[9999] flex flex-col justify-center items-center transition-custom duration-1000">
        <div class="text-center">
            <h2 class="font-en text-3xl md:text-5xl font-light tracking-[0.2em] uppercase text-coffeeText mb-4 overflow-hidden">
                <span class="inline-block animate-[revealUp_1.2s_cubic-bezier(0.16,1,0.3,1)_forwards]">Future Circulation</span>
            </h2>
            <div class="w-16 h-[1px] bg-coffeeAccent mx-auto scale-x-0 animate-[scaleX_1.5s_0.3s_cubic-bezier(0.16,1,0.3,1)_forwards] origin-center"></div>
            <p class="font-en text-xs tracking-[0.3em] text-coffeeMuted uppercase mt-4 animate-pulse">Loading Culture</p>
        </div>
    </div>

    <!-- Keyframe Animations for Loader -->
    <style>
        @keyframes revealUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }
        @keyframes scaleX {
            from { transform: scaleX(0); }
            to { transform: scaleX(1); }
        }
    </style>

    <!-- Background Canvas for Interactive Particle Circulation representing the flow of coffee culture -->
    <canvas id="webgl-canvas" class="fixed inset-0 w-full h-full z-0 pointer-events-none opacity-60"></canvas>

    <!-- Minimal Editorial Header -->
    <header class="fixed top-0 left-0 w-full px-6 py-6 md:px-12 md:py-8 flex justify-between items-center z-50 mix-blend-difference">
        <a href="#" class="font-en text-lg md:text-xl font-semibold tracking-[0.15em] text-coffeeText uppercase transition-custom hover:text-coffeeAccent">
            Future Circulation
        </a>
        <nav class="hidden md:flex items-center gap-8 text-xs tracking-[0.2em] text-coffeeText uppercase font-medium">
            <a href="#about" class="relative hover:text-coffeeAccent transition-colors">ABOUT</a>
            <a href="#coffee" class="relative hover:text-coffeeAccent transition-colors">OUR COFFEE</a>
            <a href="#products" class="relative hover:text-coffeeAccent transition-colors font-semibold text-coffeeAccent">PRODUCTS</a>
            <a href="#circulation" class="relative hover:text-coffeeAccent transition-colors">CIRCULATION</a>
        </nav>
        <a href="#contact" class="border border-coffeeText/20 hover:border-coffeeAccent px-5 py-2.5 rounded-full text-[10px] md:text-xs tracking-[0.15em] text-coffeeText hover:text-coffeeAccent uppercase transition-custom">
            Contact
        </a>
    </header>

    <!-- Smooth Scroll wrapper using Lenis -->
    <div id="smooth-wrapper" class="relative z-10 w-full">
        <div id="smooth-content" class="w-full">

            <!-- 1. TOP HERO SECTION -->
            <section class="min-h-screen flex flex-col justify-center items-center px-4 py-24 text-center relative">
                <div class="max-w-4xl mx-auto z-10">
                    <span class="font-en text-xs md:text-sm tracking-[0.4em] uppercase text-coffeeAccent mb-6 block font-medium animate-[revealUp_1.5s_0.4s_ease-out_both]">
                        Myanmar Coffee & Culture Project
                    </span>
                    <h1 class="font-en text-5xl md:text-[7.5rem] font-light leading-none tracking-tight mb-8">
                        <span class="block reveal-mask active"><span class="reveal-text">Future</span></span>
                        <span class="block reveal-mask active text-coffeeAccent font-normal italic"><span class="reveal-text">Circulation</span></span>
                    </h1>
                    <h2 class="font-jp text-lg md:text-2xl font-light tracking-[0.2em] leading-relaxed mb-12 max-w-2xl mx-auto text-coffeeText/90">
                        一杯のコーヒーから、未来の循環を。
                    </h2>
                    <div class="h-[1px] w-24 bg-coffeeAccent/40 mx-auto mb-12"></div>
                    <div class="gsap-fade-up max-w-xl mx-auto space-y-4">
                        <p class="font-jp text-xs md:text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                            Future Circulationは、ミャンマー山岳地域のコーヒーと日常文化を通して、<br class="hidden md:inline">
                            文化・ストーリー・循環を届けるブランドです。
                        </p>
                        <p class="font-jp text-xs md:text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                            単なるコーヒーではなく、その背景にある人々の暮らしや文化を、<br class="hidden md:inline">
                            現代ギフトとして再編集しています。
                        </p>
                    </div>
                </div>
                
                <!-- Scroll Indicator -->
                <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-60">
                    <span class="font-en text-[9px] tracking-[0.3em] uppercase text-coffeeMuted">Scroll</span>
                    <div class="w-[1px] h-10 bg-gradient-to-b from-coffeeMuted to-transparent animate-[scrollDown_2s_infinite_ease-in-out]"></div>
                </div>
            </section>
            
            <style>
                @keyframes scrollDown {
                    0% { transform: scaleY(0); transform-origin: top; }
                    50% { transform: scaleY(1); transform-origin: top; }
                    51% { transform: scaleY(1); transform-origin: bottom; }
                    100% { transform: scaleY(0); transform-origin: bottom; }
                }
            </style>

            <!-- 2. ABOUT SECTION (Featuring Image: 9c03a345-2db2-4b7e-b4a4-e0a84e5644ba.jpg) -->
            <section id="about" class="py-24 md:py-36 px-6 md:px-12 max-w-7xl mx-auto">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                    
                    <!-- Left: Stunning Parallax Image of Coffee Plant (9c03a345...) -->
                    <div class="lg:col-span-6 order-2 lg:order-1">
                        <div class="parallax-container h-[55vh] md:h-[70vh] w-full">
                            <!-- This image shows the beautiful coffee tree branch heavy with cherry fruits -->
                            <img src="images/green_beans.jpg" 
                                 onerror="this.onerror=null; this.src='https://images.unsplash.com/photo-1524350876685-274059332603?auto=format&fit=crop&w=1000&q=80';" 
                                 alt="Coffee Tree in Myanmar" 
                                 class="parallax-img">
                            
                            <!-- Absolute Badge on Image -->
                            <div class="absolute bottom-6 left-6 bg-coffeeBg/80 backdrop-blur-md px-4 py-2 rounded-lg border border-white/10">
                                <span class="font-en text-[10px] tracking-[0.2em] uppercase text-coffeeAccent block">Cultivation</span>
                                <span class="font-jp text-[11px] tracking-widest text-coffeeText">標高1500mの農園</span>
                            </div>
                        </div>
                    </div>

                    <!-- Right: Narrative Content -->
                    <div class="lg:col-span-6 order-1 lg:order-2 space-y-10">
                        <div class="space-y-4">
                            <span class="font-en text-xs tracking-[0.3em] text-coffeeAccent uppercase block font-semibold">ABOUT</span>
                            <h2 class="font-jp text-2xl md:text-4xl font-light leading-snug tracking-wider text-coffeeText">
                                ミャンマーの日常文化を、<br>現代ギフトとして。
                            </h2>
                        </div>

                        <div class="gsap-fade-up space-y-6">
                            <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                Future Circulationが届けたいのは、<br>「商品」だけではありません。
                            </p>
                            <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light pl-4 border-l-2 border-coffeeAccent/30">
                                コーヒーの香り。市場の空気。<br>
                                山岳地域の暮らし。日常の中で使われる布。
                            </p>
                            <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                その背景にある文化やストーリーを、現代のライフスタイルに合わせて編集し、大切に届けています。
                            </p>
                        </div>

                        <!-- Mini Sub-section: "支援"ではなく"循環"を -->
                        <div class="gsap-fade-up pt-6 border-t border-coffeeText/10 space-y-6">
                            <h3 class="font-jp text-lg tracking-widest font-normal text-coffeeAccent">
                                “支援”ではなく、“循環”を。
                            </h3>
                            <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                私たちは、「かわいそうだから助ける」という一方的な形ではなく、<strong>価値ある魅力的な文化体験が、結果的に持続可能な循環を生み出す仕組み</strong>を目指しています。
                            </p>
                            
                            <ul class="space-y-3 pt-2">
                                <li class="flex items-center gap-3 text-xs tracking-widest text-coffeeText">
                                    <span class="w-1.5 h-1.5 rounded-full bg-coffeeAccent"></span>
                                    生産者との対等で継続的なパートナーシップ
                                </li>
                                <li class="flex items-center gap-3 text-xs tracking-widest text-coffeeText">
                                    <span class="w-1.5 h-1.5 rounded-full bg-coffeeAccent"></span>
                                    持続的な教育環境への支援
                                </li>
                                <li class="flex items-center gap-3 text-xs tracking-widest text-coffeeText">
                                    <span class="w-1.5 h-1.5 rounded-full bg-coffeeAccent"></span>
                                    美しく温かな現地伝統文化の継承
                                </li>
                            </ul>
                        </div>
                    </div>

                </div>
            </section>

            <!-- 3. OUR COFFEE SECTION (Featuring Image: IMG_20200306_134254.jpg) -->
            <section id="coffee" class="py-24 md:py-36 bg-coffeeCard/50 border-y border-coffeeText/5">
                <div class="max-w-7xl mx-auto px-6 md:px-12">
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                        
                        <!-- Left: Deep copy details -->
                        <div class="lg:col-span-6 space-y-10">
                            <div class="space-y-4">
                                <span class="font-en text-xs tracking-[0.3em] text-coffeeAccent uppercase block font-semibold">OUR COFFEE</span>
                                <h2 class="font-jp text-2xl md:text-4xl font-light leading-snug tracking-wider text-coffeeText">
                                    ミャンマー山岳地域から<br>届くコーヒー
                                </h2>
                            </div>

                            <div class="gsap-fade-up space-y-6">
                                <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                    標高1500mを超える霧深き山岳地域。澄んだ空気と強烈な寒暖差の中で育まれた特別なコーヒーは、<strong>豊かなフルーティーな香りと、驚くほどやわらかな甘み</strong>が特徴です。
                                </p>
                                <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                    大自然の恵みと、現地の生産者による丁寧な手仕事によって生まれた極上の味わいを、そのまま日本のあなたのもとへ届けます。
                                </p>
                            </div>

                            <!-- Production Background -->
                            <div class="gsap-fade-up pt-6 border-t border-coffeeText/10 space-y-4">
                                <h3 class="font-jp text-base tracking-widest font-normal text-coffeeAccent">
                                    確固たる生産背景
                                </h3>
                                <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                    Future Circulationでは、単なる市場取引での仕入れではなく、現地のコミュニティに何度も直接足を運び、信頼関係を築くことを最優先しています。<br>
                                    正当な価格での継続的な直接取引（ダイレクトトレード）を通じて、生産者が安心して高品質なコーヒーを作り続けられる、持続可能な循環を実現しています。
                                </p>
                            </div>
                        </div>

                        <!-- Right: Stunning bowl of cherries image (IMG_20200306_134254.jpg) -->
                        <div class="lg:col-span-6">
                            <div class="parallax-container h-[50vh] md:h-[65vh] w-full">
                                <img src="images/coffee_cherry.jpg" 
                                     onerror="this.onerror=null; this.src='https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?auto=format&fit=crop&w=1000&q=80';" 
                                     alt="Harvested Red Coffee Cherries" 
                                     class="parallax-img">
                                
                                <div class="absolute bottom-6 right-6 bg-coffeeBg/80 backdrop-blur-md px-4 py-2 rounded-lg border border-white/10">
                                    <span class="font-en text-[10px] tracking-[0.2em] uppercase text-coffeeAccent block">Harvest</span>
                                    <span class="font-jp text-[11px] tracking-widest text-coffeeText">手摘みで選別された完熟豆</span>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>
            </section>

            <!-- 4. PRODUCTS LINEUP SECTION -->
            <section id="products" class="py-24 md:py-36 px-6 md:px-12 max-w-5xl mx-auto">
                <div class="text-center space-y-4 mb-16 md:mb-24">
                    <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">COLLECTIONS</span>
                    <h2 class="font-jp text-2xl md:text-4xl font-light tracking-[0.2em] text-coffeeText">展開ラインナップ</h2>
                </div>

                <!-- Interactive Accordion List -->
                <div class="border-t border-coffeeText/10">
                    
                    <!-- PRODUCT ITEM 01 -->
                    <div class="product-accordion group border-b border-coffeeText/10 py-8 md:py-12 cursor-pointer transition-custom hover:bg-coffeeCard/30 px-4 rounded-b-lg">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-6">
                                <span class="font-en text-lg md:text-2xl text-coffeeAccent/50 font-light group-hover:text-coffeeAccent transition-colors">01</span>
                                <div>
                                    <h3 class="font-en text-xl md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">ENTRY LINE</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1">はじめてのFuture Circulation</p>
                                </div>
                            </div>
                            <span class="font-en text-xs tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-2">
                                VIEW DETAILS 
                                <span class="transform transition-transform group-hover:translate-x-1">→</span>
                            </span>
                        </div>
                        
                        <!-- Expandable Content -->
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-coffeeText/5">
                                <p class="font-jp text-xs md:text-sm leading-[2] tracking-widest text-coffeeMuted">
                                    まずは、ミャンマーコーヒー本来の奥深い美味しさと、ブランドの持つあたたかな背景を手軽に知っていただくためのエントリーライン。
                                </p>
                                <div class="space-y-4">
                                    <p class="font-jp text-xs md:text-sm text-coffeeText font-medium">パッケージ同封内容：</p>
                                    <ul class="grid grid-cols-2 gap-2 text-xs text-coffeeMuted tracking-widest">
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>ドリップバッグ</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>生産地カード</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>ブランドストーリー</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- PRODUCT ITEM 02 -->
                    <div class="product-accordion group border-b border-coffeeText/10 py-8 md:py-12 cursor-pointer transition-custom hover:bg-coffeeCard/30 px-4 rounded-b-lg">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-6">
                                <span class="font-en text-lg md:text-2xl text-coffeeAccent/50 font-light group-hover:text-coffeeAccent transition-colors">02</span>
                                <div>
                                    <h3 class="font-en text-xl md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">BRAND LINE</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1">企業と文化をつなぐOEMギフト</p>
                                </div>
                            </div>
                            <span class="font-en text-xs tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-2">
                                VIEW DETAILS 
                                <span class="transform transition-transform group-hover:translate-x-1">→</span>
                            </span>
                        </div>
                        
                        <!-- Expandable Content -->
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-coffeeText/5">
                                <p class="font-jp text-xs md:text-sm leading-[2] tracking-widest text-coffeeMuted">
                                    企業オリジナルパッケージに対応した、OEMギフトライン。<br>
                                    「物語を宿した贈り物」として、採用ギフト、周年イベント、手土産など幅広い用途でお使いいただき、企業のソーシャルアクションを体現します。
                                </p>
                                <div class="space-y-4">
                                    <p class="font-jp text-xs md:text-sm text-coffeeText font-medium">OEM対応範囲（カスタマイズ可能）：</p>
                                    <ul class="grid grid-cols-2 gap-2 text-xs text-coffeeMuted tracking-widest">
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>オリジナルパッケージ</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>ロゴシール貼付</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>特製BOX帯デザイン</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>メッセージカード同梱</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- PRODUCT ITEM 03 -->
                    <div class="product-accordion group border-b border-coffeeText/10 py-8 md:py-12 cursor-pointer transition-custom hover:bg-coffeeCard/30 px-4 rounded-b-lg">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-6">
                                <span class="font-en text-lg md:text-2xl text-coffeeAccent/50 font-light group-hover:text-coffeeAccent transition-colors">03</span>
                                <div>
                                    <h3 class="font-en text-xl md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">PREMIUM LINE</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1">文化を丸ごと体験する至高のギフト</p>
                                </div>
                            </div>
                            <span class="font-en text-xs tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-2">
                                VIEW DETAILS 
                                <span class="transform transition-transform group-hover:translate-x-1">→</span>
                            </span>
                        </div>
                        
                        <!-- Expandable Content -->
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-coffeeText/5">
                                <p class="font-jp text-xs md:text-sm leading-[2] tracking-widest text-coffeeMuted">
                                    淹れたての極上のコーヒーに加え、ミャンマーの温かみあふれる手仕事による日常布や、現地の暮らしを綴ったオリジナルのストーリー冊子を贅沢に同梱。<br>
                                    五感を通して遥か遠い地の美しい生活文化に触れる、高付加価値な体験ギフトです。
                                </p>
                                <div class="space-y-4">
                                    <p class="font-jp text-xs md:text-sm text-coffeeText font-medium">パッケージ同封内容：</p>
                                    <ul class="grid grid-cols-2 gap-2 text-xs text-coffeeMuted tracking-widest">
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>極上シングルオリジン豆</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>一点ものミャンマー日常布</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>オリジナルブックレット</li>
                                        <li class="flex items-center gap-2"><span class="w-1 h-1 rounded-full bg-coffeeAccent"></span>クラフト外装BOX</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </section>

            <!-- 5. MYANMAR FABRIC & CIRCULATION SECTION (Featuring Image: 8e393634-e688-48a9-b44a-e8ec61671b32.jpg) -->
            <section id="circulation" class="py-24 md:py-36 bg-coffeeCard/30">
                <div class="max-w-7xl mx-auto px-6 md:px-12">
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                        
                        <!-- Left: Stunning Sorting Girl Image (8e393634-e688-48a9-b44a-e8ec61671b32.jpg) -->
                        <div class="lg:col-span-6">
                            <div class="parallax-container h-[55vh] md:h-[75vh] w-full">
                                <img src="images/coffee_processing.jpg" 
                                     onerror="this.onerror=null; this.src='https://images.unsplash.com/photo-1511537190424-bbbab87ac5eb?auto=format&fit=crop&w=1000&q=80';" 
                                     alt="Sorting coffee beans in Myanmar" 
                                     class="parallax-img">
                                
                                <div class="absolute bottom-6 left-6 bg-coffeeBg/80 backdrop-blur-md px-4 py-2 rounded-lg border border-white/10">
                                    <span class="font-en text-[10px] tracking-[0.2em] uppercase text-coffeeAccent block">Circulation</span>
                                    <span class="font-jp text-[11px] tracking-widest text-coffeeText">手仕事から繋がる明日</span>
                                </div>
                            </div>
                        </div>

                        <!-- Right: Detailed Information -->
                        <div class="lg:col-span-6 space-y-12">
                            
                            <!-- Myanmar Fabric -->
                            <div class="space-y-6">
                                <div class="space-y-2">
                                    <span class="font-en text-xs tracking-[0.3em] text-coffeeAccent uppercase block font-semibold">MYANMAR FABRIC</span>
                                    <h2 class="font-jp text-xl md:text-3xl font-light tracking-wider text-coffeeText">
                                        一点ごとに異なる、<br>ミャンマーの日常布
                                    </h2>
                                </div>
                                <div class="gsap-fade-up space-y-4">
                                    <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                        Future Circulationが製品の包装に使用している布は、お土産物用ではなく、現地の人々が実際に普段の生活の中で愛用し、流通している本物の日常布です。
                                    </p>
                                    <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                        そのため、模様や色、織り目は一点ごとにすべて異なります。効率的な大量生産品には決して真似できない、あたたかでユニークな**「一点ものとしての価値」**を、そのままあなたにお届けします。
                                    </p>
                                </div>
                            </div>

                            <div class="w-full h-[1px] bg-coffeeText/10"></div>

                            <!-- Circulation Mechanism -->
                            <div class="space-y-6">
                                <div class="space-y-2">
                                    <span class="font-en text-xs tracking-[0.3em] text-coffeeAccent uppercase block font-semibold">SUSTAINABILITY</span>
                                    <h2 class="font-jp text-xl md:text-3xl font-light tracking-wider text-coffeeText">
                                        文化が循環する仕組みを。
                                    </h2>
                                </div>
                                <div class="gsap-fade-up space-y-4">
                                    <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                        私たちのブランドは、ビジネスを通じて文化の保全や生産者の社会的地位の向上を強力に設計する「循環型モデル」を目指しています。
                                    </p>
                                    <ul class="space-y-3 pl-2 border-l border-coffeeAccent/30 text-xs tracking-widest text-coffeeMuted leading-[2]">
                                        <li>・現地の豆を適正かつ安定した公正価格で取引する「継続取引」</li>
                                        <li>・販売利益の確実な一部を、現地の子供たちへの「教育支援活動費」へ還元</li>
                                        <li>・技術継承と伝統布の生産活性化を伴う「現地日常文化の積極的保護」</li>
                                    </ul>
                                </div>
                            </div>

                        </div>

                    </div>
                </div>
            </section>

            <!-- 6. BRAND MESSAGE SECTION -->
            <section class="py-32 md:py-48 px-6 md:px-12 text-center max-w-4xl mx-auto relative overflow-hidden">
                <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-72 h-72 bg-coffeeAccent/5 rounded-full blur-3xl pointer-events-none"></div>
                <div class="space-y-10 z-10 relative">
                    <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">MESSAGE</span>
                    <h2 class="font-jp text-3xl md:text-5xl font-light tracking-[0.2em] leading-normal text-coffeeText">
                        日常を、つなぐ。
                    </h2>
                    <div class="gsap-fade-up space-y-6 max-w-2xl mx-auto">
                        <p class="font-jp text-sm md:text-base leading-[2.4] tracking-widest text-coffeeMuted font-light">
                            私たちは、ミャンマーの素朴で美しい日常文化を、<br>
                            単なる遠い国の“異国文化”として消費するのではなく、<br>
                            今のわたしたちのライフスタイルに自然にフィットする形で、<br>
                            誇りを持って未来へつないでいきたいと考えています。
                        </p>
                        <p class="font-jp text-lg md:text-xl leading-[2.4] tracking-[0.2em] text-coffeeAccent pt-8 font-normal">
                            一杯のコーヒーから、新しい未来の循環を。
                        </p>
                    </div>
                </div>
            </section>

            <!-- 7. CONTACT & FOOTER SECTION -->
            <section id="contact" class="bg-coffeeCard border-t border-coffeeText/10">
                <div class="max-w-7xl mx-auto px-6 md:px-12 py-16 md:py-24 grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24">
                    
                    <!-- Left: Brand Info & Social -->
                    <div class="lg:col-span-6 space-y-8">
                        <h2 class="font-en text-2xl tracking-[0.2em] text-coffeeAccent uppercase">
                            Future Circulation
                        </h2>
                        <p class="font-jp text-xs leading-[2] tracking-widest text-coffeeMuted max-w-sm">
                            一杯のコーヒーから、未来の循環を。<br>
                            ミャンマーの誇る特別な風味とあたたかな文化を、皆様の暮らしの中、そして特別なギフトとしてお届けします。
                        </p>
                        <div class="flex gap-6 pt-4 text-xs tracking-[0.15em] font-en uppercase text-coffeeText">
                            <a href="#" class="hover:text-coffeeAccent transition-colors">Instagram</a>
                            <a href="#" class="hover:text-coffeeAccent transition-colors">Online Store</a>
                            <a href="#" class="hover:text-coffeeAccent transition-colors">About Us</a>
                        </div>
                    </div>

                    <!-- Right: Links & CTA -->
                    <div class="lg:col-span-6 flex flex-col justify-between items-start lg:items-end gap-12">
                        <div class="w-full grid grid-cols-2 gap-8 text-xs tracking-widest text-coffeeMuted">
                            <div class="space-y-4">
                                <h4 class="text-coffeeText font-medium font-en tracking-[0.2em]">BUSINESS</h4>
                                <ul class="space-y-2 text-[11px]">
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">OEM Gift Project</a></li>
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">Retail Partnerships</a></li>
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">Media Kit</a></li>
                                </ul>
                            </div>
                            <div class="space-y-4">
                                <h4 class="text-coffeeText font-medium font-en tracking-[0.2em]">CUSTOMER</h4>
                                <ul class="space-y-2 text-[11px]">
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">Contact Support</a></li>
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">Shopping FAQ</a></li>
                                    <li><a href="#" class="hover:text-coffeeAccent transition-colors">Privacy Policy</a></li>
                                </ul>
                            </div>
                        </div>

                        <!-- Elegant CTA button -->
                        <div class="w-full flex flex-col sm:flex-row gap-4 justify-start lg:justify-end">
                            <a href="#" class="inline-block px-8 py-4 bg-coffeeAccent hover:bg-coffeeAccent/95 text-coffeeBg font-en font-semibold tracking-[0.2em] text-center text-xs uppercase rounded-full transition-custom shadow-lg hover:shadow-coffeeAccent/10">
                                OEM CONTACT (お問合せ)
                            </a>
                            <a href="#" class="inline-block px-8 py-4 bg-transparent border border-coffeeText/20 hover:border-coffeeAccent text-coffeeText hover:text-coffeeAccent font-en font-semibold tracking-[0.2em] text-center text-xs uppercase rounded-full transition-custom">
                                ONLINE STORE (EC)
                            </a>
                        </div>
                    </div>

                </div>
                
                <!-- Bottom Copyright -->
                <div class="max-w-7xl mx-auto px-6 md:px-12 py-8 border-t border-coffeeText/5 flex flex-col sm:flex-row justify-between items-center gap-4 text-[10px] text-coffeeMuted/75 tracking-wider">
                    <p>© Future Circulation Coffee Project. All Rights Reserved.</p>
                    <p>Designed for Sustainable Future.</p>
                </div>
            </section>

        </div>
    </div>

    <script>
        // ==========================================
        // 1. Lenis Smooth Scroll Setup
        // ==========================================
        const lenis = new Lenis({
            duration: 1.4,
            easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
            smooth: true,
            wheelMultiplier: 0.9
        });

        function raf(time) {
            lenis.raf(time);
            requestAnimationFrame(raf);
        }
        requestAnimationFrame(raf);

        // Update ScrollTrigger on Lenis Scroll
        lenis.on('scroll', ScrollTrigger.update);

        // ==========================================
        // 2. Dismiss Loader Function
        // ==========================================
        window.addEventListener('DOMContentLoaded', () => {
            // Dismiss loader after short delay for smoothness
            setTimeout(() => {
                const loader = document.getElementById('loader');
                if (loader) {
                    loader.style.opacity = '0';
                    loader.style.pointerEvents = 'none';
                    setTimeout(() => loader.remove(), 1000);
                }
                
                // Trigger entry text reveals
                document.querySelectorAll('.reveal-mask').forEach(el => {
                    el.classList.add('active');
                });
            }, 1200);
        });

        // Fail-safe to ensure loader closes within 3.5 seconds
        setTimeout(() => {
            const loader = document.getElementById('loader');
            if (loader) {
                loader.style.opacity = '0';
                loader.style.pointerEvents = 'none';
                setTimeout(() => loader.remove(), 1000);
            }
        }, 3500);

        // ==========================================
        // 3. GSAP Scroll Animations
        // ==========================================
        gsap.registerPlugin(ScrollTrigger);

        // Fine-tuned Image Parallax effect
        gsap.utils.toArray('.parallax-container').forEach(wrapper => {
            const img = wrapper.querySelector('.parallax-img');
            gsap.to(img, {
                yPercent: 12,
                ease: "none",
                scrollTrigger: {
                    trigger: wrapper,
                    start: "top bottom",
                    end: "bottom top",
                    scrub: true
                }
            });
        });

        // Fade up element animations
        gsap.utils.toArray('.gsap-fade-up').forEach(elem => {
            gsap.fromTo(elem, 
                { y: 40, opacity: 0 },
                { 
                    y: 0, 
                    opacity: 1, 
                    duration: 1.2, 
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: elem,
                        start: "top 85%",
                        toggleActions: "play none none none"
                    }
                }
            );
        });

        // ==========================================
        // 4. Products Accordion Interaction
        // ==========================================
        const accordions = document.querySelectorAll('.product-accordion');
        accordions.forEach(acc => {
            acc.addEventListener('click', () => {
                const details = acc.querySelector('.product-details');
                const isOpened = acc.classList.contains('active-acc');
                
                // Close all others first
                accordions.forEach(other => {
                    other.classList.remove('active-acc');
                    other.querySelector('.product-details').style.maxHeight = '0px';
                    other.querySelector('.product-details').style.opacity = '0';
                });

                if (!isOpened) {
                    acc.classList.add('active-acc');
                    // Compute accurate height to animate dynamically
                    details.style.maxHeight = details.scrollHeight + 60 + 'px';
                    details.style.opacity = '1';
                }
                
                // Inform ScrollTrigger to recalculate bounds after content heights change
                setTimeout(() => {
                    ScrollTrigger.refresh();
                }, 500);
            });
        });

        // ==========================================
        // 5. Three.js Subtle Background Floating Dust
        // ==========================================
        const canvas = document.getElementById('webgl-canvas');
        const scene = new THREE.Scene();
        
        // Deep atmosphere fog matching our coffee brand theme color
        scene.fog = new THREE.FogExp2(0x13100e, 0.04);

        const camera = new THREE.PerspectiveCamera(70, window.innerWidth / window.innerHeight, 0.1, 100);
        camera.position.z = 12;
        camera.position.y = 1;

        const renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 1800; // Refined count for seamless performance
        const posArray = new Float32Array(particlesCount * 3);
        const colorArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i += 3) {
            // Soft atmospheric distribution
            posArray[i] = (Math.random() - 0.5) * 35;
            posArray[i+1] = (Math.random() - 0.5) * 35;
            posArray[i+2] = (Math.random() - 0.5) * 35;

            // Brand palette allocation
            const rand = Math.random();
            if(rand > 0.8) {
                // Terracotta accent
                colorArray[i] = 0.76; colorArray[i+1] = 0.49; colorArray[i+2] = 0.40;
            } else if (rand > 0.6) {
                // Soft green
                colorArray[i] = 0.33; colorArray[i+1] = 0.40; colorArray[i+2] = 0.33;
            } else {
                // Warm sand beige
                colorArray[i] = 0.96; colorArray[i+1] = 0.94; colorArray[i+2] = 0.92;
            }
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        particlesGeometry.setAttribute('color', new THREE.BufferAttribute(colorArray, 3));

        // Programmatically generate beautiful round glowing particles
        const createParticleTexture = () => {
            const pCanvas = document.createElement('canvas');
            pCanvas.width = 32;
            pCanvas.height = 32;
            const ctx = pCanvas.getContext('2d');
            
            // Outer glow
            const gradient = ctx.createRadialGradient(16, 16, 0, 16, 16, 16);
            gradient.addColorStop(0, 'rgba(255, 255, 255, 1)');
            gradient.addColorStop(0.3, 'rgba(255, 255, 255, 0.8)');
            gradient.addColorStop(1, 'rgba(255, 255, 255, 0)');
            
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, 32, 32);
            
            const texture = new THREE.CanvasTexture(pCanvas);
            return texture;
        };

        const material = new THREE.PointsMaterial({
            size: 0.16,
            vertexColors: true,
            transparent: true,
            opacity: 0.4,
            map: createParticleTexture(),
            alphaTest: 0.005,
            blending: THREE.AdditiveBlending,
            depthWrite: false
        });

        const particlesMesh = new THREE.Points(particlesGeometry, material);
        scene.add(particlesMesh);

        // Track cursor movement for parallax response
        let mouseX = 0;
        let mouseY = 0;
        document.addEventListener('mousemove', (event) => {
            mouseX = (event.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(event.clientY / window.innerHeight) * 2 + 1;
        });

        // Slowly descend camera during scroll
        gsap.to(camera.position, {
            y: -15,
            ease: "none",
            scrollTrigger: {
                trigger: document.body,
                start: "top top",
                end: "bottom bottom",
                scrub: 1.5
            }
        });

        const clock = new THREE.Clock();
        
        // Loop execution function
        function tick() {
            const elapsedTime = clock.getElapsedTime();

            // Calm, fluid particle rotation indicating natural flow and circulation
            particlesMesh.rotation.y = elapsedTime * 0.015;
            particlesMesh.rotation.x = Math.sin(elapsedTime * 0.05) * 0.08;
            
            // Soft inertia transition for mouse-driven movement
            camera.position.x += (mouseX * 1.5 - camera.position.x) * 0.02;
            
            renderer.render(scene, camera);
            requestAnimationFrame(tick);
        }
        tick();

        // Screen Resize handling
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

    </script>
</body>
</html>
