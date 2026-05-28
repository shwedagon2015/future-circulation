[index.html](https://github.com/user-attachments/files/28341934/index.html)
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FUTURE CIRCULATION Co. | 一杯のコーヒーから、社会と未来の循環を。</title>
    
    <!-- Google Fonts: Cormorant Garamond & Noto Sans JP -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,400&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Custom Tailwind Configuration for Premium Brand Identity -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        coffeeBg: '#0f0d0c',      /* より締まった漆黒に近いダークマホガニー */
                        coffeeCard: '#181412',    /* 高級感溢れるソリッドなカード背景 */
                        coffeeText: '#f5f2eb',    /* ぬくもりのあるシルキーオーガニックホワイト */
                        coffeeMuted: '#9e948a',   /* 視認性と静寂を兼ね備えたアッシュグレー */
                        coffeeAccent: '#d28c73',  /* 艶を抑えたエレガントなテラコッタゴールド */
                        coffeeOlive: '#60725e',   /* 現地の豊かな大地と自然を宿すアーシーグリーン */
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
            background-color: #0f0d0c;
            color: #f5f2eb;
            -webkit-font-smoothing: antialiased;
            font-feature-settings: "palt";
        }
        
        /* Smooth Custom Transitions */
        .transition-premium {
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        /* Editorial Image Container (CSS Design Awards Standard) */
        .parallax-container {
            position: relative;
            overflow: hidden;
            border-radius: 4px; /* ミニマルな直角に近い角丸 */
            box-shadow: 0 30px 60px rgba(0,0,0,0.6);
            border: 1px solid rgba(245, 242, 235, 0.05);
        }

        .parallax-img {
            width: 100%;
            height: 140%;
            object-fit: cover;
            position: absolute;
            top: -20%;
            left: 0;
            filter: brightness(0.8) contrast(1.1);
            transition: filter 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .parallax-container:hover .parallax-img {
            filter: brightness(0.95) contrast(1.05);
            transform: scale(1.02);
        }

        /* Typography Reveal Animation */
        .reveal-mask {
            overflow: hidden;
            display: inline-block;
            vertical-align: bottom;
        }
        .reveal-text {
            display: inline-block;
            transform: translateY(110%);
            transition: transform 1.5s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-mask.active .reveal-text {
            transform: translateY(0);
        }

        /* Fine scrollbar design */
        ::-webkit-scrollbar {
            width: 4px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0d0c;
        }
        ::-webkit-scrollbar-thumb {
            background: #231e1b;
            border-radius: 2px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #d28c73;
        }

        /* Text selection style */
        ::selection {
            background: #d28c73;
            color: #0f0d0c;
        }
    </style>

    <!-- Animation & Smooth Scroll Engine Setup -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/studio-freight/lenis@1.0.29/bundled/lenis.min.js"></script>
</head>
<body class="font-jp overflow-x-hidden">

    <!-- Screen Transition Preloader -->
    <div id="loader" class="fixed inset-0 bg-coffeeBg z-[9999] flex flex-col justify-center items-center transition-premium duration-1000">
        <div class="text-center">
            <h2 class="font-en text-2xl md:text-4xl font-light tracking-[0.25em] uppercase text-coffeeText mb-4 overflow-hidden">
                <span class="inline-block animate-[revealUp_1.5s_cubic-bezier(0.16,1,0.3,1)_forwards]">FUTURE CIRCULATION</span>
            </h2>
            <div class="w-12 h-[1px] bg-coffeeAccent mx-auto scale-x-0 animate-[scaleX_1.8s_0.4s_cubic-bezier(0.16,1,0.3,1)_forwards] origin-center"></div>
            <p class="font-en text-[9px] tracking-[0.4em] text-coffeeMuted uppercase mt-4 animate-pulse">Social Coffee Enterprise</p>
        </div>
    </div>

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

    <!-- Interactive 3D Fluid Particles Background -->
    <canvas id="webgl-canvas" class="fixed inset-0 w-full h-full z-0 pointer-events-none opacity-50"></canvas>

    <!-- Global Corporate Header -->
    <header class="fixed top-0 left-0 w-full px-6 py-6 md:px-12 md:py-8 flex justify-between items-center z-50 mix-blend-difference">
        <div class="flex flex-col">
            <a href="#" class="font-en text-base md:text-lg font-medium tracking-[0.2em] text-coffeeText uppercase transition-premium hover:text-coffeeAccent">
                FUTURE CIRCULATION Co.
            </a>
            <span class="font-jp text-[8px] tracking-[0.15em] text-coffeeMuted uppercase hidden md:inline-block mt-0.5">ミャンマーコーヒー＆ソーシャルアクション</span>
        </div>
        
        <nav class="hidden lg:flex items-center gap-10 text-[10px] tracking-[0.25em] text-coffeeText uppercase font-medium">
            <a href="#about" class="relative hover:text-coffeeAccent transition-colors">ABOUT</a>
            <a href="#coffee" class="relative hover:text-coffeeAccent transition-colors">OUR COFFEE</a>
            <a href="#products" class="relative hover:text-coffeeAccent transition-colors">LINEUP</a>
            <a href="#circulation" class="relative hover:text-coffeeAccent transition-colors">CIRCULATION</a>
        </nav>

        <a href="#contact" class="border border-coffeeText/15 hover:border-coffeeAccent px-6 py-2.5 rounded-full text-[10px] tracking-[0.2em] text-coffeeText hover:text-coffeeBg hover:bg-coffeeAccent uppercase transition-premium">
            CONTACT
        </a>
    </header>

    <!-- Smooth Scroll Container (Lenis) -->
    <div id="smooth-wrapper" class="relative z-10 w-full">
        <div id="smooth-content" class="w-full">

            <!-- 1. HIGH-END BRAND & VISION HERO -->
            <section class="min-h-screen flex flex-col justify-center items-center px-6 py-24 text-center relative">
                <div class="max-w-5xl mx-auto z-10">
                    <span class="font-en text-xs tracking-[0.5em] uppercase text-coffeeAccent mb-6 block font-medium animate-[revealUp_1.5s_0.4s_ease-out_both]">
                        Social & Sustainable Coffee Project
                    </span>
                    <h1 class="font-en text-4xl sm:text-6xl md:text-[6.5rem] font-light leading-none tracking-tight mb-8">
                        <span class="block reveal-mask active"><span class="reveal-text">Future</span></span>
                        <span class="block reveal-mask active text-coffeeAccent font-normal italic"><span class="reveal-text">Circulation</span></span>
                    </h1>
                    <h2 class="font-jp text-base md:text-xl font-light tracking-[0.25em] leading-relaxed mb-12 max-w-3xl mx-auto text-coffeeText/90">
                        一杯のコーヒーから、社会と未来の循環を。
                    </h2>
                    <div class="h-[1px] w-16 bg-coffeeAccent/50 mx-auto mb-12"></div>
                    
                    <div class="gsap-fade-up max-w-2xl mx-auto space-y-4">
                        <p class="font-jp text-xs md:text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                            FUTURE CIRCULATIONは、ミャンマー山岳地域が育む最高品質のコーヒーと現地独自の日常文化を通じ、<br class="hidden md:inline">
                            企業のソーシャルアクション（ESG/SDGs）と生活者を結ぶパートナーシップブランドです。
                        </p>
                        <p class="font-jp text-xs md:text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                            単なる消費に留まらない「美しい循環」の物語を、高付加価値な体験として編集しお届けします。
                        </p>
                    </div>

                    <div class="gsap-fade-up pt-10 flex flex-wrap gap-4 justify-center">
                        <a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="px-8 py-4 bg-coffeeText text-coffeeBg hover:bg-coffeeAccent hover:text-coffeeBg font-en text-[11px] tracking-[0.2em] uppercase rounded-full transition-premium font-semibold shadow-xl">
                            ONLINE STORE <span class="ml-1 text-[9px]">↗</span>
                        </a>
                        <a href="#about" class="px-8 py-4 bg-transparent border border-coffeeText/20 hover:border-coffeeAccent text-coffeeText hover:text-coffeeAccent font-en text-[11px] tracking-[0.2em] uppercase rounded-full transition-premium">
                            LEARN MORE
                        </a>
                    </div>
                </div>
                
                <!-- Pure Interactive Scroll Down Line -->
                <a href="#about" class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-3 opacity-50 hover:opacity-100 transition-opacity">
                    <span class="font-en text-[8px] tracking-[0.4em] uppercase text-coffeeMuted">Scroll Down</span>
                    <div class="w-[1px] h-12 bg-gradient-to-b from-coffeeMuted to-transparent animate-[scrollDown_2.2s_infinite_ease-in-out]"></div>
                </a>
            </section>
            
            <style>
                @keyframes scrollDown {
                    0% { transform: scaleY(0); transform-origin: top; }
                    50% { transform: scaleY(1); transform-origin: top; }
                    51% { transform: scaleY(1); transform-origin: bottom; }
                    100% { transform: scaleY(0); transform-origin: bottom; }
                }
            </style>

            <!-- 2. CORPORATE PURPOSE & MISSION (Featuring "green_beans.jpg") -->
            <section id="about" class="py-24 md:py-40 px-6 md:px-12 max-w-7xl mx-auto">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                    
                    <!-- Left: Raw Coffee Beans in Hands -->
                    <div class="lg:col-span-6 order-2 lg:order-1">
                        <div class="parallax-container h-[55vh] md:h-[75vh] w-full">
                            <img src="green_beans.jpg" 
                                 alt="Raw Coffee Beans in Myanmar Farm" 
                                 class="parallax-img">
                            
                            <div class="absolute bottom-6 left-6 bg-coffeeBg/90 backdrop-blur-md px-5 py-3 rounded border border-white/5">
                                <span class="font-en text-[9px] tracking-[0.25em] uppercase text-coffeeAccent block font-semibold">PARTNERSHIP</span>
                                <span class="font-jp text-[11px] tracking-widest text-coffeeText">信頼を紡ぐ、手の中の原石</span>
                            </div>
                        </div>
                    </div>

                    <!-- Right: Corporate Narrative -->
                    <div class="lg:col-span-6 order-1 lg:order-2 space-y-10">
                        <div class="space-y-4">
                            <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">OUR PURPOSE</span>
                            <h2 class="font-jp text-3xl md:text-4xl font-light leading-snug tracking-wider text-coffeeText">
                                一方的な支援ではない、<br>共創される価値。
                            </h2>
                        </div>

                        <div class="gsap-fade-up space-y-6">
                            <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                近年、企業に強く求められている「持続可能な社会への貢献」と「本質的なストーリーテリング」。<br>
                                私たちは、単に寄付を募るような一過性の慈善活動ではなく、お互いを尊び、対等な経済活動の中で社会課題を解決していく<strong>「CSV (Creating Shared Value: 共通価値の創造)」</strong>を体現しています。
                            </p>
                            <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light pl-4 border-l border-coffeeAccent/35">
                                ミャンマーの山岳地帯にある豊かな生態系。そこで生きる人々の確かな手仕事。<br>
                                私たちはそれらを最高のクオリティに磨き上げ、日本の生活者や先進企業に向けて再編集したギフト・体験としてお届けします。
                            </p>
                        </div>

                        <!-- Mini Corporate Trust Section -->
                        <div class="gsap-fade-up pt-8 border-t border-coffeeText/10 space-y-6">
                            <h3 class="font-jp text-base tracking-widest font-normal text-coffeeAccent">
                                企業としてのコミットメント
                            </h3>
                            <p class="font-jp text-sm leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                当プロジェクトは、現地の生産地コミュニティと直接取引（ダイレクトトレード）を行い、適正価格での安定買い取りを通じて、持続可能な生活基盤の維持と現地の子どもたちへの教育支援を同時に実現しています。
                            </p>
                            
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 pt-2">
                                <div class="bg-coffeeCard p-4 rounded border border-white/5">
                                    <h4 class="font-jp text-xs font-semibold text-coffeeText tracking-widest mb-1">01. 対等なパートナーシップ</h4>
                                    <p class="font-jp text-[11px] text-coffeeMuted leading-relaxed">搾取のない公正な取引（フェアトレード以上のコミット）を継続しています。</p>
                                </div>
                                <div class="bg-coffeeCard p-4 rounded border border-white/5">
                                    <h4 class="font-jp text-xs font-semibold text-coffeeText tracking-widest mb-1">02. 確かな教育還元</h4>
                                    <p class="font-jp text-[11px] text-coffeeMuted leading-relaxed">収益の一部は、現地の持続可能な学校教育・環境整備に直結して活用されます。</p>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </section>

            <!-- 3. PRODUCT STORY: OUR COFFEE (Featuring "coffee_cherry.jpg") -->
            <section id="coffee" class="py-24 md:py-40 bg-coffeeCard/40 border-y border-white/5">
                <div class="max-w-7xl mx-auto px-6 md:px-12">
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                        
                        <!-- Left: Editorial Content -->
                        <div class="lg:col-span-6 space-y-10">
                            <div class="space-y-4">
                                <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">OUR COFFEE</span>
                                <h2 class="font-jp text-3xl md:text-4xl font-light leading-snug tracking-wider text-coffeeText">
                                    天空の農園から生まれる、<br>完熟の恵み。
                                </h2>
                            </div>

                            <div class="gsap-fade-up space-y-6">
                                <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                    ミャンマーの標高1500メートルを超える雲海に抱かれた山岳エリア。昼夜の極端な寒暖差と、有機的な土壌が育む特別なアラビカ豆。
                                </p>
                                <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                    私たちが扱うコーヒーは、一粒一粒を生産者が目で確認しながら、完全に熟しきった真紅のチェリーだけを手摘みしたものです。それにより、<strong>えぐみのない、澄み切ったフルーティーな酸味と、キャラメルのような深い余韻</strong>が特徴となっています。
                                </p>
                            </div>

                            <!-- Quality Statement for Enterprises -->
                            <div class="gsap-fade-up pt-6 border-t border-coffeeText/10 space-y-4">
                                <h3 class="font-jp text-sm tracking-widest font-normal text-coffeeAccent">
                                    妥協のないクオリティ管理
                                </h3>
                                <p class="font-jp text-xs leading-[2.2] tracking-widest text-coffeeMuted font-light">
                                    企業のノベルティや特別な社内ギフト、VIP顧客向けの手土産としても十分な満足をお届けできるよう、輸入ロットごとの厳格な品質検査とフレッシュな国内焙煎にこだわっています。ただの「エシカル（社会配慮）」に留まらず、純粋に「驚くほど美味しい」という体験をお約束します。
                                </p>
                            </div>
                        </div>

                        <!-- Right: Harvest Cherries Image -->
                        <div class="lg:col-span-6">
                            <div class="parallax-container h-[50vh] md:h-[70vh] w-full">
                                <img src="coffee_cherry.jpg" 
                                     alt="Freshly Harvested Red Coffee Cherries" 
                                     class="parallax-img">
                                
                                <div class="absolute bottom-6 right-6 bg-coffeeBg/90 backdrop-blur-md px-5 py-3 rounded border border-white/5">
                                    <span class="font-en text-[9px] tracking-[0.25em] uppercase text-coffeeAccent block font-semibold">HARVEST</span>
                                    <span class="font-jp text-[11px] tracking-widest text-coffeeText">宝石のように選別された完熟チェリー</span>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>
            </section>

            <!-- 4. SIGNATURE LINEUP (EC Direct Connect & Clean B2B Flow) -->
            <section id="products" class="py-24 md:py-40 px-6 md:px-12 max-w-5xl mx-auto">
                <div class="text-center space-y-4 mb-16 md:mb-28">
                    <span class="font-en text-xs tracking-[0.5em] text-coffeeAccent uppercase block font-semibold">PRODUCT PORTFOLIO</span>
                    <h2 class="font-jp text-2xl md:text-3xl font-light tracking-[0.2em] text-coffeeText">プロダクトラインナップ</h2>
                </div>

                <!-- Accordion Interface (Award-Winning UX Vibe) -->
                <div class="border-t border-white/10">
                    
                    <!-- PRODUCT 01: ENTRY LINE (Linked to BASE EC) -->
                    <div class="product-accordion group border-b border-white/10 py-8 md:py-12 cursor-pointer transition-premium hover:bg-coffeeCard/50 px-6 rounded">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-8">
                                <span class="font-en text-xl md:text-3xl text-coffeeAccent/30 font-light group-hover:text-coffeeAccent transition-colors">01</span>
                                <div>
                                    <h3 class="font-en text-lg md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">ENTRY LINE / SINGLE DRIP BAG</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1.5">日常に寄り添う、手軽で奥深い一杯</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-3">
                                <span class="font-en text-[10px] tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-1.5">
                                    GO TO STORE 
                                    <span class="transform transition-transform group-hover:translate-x-1">→</span>
                                </span>
                            </div>
                        </div>
                        
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-white/5">
                                <p class="font-jp text-xs md:text-sm leading-[2.2] tracking-widest text-coffeeMuted">
                                    ミャンマーコーヒー本来の澄んだ美味しさと、現地の美しい風土を手軽にお愉しみいただけるエントリーコレクション。ご自宅用やカジュアルなプチギフトに最適です。
                                </p>
                                <div class="space-y-4">
                                    <div class="flex justify-between items-center pb-2 border-b border-white/5">
                                        <p class="font-jp text-xs text-coffeeText">パッケージ内容</p>
                                        <span class="font-jp text-xs text-coffeeAccent">ドリップバッグ・ストーリーカード</span>
                                    </div>
                                    <a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="inline-block w-full text-center py-3 bg-coffeeAccent/10 hover:bg-coffeeAccent text-coffeeAccent hover:text-coffeeBg text-xs font-en tracking-[0.2em] rounded uppercase transition-premium font-semibold">
                                        オンラインショップで購入する ↗
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- PRODUCT 02: HANDKERCHIEF GIFT (Linked to BASE EC) -->
                    <div class="product-accordion group border-b border-white/10 py-8 md:py-12 cursor-pointer transition-premium hover:bg-coffeeCard/50 px-6 rounded">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-8">
                                <span class="font-en text-xl md:text-3xl text-coffeeAccent/30 font-light group-hover:text-coffeeAccent transition-colors">02</span>
                                <div>
                                    <h3 class="font-en text-lg md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">HANDKERCHIEF COFFEE GIFT</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1.5">ミャンマー伝統の日常布ハンカチを纏う特別なギフト</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-3">
                                <span class="font-en text-[10px] tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-1.5">
                                    GO TO STORE 
                                    <span class="transform transition-transform group-hover:translate-x-1">→</span>
                                </span>
                            </div>
                        </div>
                        
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-white/5">
                                <p class="font-jp text-xs md:text-sm leading-[2.2] tracking-widest text-coffeeMuted">
                                    ミャンマーの人々が日常的に使用する服（民族衣装「ロンジー」など）に使われている美しい織り目の布。それらを現地パートナーが丁寧に裁断し、一つ一つ想いを込めて手作りした世界に一つだけのオリジナルハンカチで、上質なコーヒーを包み込んだギフトです。
                                </p>
                                <div class="space-y-4">
                                    <div class="flex justify-between items-center pb-2 border-b border-white/5">
                                        <p class="font-jp text-xs text-coffeeText">パッケージ内容</p>
                                        <span class="font-jp text-xs text-coffeeAccent">プレミアムコーヒー豆/バッグ ＆ 手作り日常布ハンカチ</span>
                                    </div>
                                    <a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="inline-block w-full text-center py-3 bg-coffeeAccent/10 hover:bg-coffeeAccent text-coffeeAccent hover:text-coffeeBg text-xs font-en tracking-[0.2em] rounded uppercase transition-premium font-semibold">
                                        オンラインショップで購入する ↗
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- PRODUCT 03: CORPORATE / OEM SERVICES (Direct to Contact) -->
                    <div class="product-accordion group border-b border-white/10 py-8 md:py-12 cursor-pointer transition-premium hover:bg-coffeeCard/50 px-6 rounded">
                        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                            <div class="flex items-center gap-8">
                                <span class="font-en text-xl md:text-3xl text-coffeeAccent/30 font-light group-hover:text-coffeeAccent transition-colors">03</span>
                                <div>
                                    <h3 class="font-en text-lg md:text-2xl tracking-wider text-coffeeText group-hover:text-coffeeAccent transition-colors">B2B CO-CREATION / OEM SERVICES</h3>
                                    <p class="font-jp text-xs text-coffeeMuted tracking-wider mt-1.5">企業のソーシャルアクションを体現する特注ギフト・導入プラン</p>
                                </div>
                            </div>
                            <div class="flex items-center gap-3">
                                <span class="font-en text-[10px] tracking-[0.2em] text-coffeeMuted group-hover:text-coffeeAccent transition-all flex items-center gap-1.5">
                                    INQUIRE NOW 
                                    <span class="transform transition-transform group-hover:translate-x-1">→</span>
                                </span>
                            </div>
                        </div>
                        
                        <div class="product-details max-h-0 opacity-0 overflow-hidden transition-all duration-700 ease-in-out">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 pt-8 mt-6 border-t border-white/5">
                                <p class="font-jp text-xs md:text-sm leading-[2.2] tracking-widest text-coffeeMuted">
                                    企業の周年ノベルティ、株主総会のギフト、オフィスカフェでのエシカルコーヒー導入など、企業様の社会貢献（ESG）メッセージを伝える特別仕様のOEM提供に対応します。パッケージのカスタマイズや共同ストーリーペーパーの同封など柔軟にサポートいたします。
                                </p>
                                <div class="space-y-4">
                                    <div class="flex justify-between items-center pb-2 border-b border-white/5">
                                        <p class="font-jp text-xs text-coffeeText">対応カスタマイズ</p>
                                        <span class="font-jp text-xs text-coffeeAccent">企業ロゴ刻印、特注スリーブ、オリジナル布セレクト</span>
                                    </div>
                                    <a href="#contact" class="inline-block w-full text-center py-3 bg-coffeeText text-coffeeBg hover:bg-coffeeAccent font-xs font-en tracking-[0.2em] rounded uppercase transition-premium font-semibold">
                                        企画・お見積りの相談をする（無料）
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </section>

            <!-- 5. SOCIAL VALUE & IMPACT (Featuring "coffee_processing.jpg") -->
            <section id="circulation" class="py-24 md:py-40 bg-coffeeCard/30 border-t border-white/5">
                <div class="max-w-7xl mx-auto px-6 md:px-12">
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-24 items-center">
                        
                        <!-- Left: Sorting Processing Girl Image -->
                        <div class="lg:col-span-6">
                            <div class="parallax-container h-[55vh] md:h-[75vh] w-full">
                                <img src="coffee_processing.jpg" 
                                     alt="Local Burmese girl sorting coffee beans lovingly" 
                                     class="parallax-img">
                                
                                <div class="absolute bottom-6 left-6 bg-coffeeBg/90 backdrop-blur-md px-5 py-3 rounded border border-white/5">
                                    <span class="font-en text-[9px] tracking-[0.25em] uppercase text-coffeeAccent block font-semibold">CRAFTSMANSHIP</span>
                                    <span class="font-jp text-[11px] tracking-widest text-coffeeText">手作業に宿る、尊厳と誇り</span>
                                </div>
                            </div>
                        </div>

                        <!-- Right: Detailed Circulation Values -->
                        <div class="lg:col-span-6 space-y-12">
                            
                            <div class="space-y-6">
                                <div class="space-y-2">
                                    <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">HANDMADE CRAFT</span>
                                    <h2 class="font-jp text-2xl md:text-3xl font-light tracking-wider text-coffeeText">
                                        日常が美しく紡ぐ、<br>一点もののハンカチ。
                                    </h2>
                                </div>
                                <div class="gsap-fade-up space-y-4">
                                    <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                        ギフトに使用しているハンカチは、すべて現地ミャンマーの日常に深く溶け込んでいる衣服（日常布）の端切れを使用しています。<br>
                                        効率主義的な大量生産の資材ではなく、現地の人々が古くから愛し誇ってきた温もりある手仕事が息づいています。
                                    </p>
                                    <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                        ミャンマー人が日常的に使用する服に使われている布を使用し、一つ一つ手作業で作られているため、柄や織り目のニュアンスはすべて異なる。この世に二つとない<strong>「偶然の出会い」</strong>としての価値をお届けしています。
                                    </p>
                                </div>
                            </div>

                            <div class="w-full h-[1px] bg-white/10"></div>

                            <div class="space-y-6">
                                <div class="space-y-2">
                                    <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent uppercase block font-semibold">CIRCULATION SYSTEM</span>
                                    <h2 class="font-jp text-2xl md:text-3xl font-light tracking-wider text-coffeeText">
                                        持続可能に巡りゆく社会へ。
                                    </h2>
                                </div>
                                <div class="gsap-fade-up space-y-4">
                                    <p class="font-jp text-sm leading-[2.4] tracking-widest text-coffeeMuted font-light">
                                        FUTURE CIRCULATIONが提供するのは、経済活動が美しく社会の循環を生み出す、確かな仕組み（プラットフォーム）です。
                                    </p>
                                    <ul class="space-y-3 pl-3 border-l border-coffeeAccent/30 text-xs tracking-widest text-coffeeMuted leading-[2]">
                                        <li class="flex items-start gap-2">
                                            <span class="text-coffeeAccent font-semibold">◆</span>
                                            <span>生産者の社会的地位の確立：安定雇用と公正・正当価格でのダイレクト取引</span>
                                        </li>
                                        <li class="flex items-start gap-2">
                                            <span class="text-coffeeAccent font-semibold">◆</span>
                                            <span>未来を拓く教育サポート：製品販売利益の一部から、現地校舎の改修や教材支援費を捻出</span>
                                        </li>
                                        <li class="flex items-start gap-2">
                                            <span class="text-coffeeAccent font-semibold">◆</span>
                                            <span>伝統的なクラフトの振興：端切れ布を活用した裁縫雇用の創造とミャンマーが誇る文化の維持</span>
                                        </li>
                                    </ul>
                                </div>
                            </div>

                        </div>

                    </div>
                </div>
            </section>

            <!-- 6. BRAND STATEMENT -->
            <section class="py-32 md:py-52 px-6 md:px-12 text-center max-w-5xl mx-auto relative overflow-hidden">
                <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-80 h-80 bg-coffeeAccent/5 rounded-full blur-3xl pointer-events-none"></div>
                <div class="space-y-10 z-10 relative">
                    <span class="font-en text-xs tracking-[0.5em] text-coffeeAccent uppercase block font-semibold">MESSAGE</span>
                    <h2 class="font-jp text-2xl md:text-4xl font-light tracking-[0.25em] leading-snug text-coffeeText">
                        美しい日常を、未来へつなぐ。
                    </h2>
                    <div class="gsap-fade-up space-y-6 max-w-3xl mx-auto">
                        <p class="font-jp text-sm md:text-base leading-[2.6] tracking-widest text-coffeeMuted font-light">
                            遠い異国のストーリーとして「消費」するのではなく、<br class="hidden sm:inline">
                            日本の感性豊かな人々や、最先端を走る現代企業のパートナーとして、<br class="hidden sm:inline">
                            日常の中に自然とフィットする美しく気高いかたちに仕上げる。<br>
                            それこそが、私たちが果たすべき編集であり、未来への役割だと信じています。
                        </p>
                        <p class="font-jp text-lg md:text-xl leading-[2.6] tracking-[0.2em] text-coffeeAccent pt-8 font-normal">
                            一杯のコーヒーから、すべてが美しく巡る明日へ。
                        </p>
                    </div>
                </div>
            </section>

            <!-- 7. CONTACT & HIGH-TRUST FOOTER -->
            <section id="contact" class="bg-coffeeCard border-t border-white/5 relative z-20">
                <div class="max-w-7xl mx-auto px-6 md:px-12 py-20 md:py-32">
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 lg:gap-24">
                        
                        <!-- Left Panel: Company Identity & Contact Method -->
                        <div class="lg:col-span-6 space-y-8">
                            <div class="space-y-2">
                                <span class="font-en text-xs tracking-[0.4em] text-coffeeAccent block font-semibold">CONTACT US</span>
                                <h2 class="font-en text-3xl tracking-[0.15em] text-coffeeText uppercase font-light">
                                    FUTURE CIRCULATION
                                </h2>
                            </div>
                            
                            <p class="font-jp text-xs leading-[2.2] tracking-widest text-coffeeMuted max-w-md font-light">
                                共同プロジェクトのご提案、各種イベントでのオリジナルギフト、オフィスへの定期コーヒー配送のご相談、OEM製作のお見積りなど、下記メールアドレスまたはSNSアカウントよりお気軽にお問い合わせください。
                            </p>

                            <!-- High Impact Contact Email Box -->
                            <div class="bg-coffeeBg/80 p-6 rounded border border-white/5 max-w-md transition-premium hover:border-coffeeAccent">
                                <span class="font-jp text-[10px] tracking-widest text-coffeeAccent block mb-1">E-mail お問合せ（代表窓口）</span>
                                <a href="mailto:myanmar.hope.shwedagon@gmail.com" class="font-en text-base sm:text-lg text-coffeeText hover:text-coffeeAccent transition-colors block font-medium underline underline-offset-4 tracking-wider break-all">
                                    myanmar.hope.shwedagon@gmail.com
                                </a>
                                <span class="font-jp text-[9px] text-coffeeMuted block mt-2">※法人のお客様のご相談も、こちらにて一括で承っております。</span>
                            </div>

                            <div class="flex gap-8 pt-4 text-xs tracking-[0.2em] font-en uppercase text-coffeeText">
                                <a href="https://www.instagram.com/myanmar.2015/" target="_blank" rel="noopener noreferrer" class="hover:text-coffeeAccent transition-colors flex items-center gap-1.5">
                                    Instagram ↗
                                </a>
                                <a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="hover:text-coffeeAccent transition-colors flex items-center gap-1.5">
                                    Online Store ↗
                                </a>
                            </div>
                        </div>

                        <!-- Right Panel: Strategic Navigation & Direct Call To Action -->
                        <div class="lg:col-span-6 flex flex-col justify-between items-start lg:items-end gap-12">
                            <div class="w-full grid grid-cols-2 gap-8 text-xs tracking-widest text-coffeeMuted">
                                <div class="space-y-4">
                                    <h4 class="text-coffeeText font-medium font-en tracking-[0.2em] text-[10px]">NAVIGATION</h4>
                                    <ul class="space-y-2.5 text-[11px] font-light">
                                        <li><a href="#about" class="hover:text-coffeeAccent transition-colors">わたしたちについて (ABOUT)</a></li>
                                        <li><a href="#coffee" class="hover:text-coffeeAccent transition-colors">提供するコーヒー (OUR COFFEE)</a></li>
                                        <li><a href="#products" class="hover:text-coffeeAccent transition-colors">展開ラインナップ (LINEUP)</a></li>
                                        <li><a href="#circulation" class="hover:text-coffeeAccent transition-colors">美しい循環への仕組み (CIRCULATION)</a></li>
                                    </ul>
                                </div>
                                <div class="space-y-4">
                                    <h4 class="text-coffeeText font-medium font-en tracking-[0.2em] text-[10px]">OUR CHANNELS</h4>
                                    <ul class="space-y-2.5 text-[11px] font-light">
                                        <li><a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="hover:text-coffeeAccent transition-colors">BASEオンラインストア ↗</a></li>
                                        <li><a href="https://www.instagram.com/myanmar.2015/" target="_blank" rel="noopener noreferrer" class="hover:text-coffeeAccent transition-colors">公式Instagram ↗</a></li>
                                    </ul>
                                </div>
                            </div>

                            <!-- CTA Buttons (No Dummy Links) -->
                            <div class="w-full flex flex-col sm:flex-row gap-4 justify-start lg:justify-end pt-8 lg:pt-0">
                                <a href="mailto:myanmar.hope.shwedagon@gmail.com" class="inline-block px-8 py-4 bg-coffeeAccent hover:bg-coffeeAccent/90 text-coffeeBg font-en font-semibold tracking-[0.2em] text-center text-[10px] uppercase rounded transition-premium shadow-xl">
                                    EMAIL FOR OEM (お問合せ)
                                </a>
                                <a href="https://myanmar.shopselect.net" target="_blank" rel="noopener noreferrer" class="inline-block px-8 py-4 bg-transparent border border-white/20 hover:border-coffeeAccent text-coffeeText hover:text-coffeeAccent font-en font-semibold tracking-[0.2em] text-center text-[10px] uppercase rounded transition-premium">
                                    ONLINE STORE (EC) ↗
                                </a>
                            </div>
                        </div>

                    </div>
                </div>
                
                <!-- Bottom Copyright (CSSDA Signature Style) -->
                <div class="max-w-7xl mx-auto px-6 md:px-12 py-8 border-t border-white/5 flex flex-col sm:flex-row justify-between items-center gap-4 text-[9px] text-coffeeMuted tracking-widest font-light">
                    <p>© FUTURE CIRCULATION Social Coffee Enterprise. All Rights Reserved.</p>
                    <p>Designed for Regenerative & Beautiful Future.</p>
                </div>
            </section>

        </div>
    </div>

    <!-- Complete System Script -->
    <script>
        // ==========================================
        // 1. Lenis Premium Smooth Scroll (Frictionless Feel)
        // ==========================================
        const lenis = new Lenis({
            duration: 1.5,
            easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
            smooth: true,
            wheelMultiplier: 0.95
        });

        function raf(time) {
            lenis.raf(time);
            requestAnimationFrame(raf);
        }
        requestAnimationFrame(raf);

        // Notify ScrollTrigger on Scroll
        lenis.on('scroll', ScrollTrigger.update);

        // ==========================================
        // 2. Preloader Exit Pipeline
        // ==========================================
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                const loader = document.getElementById('loader');
                if (loader) {
                    loader.style.opacity = '0';
                    loader.style.pointerEvents = 'none';
                    setTimeout(() => loader.remove(), 1000);
                }
                
                // Active Text reveals
                document.querySelectorAll('.reveal-mask').forEach(el => {
                    el.classList.add('active');
                });
            }, 1000);
        });

        // Fail-safe Preloader Shutoff
        setTimeout(() => {
            const loader = document.getElementById('loader');
            if (loader) {
                loader.style.opacity = '0';
                loader.style.pointerEvents = 'none';
                setTimeout(() => loader.remove(), 1000);
            }
        }, 3000);

        // ==========================================
        // 3. GSAP Orchestrated Transitions
        // ==========================================
        gsap.registerPlugin(ScrollTrigger);

        // Asymmetric Image Parallax Dynamics
        gsap.utils.toArray('.parallax-container').forEach(wrapper => {
            const img = wrapper.querySelector('.parallax-img');
            gsap.to(img, {
                yPercent: 15,
                ease: "none",
                scrollTrigger: {
                    trigger: wrapper,
                    start: "top bottom",
                    end: "bottom top",
                    scrub: true
                }
            });
        });

        // Soft Entrance Stagger
        gsap.utils.toArray('.gsap-fade-up').forEach(elem => {
            gsap.fromTo(elem, 
                { y: 35, opacity: 0 },
                { 
                    y: 0, 
                    opacity: 1, 
                    duration: 1.4, 
                    ease: "power3.out",
                    scrollTrigger: {
                        trigger: elem,
                        start: "top 88%",
                        toggleActions: "play none none none"
                    }
                }
            );
        });

        // ==========================================
        // 4. Products Editorial Accordion Action
        // ==========================================
        const accordions = document.querySelectorAll('.product-accordion');
        accordions.forEach(acc => {
            acc.addEventListener('click', (e) => {
                // If clicked an anchor within details, let browser handle click
                if (e.target.tagName.toLowerCase() === 'a') return;

                const details = acc.querySelector('.product-details');
                const isOpened = acc.classList.contains('active-acc');
                
                // Close all others seamlessly
                accordions.forEach(other => {
                    other.classList.remove('active-acc');
                    other.querySelector('.product-details').style.maxHeight = '0px';
                    other.querySelector('.product-details').style.opacity = '0';
                });

                if (!isOpened) {
                    acc.classList.add('active-acc');
                    details.style.maxHeight = details.scrollHeight + 40 + 'px';
                    details.style.opacity = '1';
                }
                
                // Reset GSAP positions so parallax updates cleanly with height changes
                setTimeout(() => {
                    ScrollTrigger.refresh();
                }, 600);
            });
        });

        // ==========================================
        // 5. Three.js Fine Atmospheric Dust Engine
        // ==========================================
        const canvas = document.getElementById('webgl-canvas');
        const scene = new THREE.Scene();
        
        // Deep background matching brand theme color with natural haze
        scene.fog = new THREE.FogExp2(0x0f0d0c, 0.05);

        const camera = new THREE.PerspectiveCamera(70, window.innerWidth / window.innerHeight, 0.1, 100);
        camera.position.z = 10;
        camera.position.y = 1;

        const renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 1400; // Ultra fluid optimization
        const posArray = new Float32Array(particlesCount * 3);
        const colorArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i += 3) {
            posArray[i] = (Math.random() - 0.5) * 30;
            posArray[i+1] = (Math.random() - 0.5) * 30;
            posArray[i+2] = (Math.random() - 0.5) * 30;

            const rand = Math.random();
            if(rand > 0.8) {
                // Elegant Terracotta gold accent
                colorArray[i] = 0.82; colorArray[i+1] = 0.55; colorArray[i+2] = 0.45;
            } else if (rand > 0.6) {
                // Muted Green Accent
                colorArray[i] = 0.38; colorArray[i+1] = 0.45; colorArray[i+2] = 0.37;
            } else {
                // Silky organic white
                colorArray[i] = 0.96; colorArray[i+1] = 0.95; colorArray[i+2] = 0.92;
            }
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        particlesGeometry.setAttribute('color', new THREE.BufferAttribute(colorArray, 3));

        // Programmatic texture generation for soft particles
        const createParticleTexture = () => {
            const pCanvas = document.createElement('canvas');
            pCanvas.width = 16;
            pCanvas.height = 16;
            const ctx = pCanvas.getContext('2d');
            const gradient = ctx.createRadialGradient(8, 8, 0, 8, 8, 8);
            gradient.addColorStop(0, 'rgba(255, 255, 255, 1)');
            gradient.addColorStop(0.4, 'rgba(255, 255, 255, 0.7)');
            gradient.addColorStop(1, 'rgba(255, 255, 255, 0)');
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, 16, 16);
            return new THREE.CanvasTexture(pCanvas);
        };

        const material = new THREE.PointsMaterial({
            size: 0.15,
            vertexColors: true,
            transparent: true,
            opacity: 0.35,
            map: createParticleTexture(),
            blending: THREE.AdditiveBlending,
            depthWrite: false
        });

        const particlesMesh = new THREE.Points(particlesGeometry, material);
        scene.add(particlesMesh);

        // Smooth Mouse Parallax tracking
        let mouseX = 0;
        let mouseY = 0;
        document.addEventListener('mousemove', (event) => {
            mouseX = (event.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(event.clientY / window.innerHeight) * 2 + 1;
        });

        // Relate Scroll to Camera Position
        gsap.to(camera.position, {
            y: -12,
            ease: "none",
            scrollTrigger: {
                trigger: document.body,
                start: "top top",
                end: "bottom bottom",
                scrub: 1.2
            }
        });

        const clock = new THREE.Clock();
        
        function tick() {
            const elapsedTime = clock.getElapsedTime();

            // Liquid Particle Flow
            particlesMesh.rotation.y = elapsedTime * 0.012;
            particlesMesh.rotation.x = Math.sin(elapsedTime * 0.04) * 0.05;
            
            // Lagged Mouse follow inertia (Award-Winning Standard)
            camera.position.x += (mouseX * 1.2 - camera.position.x) * 0.03;
            
            renderer.render(scene, camera);
            requestAnimationFrame(tick);
        }
        tick();

        // Responsive scaling
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

    </script>
</body>
</html>
