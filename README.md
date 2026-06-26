<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حصن المسلم الرقمي | Digital Azkar</title>
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #f4f7f5 0%, #e6ebe7 100%);
            --card-bg: rgba(255, 255, 255, 0.9);
            --text-main: #0f2c22;
            --text-sub: #536c63;
            --primary: #114232; /* أخضر فاخر */
            --accent: #bc9853; /* ذهبي ملكي */
            --success: #27ae60;
            --shadow: 0 10px 30px rgba(17, 66, 50, 0.08);
            --card-border: 1px solid rgba(188, 152, 83, 0.15);
        }

        [data-theme="dark"] {
            --bg-gradient: linear-gradient(135deg, #09120e 0%, #0f1e17 100%);
            --card-bg: rgba(23, 38, 31, 0.85);
            --text-main: #f1f5f3;
            --text-sub: #a3b8b0;
            --primary: #1b4d3e;
            --accent: #dfb76c;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            --card-border: 1px solid rgba(223, 183, 108, 0.2);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: var(--bg-gradient);
            color: var(--text-main);
            padding: 30px 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            transition: background 0.4s ease;
        }

        /* الهيدر الفاخر */
        header {
            width: 100%;
            max-width: 650px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 35px;
            padding: 15px 20px;
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: var(--shadow);
            border: var(--card-border);
        }

        header h1 {
            font-size: 22px;
            font-weight: 700;
            color: var(--accent);
            letter-spacing: 0.5px;
        }

        .controls {
            display: flex;
            gap: 10px;
        }

        .controls button {
            background: var(--primary);
            color: #fff;
            border: 1px solid rgba(255,255,255,0.1);
            padding: 10px 18px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 600;
            font-size: 14px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }

        .controls button:hover {
            transform: translateY(-2px);
            background: var(--accent);
            color: #09120e;
        }

        .container {
            width: 100%;
            max-width: 650px;
        }

        /* القائمة الرئيسية المصممة كبلاطات فاخرة */
        .main-menu {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        @media (max-width: 480px) {
            .main-menu { grid-template-columns: 1fr; }
        }

        .menu-item {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            padding: 30px 20px;
            border-radius: 22px;
            text-align: center;
            cursor: pointer;
            box-shadow: var(--shadow);
            border: var(--card-border);
            font-size: 19px;
            font-weight: bold;
            color: var(--text-main);
            position: relative;
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
        }

        .menu-item::before {
            content: '';
            position: absolute;
            top: 0; right: 0; width: 6px; height: 100%;
            background: var(--accent);
        }

        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(188, 152, 83, 0.15);
            border-color: var(--accent);
        }

        /* شاشة عرض الأذكار */
        .dhikr-section {
            display: none;
        }

        .back-btn {
            background: var(--card-bg);
            border: var(--card-border);
            color: var(--text-main);
            padding: 10px 22px;
            border-radius: 30px;
            cursor: pointer;
            margin-bottom: 25px;
            font-weight: 600;
            box-shadow: var(--shadow);
            transition: all 0.3s ease;
        }

        .back-btn:hover {
            background: var(--primary);
            color: #fff;
            transform: translateX(-3px);
        }

        /* كروت الأذكار */
        .dhikr-card {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            padding: 40px 30px 25px 30px;
            border-radius: 24px;
            box-shadow: var(--shadow);
            text-align: center;
            margin-bottom: 25px;
            position: relative;
            border: var(--card-border);
            transition: transform 0.3s ease;
        }

        .settings-dot {
            position: absolute;
            top: 15px;
            left: 15px;
            cursor: pointer;
            font-size: 20px;
            opacity: 0.5;
            transition: opacity 0.3s;
        }
        html[dir="ltr"] .settings-dot { left: auto; right: 15px; }
        .settings-dot:hover { opacity: 1; }

        .color-picker-panel {
            display: none;
            background: rgba(0, 0, 0, 0.04);
            padding: 12px;
            border-radius: 14px;
            margin-top: 20px;
            justify-content: center;
            gap: 12px;
            align-items: center;
            animation: fadeIn 0.3s ease;
        }

        .color-option {
            width: 28px;
            height: 28px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid #fff;
            box-shadow: 0 3px 8px rgba(0,0,0,0.15);
        }

        .dhikr-clickable-area {
            cursor: pointer;
        }

        .dhikr-text {
            font-size: 22px;
            line-height: 2;
            font-weight: 600;
            margin-bottom: 20px;
            word-wrap: break-word;
        }

        .dhikr-translation {
            font-size: 15px;
            color: var(--text-sub);
            margin-bottom: 30px;
            line-height: 1.6;
            font-style: italic;
        }

        /* العداد الدائري الأنيق */
        .counter-badge {
            background: var(--primary);
            color: #fff;
            padding: 12px 35px;
            border-radius: 50px;
            font-weight: 700;
            font-size: 20px;
            display: inline-block;
            box-shadow: 0 5px 15px rgba(17, 66, 50, 0.2);
            border: 2px solid var(--accent);
            transition: all 0.3s ease;
        }

        .completed {
            opacity: 0.6;
            border-color: var(--success) !important;
        }

        .completed .counter-badge {
            background: var(--success) !important;
            border-color: var(--success) !important;
            box-shadow: none;
        }

        /* رسالة النجاح الكبرى */
        .congrats-message {
            background: linear-gradient(135deg, #27ae60 0%, #1e8449 100%);
            color: white;
            padding: 25px;
            border-radius: 20px;
            text-align: center;
            font-size: 22px;
            font-weight: bold;
            margin-top: 25px;
            box-shadow: 0 10px 25px rgba(39, 174, 96, 0.3);
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            display: none;
            border: 2px solid rgba(255,255,255,0.2);
        }

        @keyframes popIn {
            0% { transform: scale(0.8); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        html[dir="ltr"] .menu-item::before { right: auto; left: 0; }
        html[dir="ltr"] .back-btn:hover { transform: translateX(3px); }
    </style>
</head>
<body>

    <header>
        <h1 id="main-title">الأذكار اليومية</h1>
        <div class="controls">
            <button onclick="toggleLanguage()" id="lang-btn">English</button>
            <button onclick="toggleTheme()" id="theme-btn">🌙</button>
        </div>
    </header>

    <div class="container">
        <!-- القائمة الرئيسية المصلحة -->
        <div id="main-menu" class="main-menu"></div>

        <!-- صفحة الأذكار المنفردة -->
        <div id="dhikr-section" class="dhikr-section">
            <button class="back-btn" onclick="showMainMenu()" id="back-btn">⬅ عودة للقائمة</button>
            <div id="dhikr-container"></div>
            <div id="congrats-box" class="congrats-message"></div>
        </div>
    </div>

    <script>
        // قاعدة بيانات كاملة للأدعية وبدون أي اختصارات أو نقاط
        const azkarData = {
            morning: {
                title: { ar: "أذكار الصباح", en: "Morning Azkar" },
                items: [
                    { ar: "أَصْبَحْنَا وَأَصْبَحَ المُلْكُ لِلَّهِ وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ المُلْكُ وَلَهُ الحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ، رَبِّ أَسْأَلُكَ خَيْرَ مَا فِي هَذَا اليَوْمِ وَخَيْرَ مَا بَعْدَهُ، وَأَعُوذُ بِكَ مِنْ شَرِّ مَا فِي هَذَا اليَوْمِ وَشَرِّ مَا بَعْدَهُ، رَبِّ أَعُوذُ بِكَ مِنَ الكَسَلِ وَسُوءِ الكِبَرِ، رَبِّ أَعُوذُ بِكَ مِنْ عَذَابٍ فِي النَّارِ وَعَذَابٍ فِي القَبْرِ.", en: "We have reached the morning and at this very time unto Allah belongs all sovereignty and praise. None has the right to be worshipped except Allah, alone, without partner, to Him belongs all sovereignty and praise and He is over all things omnipotent.", count: 1 },
                    { ar: "اللَّهُمَّ بِكَ أَصْبَحْنَا، وَبِكَ أَمْسَيْنَا، وَبِكَ نَحْيَا، وَبِكَ نَمُوتُ، وَإِلَيْكَ النُّشُورُ.", en: "O Allah, by Your leave we have reached the morning and by Your leave we have reached the evening, by Your leave we live and by Your leave we die and unto You is our resurrection.", count: 1 },
                    { ar: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ: عَدَدَ خَلْقِهِ، وَرِضَا نَفْسِهِ، وَزِنَةَ عَرْشِهِ، وَمِدَادَ كَلِمَاتِهِ.", en: "Glory be to Allah and His is the praise, according to the number of His creation, and according to His pleasure, and according to the weight of His Throne, and according to the ink of His words.", count: 3 },
                    { ar: "يَا حَيُّ يَا قَيُّومُ بِرَحْمَتِكَ أَسْتَغيثُ أَصْلِحْ لِي شَأْنِي كُلَّهُ وَلَا تَكِلْنِي إِلَى نَفْسِي طَرْفَةَ عَيْنٍ.", en: "O Ever Living One, O Sustainer of all, by Your mercy I call upon You to set right all my affairs. Do not leave me to myself even for the blink of an eye.", count: 1 }
                ]
            },
            evening: {
                title: { ar: "أذكار المساء", en: "Evening Azkar" },
                items: [
                    { ar: "أَمْسَيْنَا وَأَمْسَى المُلْكُ لِلَّهِ وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ المُلْكُ وَلَهُ الحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ، رَبِّ أَسْأَلُكَ خَيْرَ مَا فِي هَذِهِ اللَّيْلَةِ وَخَيْرَ مَا بَعْدَهَا، وَأَعُوذُ بِكَ مِنْ شَرِّ مَا فِي هَذِهِ اللَّيْلَةِ وَشَرِّ مَا بَعْدَهَا.", en: "We have reached the evening and at this very time unto Allah belongs all sovereignty and praise. None has the right to be worshipped except Allah, alone, without partner.", count: 1 },
                    { ar: "اللَّهُمَّ بِكَ أَمْسَيْنَا، وَبِكَ أَصْبَحْنَا، وَبِكَ نَحْيَا، وَبِكَ نَمُوتُ، وَإِلَيْكَ المَصِيرُ.", en: "O Allah, by Your leave we have reached the evening and by Your leave we have reached the morning, by Your leave we live and by Your leave we die and unto You is our return.", count: 1 },
                    { ar: "أَعُوذُ بِكَلِمَاتِ اللَّهِ التَّامَّاتِ مِنْ شَرِّ مَا خَلَقَ.", en: "I seek refuge in the Perfect Words of Allah from the evil of what He has created.", count: 3 }
                ]
            },
            istighfar: {
                title: { ar: "الاستغفار المكثف", en: "Abundant Istighfar" },
                items: [
                    { ar: "أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ.", en: "I seek Allah's forgiveness and turn to Him in repentance.", count: 100 },
                    { ar: "اللَّهُمَّ أَنْتَ رَبِّي لَا إِلَهَ إِلَّا أَنْتَ، خَلَقْتَنِي وَأَنَا عَبْدُكَ، وَأَنَا عَلَى عَهْدِكَ وَوَعْدِكَ مَا اسْتَطَعْتُ، أَعُوذُ بِكَ مِنْ شَرِّ مَا صَنَعْتُ، أَبُوءُ لَكَ بِنِعْمَتِكَ عَلَيَّ، وَأَبُوءُ لَكَ بِذَنْبِي فَاغْفِرْ لِي، فَإِنَّهُ لَا يَغْفِرُ الذُّنُوبَ إِلَّا أَنْتَ.", en: "O Allah, You are my Lord, there is none worthy of worship but You. You created me and I am your slave. I keep Your covenant, and my pledge to You so far as I am able. I seek refuge in You from the evil of what I have done. I admit to Your blessings upon me, and I admit to my misdeeds. Forgive me, for there is none who may forgive sins but You.", count: 3 },
                    { ar: "أَسْتَغْفِرُ اللَّهَ العَظِيمَ الَّذِي لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ وَأَتُوبُ إِلَيْهِ.", en: "I seek the forgiveness of Allah the Almighty, whom there is no deity except Him, The Living, The Sustainer, and I repent to Him.", count: 10 },
                    { ar: "رَبِّ اغْفِرْ لِي وَتُبْ عَلَيَّ إِنَّكَ أَنْتَ التَّوَّابُ الرَّحِيمُ.", en: "My Lord, forgive me and accept my repentance, You are indeed the Accepting of Repentance, the Most Merciful.", count: 30 },
                    { ar: "اللَّهُمَّ إِنِّي ظَلَمْتُ نَفْسِي ظُلْمًا كَثِيرًا، وَلَا يَغْفِرُ الذُّنُوبَ إِلَّا أَنْتَ، فَاغْفِرْ لِي مَغْفِرَةً مِنْ عِنْدِكَ، وَارْحَمْنِي إِنَّكَ أَنْتَ الغَفُورُ الرَّحِيمُ.", en: "O Allah, I have greatly wronged myself, and no one forgives sins except You. So grant me forgiveness from You and have mercy on me. You are the Forgiving, the Merciful.", count: 5 }
                ]
            },
            sleep: {
                title: { ar: "أذكار قبل النوم", en: "Before Sleeping" },
                items: [
                    { ar: "بِاسْمِكَ اللَّهُمَّ أَمُوتُ وَأَحْيَا.", en: "In Your name, O Allah, I die and I live.", count: 1 },
                    { ar: "اللَّهُ لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ لَا تَأْخُذُهُ سِنَةٌ وَلَا نَوْمٌ لَهُ مَا فِي السَّمَاوَاتِ وَمَا فِي الْأَرْضِ مَنْ ذَا الَّذِي يَشْفَعُ عِنْدَهُ إِلَّا بِإِذْنِهِ يَعْلَمُ مَا بَيْنَ أَيْدِيهِمْ وَمَا خَلْفَهُمْ وَلَا يُحِيطُونَ بِشَيْءٍ مِنْ عِلْمِهِ إِلَّا بِمَا شَاءَ وَسِعَ كُرْسِيُّهُ السَّمَاوَاتِ وَالْأَرْضَ وَلَا يَئُودُهُ حِفْظُهُمَا وَهُوَ الْعَلِيُّ الْعَظِيمُ.", en: "Allah! There is no deity except Him, the Ever-Living, the Sustainer of existence. Neither drowsiness overtakes Him nor sleep. To Him belongs whatever is in the heavens and whatever is on the earth. Who is it that can intercede with Him except by His permission? He knows what is presently before them and what will be after them, and they encompass not a thing of His knowledge except for what He wills. His Kursi extends over the heavens and the earth, and their preservation tires Him not. And He is the Most High, the Most Great.", count: 1 },
                    { ar: "قُلْ هُوَ اللَّهُ أَحَدٌ، اللَّهُ الصَّمَدُ، لَمْ يَلِدْ وَلَمْ يُولَدْ، وَلَمْ يَكُنْ لَهُ كُفُوًا أَحَدٌ.", en: "Say, 'He is Allah, [who is] One. Allah, the Eternal Refuge. He neither begets nor is born, Nor is there to Him any equivalent.'", count: 1 }
                ]
            },
            waking: {
                title: { ar: "أذكار الاستيقاظ", en: "Waking Up" },
                items: [
                    { ar: "الْحَمْدُ لِلَّهِ الَّذِي أَحْيَانَا بَعْدَ مَا أَمَاتَنَا وَإِلَيْهِ النُّشُورُ.", en: "Praise is to Allah Who gives us life after He has caused us to die and to Him is the return.", count: 1 },
                    { ar: "الْحَمْدُ لِلَّهِ الَّذِي عَافَانِي فِي جَسَدِي، وَرَدَّ عَلَيَّ رُوحِي، وَأَذِنَ لِي بِذِكْرِهِ.", en: "Praise is to Allah Who gave strength to my body and returned my soul to me and permitted me to remember Him.", count: 1 }
                ]
            },
            enter_bathroom: {
                title: { ar: "دخول الحمام", en: "Entering the Bathroom" },
                items: [
                    { ar: "بِسْمِ اللَّهِ، اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْخُبُثِ وَالْخَبَائِثِ.", en: "In the name of Allah. O Allah, I seek refuge in You from the male and female evil spirits.", count: 1 }
                ]
            },
            exit_bathroom: {
                title: { ar: "خروج الحمام", en: "Leaving the Bathroom" },
                items: [
                    { ar: "غُفْرَانَكَ.", en: "I ask for Your forgiveness.", count: 1 }
                ]
            }
        };

        const colorThemes = [
            { name: "Default", bg: "var(--card-bg)", text: "var(--text-main)" },
            { name: "Emerald", bg: "rgba(212, 237, 218, 0.95)", text: "#155724" },
            { name: "Amber", bg: "rgba(255, 243, 205, 0.95)", text: "#856404" },
            { name: "Sapphire", bg: "rgba(204, 229, 255, 0.95)", text: "#004085" }
        ];

        let currentLang = 'ar';
        let activeDhikrCounts = [];

        function initMenu() {
            const menuContainer = document.getElementById('main-menu');
            menuContainer.innerHTML = '';
            
            for (const key in azkarData) {
                const item = azkarData[key];
                const btn = document.createElement('div');
                btn.className = 'menu-item';
                btn.innerText = item.title[currentLang];
                btn.onclick = () => showDhikr(key);
                menuContainer.appendChild(btn);
            }
            
            document.getElementById('main-title').innerText = currentLang === 'ar' ? 'حصن المسلم الرقمي' : 'Digital Fort of Muslim';
            document.getElementById('back-btn').innerText = currentLang === 'ar' ? '⬅ عودة للقائمة الرئيسية' : '⬅ Back to Main Menu';
        }

        function showDhikr(category) {
            document.getElementById('main-menu').style.display = 'none';
            document.getElementById('dhikr-section').style.display = 'block';
            
            const congratsBox = document.getElementById('congrats-box');
            congratsBox.style.display = 'none';

            const container = document.getElementById('dhikr-container');
            container.innerHTML = '';
            
            const items = JSON.parse(JSON.stringify(azkarData[category].items));
            activeDhikrCounts = items.map(item => item.count);

            items.forEach((item, index) => {
                const card = document.createElement('div');
                card.className = 'dhikr-card';
                card.id = `card-${index}`;

                let colorOptionsHTML = colorThemes.map(theme => 
                    `<div class="color-option" style="background: ${theme.bg};" onclick="changeCardColor(${index}, '${theme.bg}', '${theme.text}', event)"></div>`
                ).join('');

                card.innerHTML = `
                    <div class="settings-dot" onclick="toggleColorPicker(${index}, event)">⚙️</div>
                    <div class="dhikr-clickable-area" onclick="decrementCounter(${index})">
                        <div class="dhikr-text">${item.ar}</div>
                        <div class="dhikr-translation">${item.en}</div>
                        <div class="counter-badge" id="count-${index}">${activeDhikrCounts[index]}</div>
                    </div>
                    <div class="color-picker-panel" id="picker-${index}">
                        <span style="font-weight: bold; margin-left: 5px;">${currentLang === 'ar' ? 'اللون:' : 'Color:'}</span>
                        ${colorOptionsHTML}
                    </div>
                `;

                container.appendChild(card);
            });
        }

        function toggleColorPicker(index, event) {
            event.stopPropagation();
            const panel = document.getElementById(`picker-${index}`);
            panel.style.display = panel.style.display === 'flex' ? 'none' : 'flex';
        }

        function changeCardColor(index, bgColor, textColor, event) {
            event.stopPropagation();
            const card = document.getElementById(`card-${index}`);
            card.style.background = bgColor;
            card.style.color = textColor;
            
            const translationText = card.querySelector('.dhikr-translation');
            if(translationText) translationText.style.color = textColor;
        }

        function decrementCounter(index) {
            if (activeDhikrCounts[index] > 0) {
                activeDhikrCounts[index]--;
                const badge = document.getElementById(`count-${index}`);
                badge.innerText = activeDhikrCounts[index];
                
                if (activeDhikrCounts[index] === 0) {
                    const card = document.getElementById(`card-${index}`);
                    card.classList.add('completed');
                    badge.innerText = currentLang === 'ar' ? 'أحسنت ✓' : 'Done ✓';
                    checkAllCompleted();
                }
            }
        }

        function checkAllCompleted() {
            const allDone = activeDhikrCounts.every(count => count === 0);
            if (allDone) {
                const congratsBox = document.getElementById('congrats-box');
                congratsBox.innerText = currentLang === 'ar' ? '🎉 مبروك لقد أنهيت الدعاء بنجاح 🎉' : '🎉 Congratulations! You have successfully completed the Azkar 🎉';
                congratsBox.style.display = 'block';
                congratsBox.scrollIntoView({ behavior: 'smooth' });
            }
        }

        function showMainMenu() {
            document.getElementById('dhikr-section').style.display = 'none';
            document.getElementById('main-menu').style.display = 'grid';
        }

        function toggleTheme() {
            const body = document.body;
            const btn = document.getElementById('theme-btn');
            if (body.getAttribute('data-theme') === 'dark') {
                body.removeAttribute('data-theme');
                btn.innerText = '🌙';
            } else {
                body.setAttribute('data-theme', 'dark');
                btn.innerText = '☀️';
            }
        }

        function toggleLanguage() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
            document.documentElement.lang = currentLang;
            document.getElementById('lang-btn').innerText = currentLang === 'ar' ? 'English' : 'العربية';
            initMenu();
            showMainMenu();
        }

        initMenu();
    </script>
</body>
</html> 
