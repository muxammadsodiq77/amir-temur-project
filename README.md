<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amir Temur: Adolat va Qudrat Merosi</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Montserrat:wght@300;400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    
    <script>
        // API kaliti muhit tomonidan taqdim etiladi
        const apiKey = ""; 

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
        body { font-family: 'Montserrat', sans-serif; scroll-behavior: smooth; }
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
            backdrop-filter: blur(12px);
            border: 1px solid rgba(212, 175, 55, 0.3);
        }
        
        .active-tab { 
            border-bottom: 4px solid #d4af37 !important; 
            color: #d4af37 !important; 
            background: rgba(255, 255, 255, 0.05);
        }
        
        .is-speaking {
            animation: pulse-glow 1.5s infinite;
            border: 2px solid #d4af37 !important;
        }

        @keyframes pulse-glow {
            0% { box-shadow: 0 0 0 0 rgba(212, 175, 55, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(212, 175, 55, 0); }
            100% { box-shadow: 0 0 0 0 rgba(212, 175, 55, 0); }
        }
        
        .chat-container { height: 450px; overflow-y: auto; scrollbar-width: thin; }
        .bot-msg { background: rgba(212, 175, 55, 0.1); border-left: 4px solid #d4af37; }
        
        .loading-spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin { to { transform: rotate(360deg); } }
    </style>
</head>
<body class="bg-[#f8fafc] text-slate-900">

    <!-- Header -->
    <header class="relative min-h-screen flex items-center islamic-bg text-white overflow-hidden">
        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-temurid-900/80 to-temurid-900"></div>
        <div class="container mx-auto px-6 relative z-10 text-center">
            <div class="flex flex-col items-center mb-8">
                <span class="inline-block px-6 py-2 border-2 border-temurid-gold/50 text-temurid-gold rounded-full tracking-widest text-sm uppercase mb-4 bg-temurid-gold/5 italic">
                    Interaktiv Tarixiy Platforma
                </span>
            </div>
            <h1 class="serif text-7xl md:text-9xl mb-6 gold-gradient font-black tracking-tighter">Amir Temur</h1>
            <p class="text-2xl md:text-5xl font-light text-blue-100 mb-10 italic">"Kuch — adolatdadir"</p>
            
            <div class="flex flex-wrap justify-center gap-6">
                <button onclick="generateInsight(this)" class="bg-temurid-gold text-temurid-900 px-10 py-5 rounded-2xl font-bold hover:scale-105 active:scale-95 transition-all shadow-2xl flex items-center gap-3 min-w-[220px] justify-center">
                    <i class="fa-solid fa-wand-magic-sparkles"></i> <span>Yangi Hikmat</span>
                </button>
                <button onclick="speakText('Kuch adolatdadir. Adolat esa har bir ishning asosidir.', this)" class="bg-white/10 backdrop-blur-xl border border-white/20 px-10 py-5 rounded-2xl font-bold hover:bg-white/20 transition-all flex items-center gap-3">
                    <i class="fa-solid fa-volume-high"></i> Ovozli tinglash
                </button>
            </div>
            
            <div id="insight-box" class="mt-12 max-w-3xl mx-auto glass p-8 rounded-3xl text-2xl text-temurid-gold italic hidden border-2 border-temurid-gold/30"></div>
        </div>
    </header>

    <main class="py-24 container mx-auto px-6 space-y-32">
        
        <!-- Xronologiya -->
        <section class="bg-white rounded-[3rem] shadow-2xl border border-slate-200 overflow-hidden">
            <div class="grid grid-cols-1 lg:grid-cols-12">
                <div class="lg:col-span-4 bg-temurid-900 p-12 text-white flex flex-col justify-between">
                    <div>
                        <h2 class="serif text-4xl mb-8 border-b-2 border-temurid-gold/30 pb-6 flex items-center gap-3 text-temurid-gold">
                            <i class="fa-solid fa-calendar-days"></i> Tarixiy Davrlar
                        </h2>
                        <div class="space-y-4">
                            <button onclick="changeStep(0)" id="btn-0" class="timeline-nav w-full text-left p-6 rounded-2xl hover:bg-white/5 transition-all active-tab group">
                                <span class="block text-temurid-gold font-bold text-xl mb-1">1336 — 1370</span>
                                <span class="text-sm opacity-60">Yoshlik yillari</span>
                            </button>
                            <button onclick="changeStep(1)" id="btn-1" class="timeline-nav w-full text-left p-6 rounded-2xl hover:bg-white/5 transition-all group">
                                <span class="block text-temurid-gold font-bold text-xl mb-1">1370 — 1390</span>
                                <span class="text-sm opacity-60">Saltanat Tiklanishi</span>
                            </button>
                            <button onclick="changeStep(2)" id="btn-2" class="timeline-nav w-full text-left p-6 rounded-2xl hover:bg-white/5 transition-all group">
                                <span class="block text-temurid-gold font-bold text-xl mb-1">1390 — 1405</span>
                                <span class="text-sm opacity-60">Buyuk Zafarlar</span>
                            </button>
                        </div>
                    </div>
                </div>
                
                <div id="timeline-content" class="lg:col-span-8 p-16 flex flex-col justify-center bg-slate-50/50">
                    <div class="flex justify-between items-start mb-8">
                        <h3 id="step-title" class="serif text-5xl text-temurid-800 font-black">Yoshlik va Kamolot</h3>
                        <button onclick="speakText(document.getElementById('step-desc').innerText, this)" class="bg-temurid-gold/10 p-4 rounded-full hover:bg-temurid-gold/30 transition text-xl text-temurid-gold">🔊</button>
                    </div>
                    <div class="space-y-8">
                        <p id="step-desc" class="text-2xl text-slate-700 leading-relaxed font-light italic">Amir Temur bir ming uch yuz o'ttiz oltinchi yilda Shahrisabzda dunyoga keldi. U yoshligidan jasur va o'tkir zehni bilan ajralib turdi.</p>
                        <div class="bg-white p-8 rounded-[2rem] border-l-8 border-temurid-gold shadow-lg">
                            <h4 class="font-bold text-temurid-900 mb-3 uppercase tracking-wider text-sm flex items-center gap-2">
                                <i class="fa-solid fa-lightbulb text-temurid-gold"></i> Tarixiy fakt:
                            </h4>
                            <p id="step-fact" class="text-lg text-slate-600 leading-relaxed italic">Amir Temur shaxmat o'yinining mohir ustasi bo'lgan.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- AI Chat Section -->
        <section class="max-w-5xl mx-auto" id="muloqot">
            <div class="glass p-12 rounded-[3.5rem] shadow-2xl border-2 border-temurid-gold/20 relative overflow-hidden islamic-bg">
                <div class="absolute top-0 left-0 w-full h-2 bg-gradient-to-r from-temurid-gold via-white to-temurid-gold"></div>
                <div class="text-center mb-10 relative z-10">
                    <i class="fa-solid fa-crown text-temurid-gold text-4xl mb-4"></i>
                    <h2 class="serif text-4xl text-white mb-2">Sohibqiron bilan muloqot</h2>
                    <p class="text-blue-200 opacity-80">Savollaringizga Temur Tuzuklari asosida javob oling</p>
                </div>
                
                <div id="chat-box" class="chat-container mb-8 space-y-6 p-8 bg-black/40 rounded-[2rem] border border-white/5 relative z-10">
                    <div class="flex flex-col items-start max-w-[85%]">
                        <div class="p-6 rounded-2xl bot-msg text-xl text-white shadow-lg relative">
                            <span class="text-temurid-gold font-bold text-xs uppercase block mb-2 tracking-widest">Amir Temur ✨</span>
                            <p id="welcome-text" class="leading-relaxed italic">Assalomu alaykum, ey kelajak vorisi. Bizning saltanatimiz haqida ne savolingiz bor? Savol bering, javobini bizdan ovozli tinglang.</p>
                            <button onclick="speakText(document.getElementById('welcome-text').innerText, this)" class="mt-4 text-temurid-gold text-sm flex items-center gap-2 hover:underline">
                                <i class="fa-solid fa-volume-high"></i> Ovozli eshitish
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="flex flex-col md:flex-row gap-4 relative z-10">
                    <input type="text" id="user-input" placeholder="Savolingizni shu yerga yozing..." 
                           class="flex-1 px-8 py-5 rounded-2xl bg-white/10 border border-white/20 focus:outline-none focus:ring-4 focus:ring-temurid-gold/40 text-white text-xl placeholder:text-white/40" 
                           onkeypress="if(event.key === 'Enter') askAI()">
                    <button id="send-btn" onclick="askAI()" class="bg-temurid-gold text-temurid-900 px-12 py-5 rounded-2xl font-black hover:bg-yellow-400 active:scale-95 shadow-2xl transition-all uppercase tracking-wider flex items-center justify-center gap-2">
                        Yuborish <i class="fa-solid fa-paper-plane"></i>
                    </button>
                </div>
            </div>
        </section>

    </main>

    <footer class="islamic-bg text-white py-16 text-center border-t-8 border-temurid-gold">
        <div class="container mx-auto px-6">
            <h3 class="text-temurid-gold serif text-4xl mb-6 italic font-bold">"ADOLAT - NAJOTDIR"</h3>
            <p class="text-xs text-slate-500 uppercase tracking-widest">© 2026 Raqamli Tarix Platformasi</p>
        </div>
    </footer>

    <script>
        let currentAudio = null;
        const steps = [
            { t: "Yoshlik va Kamolot", d: "Amir Temur 1336-yilda tug'ilgan. Yoshligidan harbiy san'at, strategiya va ilmga qattiq qiziqqan. Uning xarakteri 'Kuch adolatdadir' shiori ostida shakllandi.", f: "U nafaqat sarkarda, balki Qur'onni yod bilgan hofiz ham edi." },
            { t: "Saltanat Tiklanishi", d: "1370-yilda u Movarounnahrni birlashtirdi. Samarqandni poytaxt qilib, dunyodagi eng go'zal shaharga aylantirishni maqsad qildi.", f: "Samarqandni Osiyo sayqali deb atashgan." },
            { t: "Buyuk Zafarlar", d: "Uning davlati Hindistondan Turkiyagacha yoyilgan edi. 35 yillik yurishlarida biror marta ham mag'lubiyatga uchramagan kamsonli g'oliblardan biridir.", f: "Anqara jangidagi g'alabasi butun Yevropa tarixini o'zgartirib yuborgan." }
        ];

        function changeStep(i) {
            document.querySelectorAll('.timeline-nav').forEach(b => b.classList.remove('active-tab'));
            document.getElementById('btn-' + i).classList.add('active-tab');
            document.getElementById('step-title').innerText = steps[i].t;
            document.getElementById('step-desc').innerText = steps[i].d;
            document.getElementById('step-fact').innerText = steps[i].f;
        }

        // Exponential backoff bilan fetch funksiyasi
        async function fetchWithRetry(url, options, retries = 5, delay = 1000) {
            for (let i = 0; i < retries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (response.ok) return await response.json();
                } catch (e) {
                    if (i === retries - 1) throw e;
                }
                await new Promise(res => setTimeout(res, delay));
                delay *= 2;
            }
        }

        // PCM -> WAV (TTS uchun)
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

        async function speakText(text, btn) {
            if (currentAudio) { currentAudio.pause(); currentAudio = null; }
            const originalContent = btn.innerHTML;
            btn.innerHTML = '<span class="loading-spinner"></span>';
            btn.disabled = true;

            try {
                const data = await fetchWithRetry(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: `Vazmin va ulug'vor ovozda o'zbekcha ayting: ${text.substring(0, 500)}` }] }],
                        generationConfig: {
                            responseModalities: ["AUDIO"],
                            speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: "Kore" } } }
                        },
                        model: "gemini-2.5-flash-preview-tts"
                    })
                });

                const b64Data = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData)?.inlineData?.data;
                if (!b64Data) throw new Error();

                const bin = atob(b64Data);
                const pcm = new Int16Array(bin.length / 2);
                for (let i = 0; i < bin.length; i += 2) pcm[i / 2] = (bin.charCodeAt(i + 1) << 8) | bin.charCodeAt(i);

                const blob = pcmToWav(pcm, 24000);
                currentAudio = new Audio(URL.createObjectURL(blob));
                
                currentAudio.onplay = () => {
                    btn.innerHTML = '<i class="fa-solid fa-volume-high animate-bounce"></i>';
                    btn.classList.add('is-speaking');
                };
                currentAudio.onended = () => {
                    btn.innerHTML = originalContent;
                    btn.disabled = false;
                    btn.classList.remove('is-speaking');
                    currentAudio = null;
                };
                currentAudio.play();
            } catch (e) {
                btn.innerHTML = '<i class="fa-solid fa-circle-exclamation"></i>';
                btn.disabled = false;
                setTimeout(() => { btn.innerHTML = originalContent; }, 2000);
            }
        }

        async function generateInsight(btn) {
            const box = document.getElementById('insight-box');
            const span = btn.querySelector('span');
            const icon = btn.querySelector('i');
            
            span.innerText = "Yozilmoqda...";
            icon.className = "fa-solid fa-spinner animate-spin";
            
            try {
                const data = await fetchWithRetry(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: "Amir Temur tuzuklaridan bitta juda qisqa va o'tkir hikmat yozing. Faqat hikmat matnini o'zini yuboring." }] }]
                    })
                });
                const res = data.candidates?.[0]?.content?.parts?.[0]?.text || "Adolat — najotdir.";
                box.classList.remove('hidden');
                box.innerHTML = `<i class="fa-solid fa-quote-left opacity-30 block mb-2"></i> ${res.trim()}`;
            } catch (e) {}
            
            span.innerText = "Yangi Hikmat";
            icon.className = "fa-solid fa-wand-magic-sparkles";
        }

        async function askAI() {
            const input = document.getElementById('user-input');
            const chatBox = document.getElementById('chat-box');
            const sendBtn = document.getElementById('send-btn');
            const userText = input.value.trim();

            if (!userText) return;

            chatBox.innerHTML += `<div class="flex justify-end w-full"><div class="p-4 rounded-2xl bg-white/10 text-white border border-white/5 max-w-[80%] text-right"><span class="text-[10px] opacity-50 block mb-1">Siz</span><p>${userText}</p></div></div>`;
            input.value = "";
            chatBox.scrollTop = chatBox.scrollHeight;

            sendBtn.disabled = true;
            sendBtn.innerHTML = '<span class="loading-spinner"></span>';

            try {
                const data = await fetchWithRetry(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: userText }] }],
                        systemInstruction: { parts: [{ text: "Siz Amir Temursiz. O'zbek tilida, vazmin va donishmand ohangda javob bering. Tuzuklarga tayaning." }] }
                    })
                });

                const response = data.candidates?.[0]?.content?.parts?.[0]?.text || "Biz bu borada tafakkur qilmoqdamiz.";
                const mid = 'msg-' + Date.now();
                chatBox.innerHTML += `
                    <div class="flex flex-col items-start max-w-[85%]">
                        <div class="p-6 rounded-2xl bot-msg text-xl text-white shadow-lg">
                            <span class="text-temurid-gold font-bold text-xs uppercase block mb-2">Amir Temur ✨</span>
                            <p id="${mid}" class="leading-relaxed italic">${response}</p>
                            <button onclick="speakText(document.getElementById('${mid}').innerText, this)" class="mt-4 text-temurid-gold text-sm flex items-center gap-2 hover:underline">
                                <i class="fa-solid fa-volume-high"></i> Ovozli eshitish
                            </button>
                        </div>
                    </div>`;
            } catch (e) {}

            sendBtn.disabled = false;
            sendBtn.innerHTML = 'Yuborish <i class="fa-solid fa-paper-plane"></i>';
            chatBox.scrollTop = chatBox.scrollHeight;
        }
    </script>
</body>
</html>
