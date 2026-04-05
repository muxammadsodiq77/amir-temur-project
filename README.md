
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amir Temur: Adolat va Qudrat Merosi</title>
    
    <!-- Kutubxonalar -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Montserrat:wght@300;400;700&display=swap" rel="stylesheet">
    
    <script>
        /**
         * DIQQAT: Ovozli funksiyalar ishlashi uchun API KEY kerak.
         * Uni https://aistudio.google.com/ saytidan bepul olishingiz mumkin.
         * Olingan kalitni pastdagi qo'shtirnoq ichiga qo'ying:
         */
        const apiKey = "AIzaSyCe3KHntBtXqGu2pVr4_-yS3g3vxrHid3k"; 
        
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'temur-heritage-2026';
        const authorName = "Muxammadsodiq Xoshimov"; 

        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        temurid: {
                            900: '#0a1128',
                            800: '#1c2541',
                            gold: '#d4af37',
                            azure: '#3a506b',
                            teal: '#1a936f'
                        }
                    }
                }
            }
        };
    </script>

    <style>
        body { font-family: 'Montserrat', sans-serif; scroll-behavior: smooth; background-color: #f0f2f5; }
        .serif { font-family: 'Playfair Display', serif; }
        
        .gold-gradient {
            background: linear-gradient(135deg, #d4af37 0%, #f1e5ac 50%, #d4af37 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .islamic-bg {
            background-image: url('https://www.transparenttextures.com/patterns/islamic-art.png');
            background-color: #0a1128;
        }

        .glass {
            background: rgba(28, 37, 65, 0.85);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(212, 175, 55, 0.3);
        }

        .active-tab { border-left: 6px solid #d4af37 !important; background: rgba(212, 175, 55, 0.1); color: #d4af37 !important; }
        
        @keyframes pulse-glow {
            0% { box-shadow: 0 0 0 0 rgba(212, 175, 55, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(212, 175, 55, 0); }
            100% { box-shadow: 0 0 0 0 rgba(212, 175, 55, 0); }
        }
        .is-speaking {
            animation: pulse-glow 1.5s infinite;
            border-color: #d4af37 !important;
            background: #d4af37 !important;
            color: #0a1128 !important;
        }

        .chat-container { 
            height: 400px; 
            overflow-y: auto; 
        }

        .bot-msg { background: rgba(212, 175, 55, 0.1); border-left: 4px solid #d4af37; }
        
        /* Modal uslubi */
        #api-modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.8);
            z-index: 100;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
    </style>
</head>
<body class="text-temurid-900">

    <!-- API OGOHLANTIRISH MODALI -->
    <div id="api-modal">
        <div class="bg-white p-8 rounded-3xl max-w-md w-full text-center">
            <div class="text-5xl mb-4">🔑</div>
            <h3 class="text-2xl font-bold mb-4">API Kalit Topilmadi</h3>
            <p class="text-gray-600 mb-6">
                Ovozli funksiyalar (TTS) ishlashi uchun Google AI API kaliti kerak. 
                Uni <b>aistudio.google.com</b> saytidan bepul olib, kodning 16-qatoriga qo'ying.
            </p>
            <button onclick="document.getElementById('api-modal').style.display='none'" class="w-full bg-temurid-900 text-white py-3 rounded-xl font-bold">Tushunarli</button>
        </div>
    </div>

    <!-- HEADER -->
    <header class="relative min-h-screen flex items-center islamic-bg text-white overflow-hidden border-b-8 border-temurid-gold">
        <div class="absolute inset-0 bg-gradient-to-b from-transparent to-temurid-900 opacity-90"></div>
        
        <div class="container mx-auto px-6 relative z-10 text-center">
            <div class="mb-6">
                <span class="inline-block px-6 py-2 border border-temurid-gold text-temurid-gold rounded-full tracking-widest text-sm uppercase mb-4 bg-temurid-gold/5">
                    Raqamli Tarixiy Eksponat • 2026
                </span>
                <h1 class="serif text-7xl md:text-9xl mb-6 gold-gradient font-black tracking-tight">Amir Temur</h1>
                <p class="text-2xl md:text-5xl font-light text-gray-300 mb-10 italic">"Kuch — adolatdadir"</p>
            </div>

            <div class="flex flex-wrap justify-center gap-6">
                <button onclick="generateInsight()" class="bg-temurid-gold text-temurid-900 px-10 py-5 rounded-2xl font-bold hover:scale-105 transition-all shadow-xl flex items-center gap-3 text-lg">
                    <span>✨ Yangi Hikmat</span>
                </button>
                <button id="main-speak-btn" onclick="speakWithGemini('Kuch adolatdadir. Adolat esa har bir ishning asosidir.', this)" class="bg-white/10 backdrop-blur-xl border border-white/20 px-10 py-5 rounded-2xl font-bold hover:bg-white/20 transition-all flex items-center gap-3 text-lg">
                    <span>🔊 Tinglash</span>
                </button>
            </div>

            <div id="insight-box" class="mt-12 max-w-3xl mx-auto glass p-8 rounded-3xl text-2xl text-temurid-gold italic hidden animate-fade shadow-2xl"></div>
            
            <div class="mt-16 text-white/50 text-sm">
                Loyiha muallifi: <span class="text-temurid-gold font-bold" id="author-display"></span>
            </div>
        </div>
    </header>

    <main class="py-24 container mx-auto px-6 space-y-32">
        
        <!-- XRONOLOGIYA -->
        <section class="bg-white rounded-[3rem] shadow-2xl overflow-hidden border border-gray-100">
            <div class="grid grid-cols-1 lg:grid-cols-12">
                <div class="lg:col-span-4 bg-temurid-900 p-12 text-white">
                    <h2 class="serif text-4xl mb-10 border-b border-temurid-gold pb-6 text-temurid-gold">Tarixiy Davrlar</h2>
                    <div class="space-y-4">
                        <button onclick="changeStep(0)" id="btn-0" class="timeline-nav w-full text-left p-6 rounded-2xl transition-all active-tab">
                            <span class="block font-bold text-lg">1336 - 1370</span>
                            <span class="text-sm opacity-60">Yoshlik va Yuksalish</span>
                        </button>
                        <button onclick="changeStep(1)" id="btn-1" class="timeline-nav w-full text-left p-6 rounded-2xl transition-all">
                            <span class="block font-bold text-lg">1370 - 1390</span>
                            <span class="text-sm opacity-60">Yagona Saltanat</span>
                        </button>
                        <button onclick="changeStep(2)" id="btn-2" class="timeline-nav w-full text-left p-6 rounded-2xl transition-all">
                            <span class="block font-bold text-lg">1390 - 1405</span>
                            <span class="text-sm opacity-60">Jahon G'olibi</span>
                        </button>
                    </div>
                </div>

                <div id="timeline-wrapper" class="lg:col-span-8 p-16 flex flex-col justify-center">
                    <div class="flex justify-between items-center mb-10">
                        <h3 id="step-title" class="serif text-5xl text-temurid-900 font-bold">Yoshlik va Kamolot</h3>
                        <button onclick="speakCurrentStep(this)" class="w-16 h-16 bg-temurid-gold/20 text-temurid-900 rounded-full hover:scale-110 transition flex items-center justify-center">
                            <span class="text-2xl">🔊</span>
                        </button>
                    </div>
                    <div class="space-y-8">
                        <p id="step-desc" class="text-2xl text-gray-700 leading-relaxed italic font-light">
                            Amir Temur bir ming uch yuz o'ttiz oltinchi yilda Shahrisabzda dunyoga keldi. U yoshligidan jasur va o'tkir zehni bilan ajralib turdi.
                        </p>
                        <div class="bg-temurid-gold/10 p-8 rounded-[2rem] border-l-8 border-temurid-gold">
                            <p id="step-fact" class="text-lg text-gray-800 font-medium">Amir Temur shaxmat o'yinining mohir ustasi bo'lgan va murakkab strategiyalarni sevgan.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- CHAT -->
        <section class="max-w-5xl mx-auto">
            <div class="glass p-12 rounded-[4rem] shadow-2xl border-2 border-temurid-gold/20">
                <div class="text-center mb-12">
                    <h2 class="serif text-5xl text-temurid-gold mb-4">Sohibqiron bilan suhbat</h2>
                    <p class="text-gray-300 text-lg">Tarix, adolat va saltanat sirlari haqida so'rang</p>
                </div>

                <div id="chat-box" class="chat-container mb-8 space-y-6 p-8 bg-black/20 rounded-[2.5rem] border border-white/5">
                    <div class="p-6 rounded-3xl bot-msg text-xl flex justify-between items-start text-white">
                        <div>
                            <span class="text-temurid-gold font-bold block mb-2 text-sm uppercase tracking-widest">Amir Temur ✨</span>
                            <p class="leading-relaxed">Assalomu alaykum, ey kelajak vorisi. Bizning saltanatimiz haqida ne savolingiz bor?</p>
                        </div>
                        <button onclick="speakWithGemini(this.previousElementSibling.querySelector('p').innerText, this)" class="mt-4 text-temurid-gold text-2xl">🔊</button>
                    </div>
                </div>

                <div class="flex gap-4 p-2 bg-white rounded-3xl shadow-lg border border-gray-200">
                    <input type="text" id="user-input" placeholder="Savolingizni yozing..." 
                        class="flex-1 bg-transparent px-8 py-6 rounded-2xl focus:outline-none text-xl" 
                        onkeypress="if(event.key === 'Enter') askAI()">
                    <button onclick="askAI()" class="bg-temurid-900 text-white px-12 py-6 rounded-[1.5rem] font-bold hover:bg-temurid-800 transition-all text-lg">
                        Yuborish
                    </button>
                </div>
            </div>
        </section>
    </main>

    <footer class="islamic-bg text-white py-24 text-center border-t-8 border-temurid-gold">
        <div class="container mx-auto px-6">
            <h3 class="text-temurid-gold serif text-4xl mb-6 italic font-bold">"Adolat - najotdir"</h3>
            <p class="text-gray-400 max-w-xl mx-auto mb-8">
                Ushbu interaktiv loyiha Amir Temur bobomizning buyuk merosini 2026-yil texnologiyalari bilan uyg'unlashtiradi.
            </p>
            <div class="pt-10 border-t border-white/10 text-sm">
                Tayyorladi: <span class="text-temurid-gold font-bold" id="footer-author"></span> | © 2026
            </div>
        </div>
    </footer>

    <script>
        window.onload = function() {
            document.getElementById('author-display').innerText = authorName;
            document.getElementById('footer-author').innerText = authorName;
        };

        let currentAudio = null;

        function pcmToWav(pcmData, sampleRate) {
            const buffer = new ArrayBuffer(44 + pcmData.length * 2);
            const view = new DataView(buffer);
            const writeString = (offset, string) => {
                for (let i = 0; i < string.length; i++) view.setUint8(offset + i, string.charCodeAt(i));
            };
            writeString(0, 'RIFF');
            view.setUint32(4, 32 + pcmData.length * 2, true);
            writeString(8, 'WAVE');
            writeString(12, 'fmt ');
            view.setUint32(16, 16, true);
            view.setUint16(20, 1, true);
            view.setUint16(22, 1, true);
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, sampleRate * 2, true);
            view.setUint16(32, 2, true);
            view.setUint16(34, 16, true);
            writeString(36, 'data');
            view.setUint32(40, pcmData.length * 2, true);
            for (let i = 0; i < pcmData.length; i++) view.setInt16(44 + i * 2, pcmData[i], true);
            return new Blob([buffer], { type: 'audio/wav' });
        }

        async function speakWithGemini(text, btnElement) {
            if (currentAudio && !currentAudio.paused) {
                currentAudio.pause();
                currentAudio = null;
                btnElement.classList.remove('is-speaking');
                btnElement.innerText = "🔊";
                return;
            }
            
            if (!apiKey) {
                document.getElementById('api-modal').style.display = 'flex';
                return;
            }

            btnElement.classList.add('audio-loading');
            btnElement.innerText = "⏳";

            try {
                const cleanText = text.replace(/Amir Temur ✨:|Siz:/g, '').trim();
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: `Vazmin ovozda ayting: ${cleanText}` }] }],
                        generationConfig: {
                            responseModalities: ["AUDIO"],
                            speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: "Kore" } } }
                        }
                    })
                });
                const data = await response.json();
                const audioPart = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData);
                const pcmData = new Int16Array(atob(audioPart.inlineData.data).split('').map((c, i, a) => i % 2 === 0 ? (a[i+1].charCodeAt(0) << 8) | c.charCodeAt(0) : null).filter(v => v !== null));
                const wavBlob = pcmToWav(pcmData, 24000);
                const audio = new Audio(URL.createObjectURL(wavBlob));
                audio.onplay = () => {
                    btnElement.classList.remove('audio-loading');
                    btnElement.classList.add('is-speaking');
                    btnElement.innerText = "⏹️";
                    currentAudio = audio;
                };
                audio.onended = () => {
                    btnElement.classList.remove('is-speaking');
                    btnElement.innerText = "🔊";
                };
                audio.play();
            } catch (error) {
                btnElement.classList.remove('audio-loading');
                btnElement.innerText = "🔊";
            }
        }

        async function callGemini(prompt, systemInstruction = "") {
            if(!apiKey) return "AIzaSyCe3KHntBtXqGu2pVr4_-yS3g3vxrHid3k";
            try {
                const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`;
                const response = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: prompt }] }],
                        systemInstruction: systemInstruction ? { parts: [{ text: systemInstruction }] } : undefined
                    })
                });
                const result = await response.json();
                return result.candidates?.[0]?.content?.parts?.[0]?.text || "Javob topilmadi.";
            } catch (e) { return "Xatolik yuz berdi."; }
        }

        async function generateInsight() {
            const box = document.getElementById('insight-box');
            box.classList.remove('hidden');
            box.innerText = "⏳ Yuklanmoqda...";
            const insight = await callGemini("Amir Temurning 'Temur tuzuklari'dan bitta qisqa hikmat bering.");
            box.innerText = `“${insight.trim()}”`;
        }

        async function askAI() {
            const input = document.getElementById('user-input');
            const chatBox = document.getElementById('chat-box');
            if (!input.value.trim()) return;
            const userText = input.value;
            chatBox.innerHTML += `<div class="p-6 rounded-3xl bg-white/10 text-right ml-20 text-white"><p class="text-xl">${userText}</p></div>`;
            input.value = "";
            chatBox.scrollTop = chatBox.scrollHeight;
            const response = await callGemini(userText, "Siz Amir Temursiz. Vazmin va donishmand ohangda javob bering.");
            const resId = 'ai-' + Date.now();
            chatBox.innerHTML += `<div class="p-6 rounded-3xl bot-msg mr-20 flex justify-between items-start text-white"><div><span class="text-temurid-gold font-bold block mb-2 text-sm uppercase tracking-widest">Amir Temur ✨</span><p id="${resId}" class="text-xl leading-relaxed">${response}</p></div><button onclick="speakWithGemini(document.getElementById('${resId}').innerText, this)" class="mt-4 text-temurid-gold text-2xl">🔊</button></div>`;
            chatBox.scrollTop = chatBox.scrollHeight;
        }

        const steps = [
            { t: "Yoshlik va Yuksalish", d: "Amir Temur 1336-yil Shahrisabzda tug'ilgan. U yoshligidan harbiy san'at va davlat boshqaruviga qiziqqan.", f: "Uning ismi 'Temur' - mustahkam degan ma'noni anglatadi." },
            { t: "Yagona Saltanat", d: "1370-yilda Movarounnahrni birlashtirib, Samarqandni poytaxt etib belgiladi.", f: "Uning davrida Samarqand dunyo poytaxtiga aylandi." },
            { t: "Jahon G'olibi", d: "Temur hayoti davomida birorta jangda mag'lub bo'lmagan buyuk sarkardadir.", f: "35 yillik yurishlar davomida u 27 mamlakatni birlashtirdi." }
        ];

        function changeStep(i) {
            document.querySelectorAll('.timeline-nav').forEach(b => b.classList.remove('active-tab'));
            document.getElementById('btn-' + i).classList.add('active-tab');
            document.getElementById('step-title').innerText = steps[i].t;
            document.getElementById('step-desc').innerText = steps[i].d;
            document.getElementById('step-fact').innerText = steps[i].f;
        }

        function speakCurrentStep(btn) {
            speakWithGemini(document.getElementById('step-desc').innerText, btn);
        }
    </script>
</body>
</html>
