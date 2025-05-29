<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kapsamlı Yapay Zeka Prompt Kılavuzu</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f9fafb; /* Açık gri arka plan */
        }
        .content-section {
            background-color: white;
            padding: 2rem;
            margin-bottom: 2rem;
            border-radius: 0.75rem; /* Daha yuvarlak köşeler */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        h1, h2, h3 {
            color: #1f2937; /* Koyu gri başlıklar */
        }
        h1 {
            font-size: 2.25rem; /* 36px */
            font-weight: 700;
            margin-bottom: 1.5rem;
            border-bottom: 2px solid #e5e7eb; /* Başlık altı çizgi */
            padding-bottom: 0.75rem;
        }
        h2 {
            font-size: 1.875rem; /* 30px */
            font-weight: 600;
            margin-top: 2rem;
            margin-bottom: 1rem;
            color: #2563eb; /* Mavi tema rengi */
        }
        h3 {
            font-size: 1.5rem; /* 24px */
            font-weight: 600;
            margin-top: 1.5rem;
            margin-bottom: 0.75rem;
            color: #1e40af; /* Koyu mavi */
        }
        p, li {
            color: #374151; /* Orta gri metin */
            line-height: 1.75;
            margin-bottom: 0.75rem;
        }
        ul {
            list-style-type: disc;
            padding-left: 1.5rem;
        }
        ol {
            list-style-type: decimal;
            padding-left: 1.5rem;
        }
        code, .gemini-output {
            background-color: #eef2ff; /* Açık mavi kod bloğu arka planı */
            color: #3730a3; /* Koyu mor kod metni */
            padding: 0.75rem 1rem; /* Increased padding */
            border-radius: 0.375rem;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.95em;
            display: block; 
            margin-bottom: 0.5rem;
            white-space: pre-wrap; 
            border: 1px solid #c7d2fe; /* Kod bloğu kenarlığı */
            line-height: 1.6;
        }
        .prompt-category > ul > li > code, .prompt-category > ol > li > code {
             margin-top: 0.5rem;
        }
        .prompt-tip { /* Eski kaynak-destegi yerine */
            background-color: #f0f9ff; /* Açık camgöbeği */
            padding: 0.75rem;
            border-radius: 0.375rem;
            margin-top: 0.25rem;
            margin-left: 1rem;
            font-size: 0.875rem; /* Daha küçük font */
            color: #075985; /* Koyu camgöbeği metin */
            border-left: 3px solid #0ea5e9; /* Sol kenarlık vurgusu */
        }
        .prompt-tip p {
            margin-bottom: 0.25rem;
        }
        #scrollToTopBtn {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #2563eb;
            color: white;
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            font-size: 24px;
            cursor: pointer;
            display: none; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            transition: opacity 0.3s, visibility 0.3s;
            z-index: 1000;
        }
        #scrollToTopBtn:hover {
            background-color: #1d4ed8;
        }
        .gemini-feature-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #d1d5db;
            border-radius: 0.375rem;
            margin-bottom: 0.75rem;
            box-shadow: inset 0 1px 2px rgba(0,0,0,0.05);
        }
        .gemini-feature-button {
            background-color: #2563eb;
            color: white;
            padding: 0.625rem 1.25rem; /* 10px 20px */
            border-radius: 0.375rem;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.2s;
            border: none;
        }
        .gemini-feature-button:hover {
            background-color: #1d4ed8;
        }
        .loading-indicator {
            display: none; /* Initially hidden */
            text-align: center;
            padding: 1rem;
            color: #1e40af;
        }
        .loading-spinner {
            border: 4px solid #f3f4f6; /* Light grey */
            border-top: 4px solid #3b82f6; /* Blue */
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 0 auto 0.5rem auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .error-message {
            color: #dc2626; /* Red for errors */
            background-color: #fee2e2;
            border: 1px solid #fecaca;
            padding: 0.75rem;
            border-radius: 0.375rem;
            margin-top: 0.5rem;
        }
    </style>
</head>
<body class="text-gray-800">
    <div class="container mx-auto p-4 md:p-8 max-w-4xl">
        <header class="text-center mb-8">
            <h1 class="text-4xl font-bold text-blue-700">Kapsamlı Yapay Zeka Prompt Kılavuzu</h1>
        </header>

        <section class="content-section">
            <p>Yapay zeka modelleri (Gemini, GPT serisi, Claude, Llama vb.) ile etkileşim kurmanın en önemli yolu etkili promptlar (komutlar veya yönlendirmeler) yazmaktır. Bu kılavuz, çeşitli yapay zeka modellerinden istediğiniz sonuçları almanıza yardımcı olacak temel ilkeleri, stratejileri ve kategorize edilmiş prompt örneklerini sunmaktadır.</p>
            <p>Amacımız, prompt mühendisliği becerilerinizi geliştirerek yapay zekanın gücünden en üst düzeyde yararlanmanızı sağlamaktır. Kılavuzdaki bilgiler ve araçlar, daha net, hedef odaklı ve yaratıcı promptlar oluşturmanıza olanak tanıyacaktır.</p>
        </section>

        <section class="content-section">
            <h2>✨ Gemini API Destekli Araçlar</h2>
            <p>Bu bölümde, yapay zeka promptlarınızı daha da geliştirmek ve yeni prompt fikirleri üretmek için Gemini API'nin gücünden yararlanan araçları bulabilirsiniz.</p>

            <div class="prompt-category mt-6">
                <h3>Prompt İyileştirici</h3>
                <p>Mevcut bir prompt fikriniz mi var? Aşağıya yazın ve Gemini'nin bu prompt'u nasıl daha etkili hale getirebileceğine dair öneriler alın. Genel iyi prompt yazma ilkelerine göre iyileştirmeler yapılacaktır.</p>
                <textarea id="draftPromptInput" class="gemini-feature-input" rows="3" placeholder="Örnek: 'Bana kediler hakkında bir şeyler yaz.'"></textarea>
                <button id="enhancePromptBtn" class="gemini-feature-button">Promptumu İyileştir ✨</button>
                <div id="enhancerLoading" class="loading-indicator">
                    <div class="loading-spinner"></div>
                    İyileştiriliyor...
                </div>
                <div id="enhancedPromptOutput" class="gemini-output mt-4" style="display: none;"></div>
                <div id="enhancerError" class="error-message" style="display: none;"></div>
            </div>

            <div class="prompt-category mt-8">
                <h3>Senaryo Tabanlı Prompt Üretici</h3>
                <p>Belirli bir göreviniz, projeniz veya elde etmek istediğiniz bir sonuç mu var? Senaryonuzu aşağıya açıklayın ve Gemini'nin bu duruma uygun, kılavuzdaki kategorilerden ilham alan prompt örnekleri sunmasını sağlayın.</p>
                <textarea id="scenarioInput" class="gemini-feature-input" rows="3" placeholder="Örnek: 'Yeni bir ürün için pazarlama sloganları bulmam gerekiyor.'"></textarea>
                <button id="suggestPromptsBtn" class="gemini-feature-button">Prompt Önerileri Al ✨</button>
                <div id="suggesterLoading" class="loading-indicator">
                    <div class="loading-spinner"></div>
                    Öneriler üretiliyor...
                </div>
                <div id="suggestedPromptsOutput" class="gemini-output mt-4" style="display: none;"></div>
                <div id="suggesterError" class="error-message" style="display: none;"></div>
            </div>
        </section>

        <section class="content-section">
            <h2>Temel Prompt Yazma İlkeleri (Tüm Modeller İçin Geçerli)</h2>
            <p>Yapay zeka modellerinden en iyi sonuçları almak için aşağıdaki temel ilkeleri göz önünde bulundurun:</p>
            <ol>
                <li><strong>Açık ve Net Olun:</strong> Ne istediğinizi spesifik ve anlaşılır bir dille ifade edin. Muğlaklıktan kaçının.</li>
                <li><strong>Bağlam Sağlayın:</strong> Modele, isteğinizi daha iyi anlaması için gerekli arka plan bilgilerini, konuyu veya durumu açıklayın.</li>
                <li><strong>Rol Atayın (Persona):</strong> Modelin belirli bir uzman, karakter veya tarzda yanıt vermesini isteyin. Örneğin, "Sen bir deneyimli bir şefsin..." veya "Dostça bir ton kullan..."</li>
                <li><strong>İstenen Çıktı Formatını Belirtin:</strong> Cevabın hangi formatta (liste, tablo, e-posta, kod bloğu, makale vb.) olması gerektiğini açıkça belirtin.</li>
                <li><strong>Adım Adım Düşünmesini İsteyin (Chain-of-Thought):</strong> Özellikle karmaşık veya çok aşamalı görevler için modelden çözüm yolunu adım adım düşünerek açıklamasını isteyin. "Adım adım düşünelim." gibi bir ifade kullanabilirsiniz.</li>
                <li><strong>Örnekler Verin (Few-Shot Prompting):</strong> İstediğiniz çıktıya benzer bir veya birkaç örnek sunarak modelin ne tür bir yanıt beklediğinizi daha iyi anlamasını sağlayın.</li>
                <li><strong>Kısıtlamalar ve Yönergeler Belirleyin:</strong> Yanıtın uzunluğu, tonu, içermesi veya içermemesi gerekenler gibi kısıtlamalar veya özel yönergeler ekleyin.</li>
                <li><strong>Iterasyon Yapın ve Geliştirin:</strong> İlk denemede mükemmel sonuç alamayabilirsiniz. Aldığınız yanıtlara göre promptunuzu düzenleyerek ve geliştirerek daha iyi sonuçlara ulaşın.</li>
                <li><strong>Modelin Yeteneklerini ve Sınırlarını Anlayın:</strong> Kullandığınız yapay zeka modelinin güçlü ve zayıf yönlerini, bilgi kesim tarihini ve genel yeteneklerini bilmek, daha gerçekçi beklentilere sahip olmanızı sağlar.</li>
                <li><strong>Pozitif ve Yapıcı İfadeler Kullanın:</strong> Genellikle "şunu yapma" yerine "şunu yap" gibi pozitif ve yönlendirici ifadeler daha iyi sonuçlar verir.</li>
                <li><strong>Karmaşıklığı Yönetin:</strong> Çok karmaşık bir isteği tek bir prompt'ta sormak yerine, görevi daha küçük, yönetilebilir parçalara bölerek birden fazla prompt kullanmayı düşünün.</li>
            </ol>
        </section>

        <section class="content-section">
            <h2>Kullanım Şekillerine Göre Kategorize Edilmiş Prompt Örnekleri</h2>
            <p>Aşağıdaki promptlar, kendi ihtiyaçlarınıza göre uyarlayabileceğiniz genel şablonlardır. <strong>[köşeli parantez]</strong> içindeki ifadeleri kendi bilgilerinizle değiştirin.</p>

            <div class="prompt-category">
                <h3>Kategori 1: Metin Üretimi ve Düzenleme</h3>
                <p>Bu kategori, çeşitli metin türleri oluşturmak, mevcut metinleri iyileştirmek veya dönüştürmek için kullanılır.</p>
                <ul>
                    <li><strong>Yaratıcı Yazarlık:</strong>
                        <ul>
                            <li><code>"Bana [fantastik bir dünya]da geçen, [cesur bir kahraman] ve [gizemli bir olay] hakkında kısa bir hikaye yaz. Hikaye [şaşırtıcı bir son] ile bitsin."</code></li>
                            <li><code>"[Doğanın güzellikleri] temalı, [serbest ölçü]de bir şiir kaleme al."</code></li>
                            <li><code>"İki eski dostun yıllar sonra bir kafede karşılaştığı duygusal bir sahne için diyalog yaz. Karakterler: [Karakter A], [Karakter B]."</code></li>
                        </ul>
                    </li>
                    <li><strong>İçerik Oluşturma:</strong>
                        <ul>
                            <li><code>"[Yapay zekanın eğitimdeki rolü] konulu, yaklaşık 500 kelimelik bilgilendirici bir blog yazısı taslağı oluştur. Giriş, gelişme ve sonuç bölümleri olsun."</code></li>
                            <li><code>"Yeni çıkan [mobil uygulamamızın adı] için dikkat çekici 3 farklı sosyal medya gönderi metni hazırla. Hedef kitle: [Hedef kitle tanımı]."</code></li>
                            <li><code>"Bir ürün tanıtım e-postası yaz. Ürün: [Ürün adı ve temel özelliği]. Amaç: [Okuyucuyu web sitesine yönlendirmek]."</code></li>
                        </ul>
                    </li>
                    <li><strong>Özetleme:</strong>
                        <ul>
                            <li><code>"Aşağıdaki uzun metni ana fikirlerini koruyarak 3 cümlelik bir özete indirge: [Uzun metni buraya yapıştırın]."</code></li>
                            <li><code>"Verdiğim [makalenin URL'si] adresindeki makalenin kilit noktalarını madde işaretleriyle özetle."</code></li>
                        </ul>
                    </li>
                    <li><strong>Yeniden Yazma / Basitleştirme:</strong>
                        <ul>
                            <li><code>"Bu karmaşık teknik paragrafı, [10 yaşındaki bir çocuğun anlayabileceği şekilde] yeniden yaz: [Karmaşık paragraf]."</code></li>
                            <li><code>"Aşağıdaki metni daha resmi bir üslupla yeniden ifade et: [Gayriresmi metin]."</code></li>
                        </ul>
                    </li>
                </ul>
            </div>

            <div class="prompt-category">
                <h3>Kategori 2: Bilgi Alma ve Soru Cevaplama</h3>
                <p>Belirli konularda bilgi edinmek, sorulara yanıt bulmak ve kavramları anlamak için kullanılır.</p>
                <ul>
                    <li><code>"[Fotosentez nedir] ve canlılar için neden önemlidir? Basit bir dille açıkla."</code></li>
                    <li><code>"[Fransız İhtilali'nin] başlıca nedenleri ve sonuçları nelerdir?"</code></li>
                    <li><code>"[Kuantum bilgisayarları] ile [klasik bilgisayarlar] arasındaki temel farkları karşılaştır."</code></li>
                    <li><code>"Bana [Antik Mısır medeniyeti] hakkında 5 ilginç bilgi ver."</code></li>
                </ul>
            </div>

            <div class="prompt-category">
                <h3>Kategori 3: Kod Üretimi ve Açıklama</h3>
                <p>Yazılım geliştirme süreçlerine yardımcı olmak, kod yazmak, hataları ayıklamak veya mevcut kodu anlamak için kullanılır.</p>
                <ul>
                    <li><strong>Kod Yazma:</strong>
                        <ul>
                            <li><code>"Python dilinde, bir listedeki sayıların ortalamasını bulan bir fonksiyon yaz."</code></li>
                            <li><code>"HTML ve CSS kullanarak, ortalanmış bir başlık ve altında bir paragraf içeren basit bir web sayfası oluştur."</code></li>
                            <li><code>"JavaScript ile bir butona tıklandığında 'Merhaba Dünya!' mesajı gösteren bir kod yaz."</code></li>
                        </ul>
                    </li>
                    <li><strong>Kod Açıklama:</strong>
                        <ul>
                            <li><code>"Aşağıdaki [Python kodu parçasını] adım adım ne yaptığını açıkla: [Kod parçası]."</code></li>
                            <li><code>"Bu [SQL sorgusunun] amacı nedir ve nasıl çalışır: [SQL Sorgusu]?"</code></li>
                        </ul>
                    </li>
                    <li><strong>Hata Ayıklama Yardımı:</strong>
                        <ul>
                            <li><code>"Aşağıdaki [Java kodumda] bir hata alıyorum: [Hata mesajı]. Sorun ne olabilir? Kod: [Hatalı kod]."</code></li>
                        </ul>
                    </li>
                </ul>
            </div>

            <div class="prompt-category">
                <h3>Kategori 4: Görüntü Oluşturma (Genel İlkeler)</h3>
                <p>Metinden görüntü üreten yapay zeka modelleri (örn: Imagen, DALL-E, Midjourney) için prompt yazarken dikkat edilmesi gerekenler:</p>
                <ul>
                    <li><strong>Detaylı Açıklamalar:</strong> <code>"Geniş açılı, gün batımında, mor ve turuncu tonların hakim olduğu bir gökyüzünün altında, sakin bir göl kenarında duran yalnız bir ağacın fotoğraf gerçekliğinde görüntüsü."</code></li>
                    <li><strong>Stil Belirtme:</strong> <code>"Bir kedinin [Van Gogh tarzında] yapılmış yağlı boya tablosu."</code> / <code>"Fütüristik bir şehrin [çizgi roman sanatı] stilinde illüstrasyonu."</code></li>
                    <li><strong>Kompozisyon ve Perspektif:</strong> <code>"[Yakın çekim], [alttan görünüm], [nesne] merkezde olacak şekilde..."</code></li>
                    <li><strong>Renk Paleti ve Atmosfer:</strong> <code>"Sıcak renklerin kullanıldığı, [huzurlu bir atmosferde] bir kütüphane iç mekanı."</code></li>
                    <li><strong>Negatif Promptlar (İstenmeyen Öğeler):</strong> Bazı modellerde, <code>"--no insanlar"</code> veya <code>"bulanık olmayan"</code> gibi ifadelerle istenmeyen unsurları dışarıda bırakabilirsiniz. (Modelin dokümantasyonuna bakın)</li>
                    <li><strong>Örnek Prompt (Gemini/Imagen için):</strong> <code>"Bir astronotun Jüpiter'in halkaları üzerinde süzüldüğü, arka planda parlayan yıldızların olduğu, sinematik ve epik bir dijital sanat eseri. Renkler canlı ve kontrast yüksek olmalı."</code></li>
                </ul>
            </div>
            <div class="prompt-category">
                <h3>Kategori 5: Çeviri ve Dil Araçları</h3>
                <p>Farklı diller arasında çeviri yapmak veya dilbilgisi konularında yardım almak için kullanılır.</p>
                <ul>
                    <li><code>"Aşağıdaki İngilizce metni Türkçeye çevir: '[İngilizce metin]'."</code></li>
                    <li><code>"Bu cümlenin Fransızcası nedir: '[Türkçe cümle]'?"</code></li>
                    <li><code>"Bu metindeki dilbilgisi hatalarını bul ve düzelt: '[Hatalı metin]'."</code></li>
                    <li><code>"'Empati' kelimesinin eş anlamlılarını listele."</code></li>
                </ul>
            </div>
             <div class="prompt-category">
                <h3>Kategori 6: Analiz ve Fikir Üretme</h3>
                <p>Verileri yorumlamak, trendleri belirlemek, yeni fikirler geliştirmek veya problem çözmek için kullanılır.</p>
                <ul>
                    <li><code>"Verdiğim müşteri geri bildirimlerini analiz et ve en sık belirtilen 3 şikayeti özetle: [Geri bildirimler]."</code></li>
                    <li><code>"Sürdürülebilir enerji kaynakları konusunda yenilikçi 5 proje fikri üret."</code></li>
                    <li><code>"Bir küçük işletmenin online görünürlüğünü artırmak için uygulanabilecek pazarlama stratejileri nelerdir? Bir liste halinde sun."</code></li>
                    <li><code>"Ekip motivasyonunu artırmak için 3 farklı yöntem öner."</code></li>
                </ul>
            </div>
            <div class="prompt-category">
                <h3>Kategori 7: Rol Yapma ve Simülasyon</h3>
                <p>Belirli bir karakteri canlandırmak veya bir durumu simüle etmek için kullanılır.</p>
                <ul>
                    <li><code>"Sen bir tarih profesörüsün. Bana [Rönesans dönemi sanatı] hakkında tutkulu bir şekilde bilgi ver."</code></li>
                    <li><code>"Bir iş görüşmesi simülasyonu yapalım. Sen işe alım uzmanısın, ben ise [yazılım geliştirici] pozisyonuna başvuran adayım. Bana sorular sor."</code></li>
                    <li><code>"Müşteri hizmetleri temsilcisi rolünü üstlen. Ürünümle ilgili bir sorun yaşayan kızgın bir müşteriye nasıl yanıt vereceğimi göster."</code></li>
                </ul>
            </div>
        </section>

        <section class="content-section">
            <h2>Farklı Modeller İçin İpuçları ve Gelişmiş Teknikler</h2>
            
            <h3>Gemini Modeline Özel İpuçları</h3>
            <ul>
                <li><strong>Çok Yönlülük:</strong> Gemini, metin, kod, ve API aracılığıyla görüntü gibi farklı türde içeriklerle çalışabilir. Promptlarınızda bu çeşitlilikten yararlanın.</li>
                <li><strong>Uzun Bağlam Yeteneği:</strong> Gemini'nin geniş bağlam penceresi, karmaşık ve çok adımlı konuşmaları veya uzun doküman analizlerini daha etkili bir şekilde yönetmenizi sağlar. Önceki konuşmaları referans alarak devam edin.</li>
                <li><strong>Açık Uçlu Keşif:</strong> Gemini'den yaratıcı fikirler, farklı bakış açıları veya karmaşık konuların derinlemesine analizini isteyebilirsiniz.</li>
                <li><strong>Örnek Gemini Promptu (Fikir Geliştirme):</strong> <code>"Küresel iklim değişikliğiyle mücadele için teknoloji, politika ve bireysel davranış değişikliği alanlarında 3 yenilikçi ve uygulanabilir çözüm önerisi geliştir. Her önerinin potansiyel etkilerini ve zorluklarını kısaca açıkla."</code></li>
            </ul>

            <h3>Diğer Popüler Modeller İçin Genel Notlar</h3>
            <ul>
                <li><strong>GPT Serisi (OpenAI):</strong> Genellikle güçlü metin üretimi, yaratıcı yazarlık ve kodlama yetenekleriyle bilinir. Karmaşık talimatları anlama ve tutarlı içerik üretme konusunda başarılıdır.</li>
                <li><strong>Claude Serisi (Anthropic):</strong> Özellikle uzun metinleri işleme, özetleme, soru-cevap ve güvenli içerik üretme konularında güçlüdür. Daha dikkatli ve düşünülmüş yanıtlar verme eğilimindedir.</li>
                <li><strong>Llama Serisi (Meta):</strong> Açık kaynak olmaları ve çeşitli boyutlarda sunulmalarıyla dikkat çekerler. Araştırmacılar ve geliştiriciler tarafından sıkça kullanılır ve farklı görevler için ince ayar yapılabilirler.</li>
                <li><strong>Model Dokümantasyonunu İnceleyin:</strong> Her modelin kendine özgü güçlü yanları, sınırlılıkları ve en iyi prompt yazma pratikleri olabilir. Kullandığınız modelin resmi dokümantasyonunu veya rehberlerini incelemek her zaman faydalıdır.</li>
            </ul>

            <h3>Gelişmiş Prompt Mühendisliği Teknikleri (Kavramsal)</h3>
            <ul>
                <li><strong>Chain-of-Thought (CoT) Prompting:</strong> Modelin bir problemi çözerken veya bir sonuca varırken düşünme sürecini adım adım açıklamasını istemek. Bu, özellikle mantık ve çıkarım gerektiren görevlerde doğruluğu artırabilir. (Örnek: "Bu matematik problemini çöz. Çözüm adımlarını detaylıca açıkla.")</li>
                <li><strong>Self-Consistency:</strong> Karmaşık bir soruya birden fazla farklı CoT yoluyla yanıt üretmesini isteyip, en tutarlı veya en sık tekrarlanan yanıtı seçmek.</li>
                <li><strong>Few-Shot / In-Context Learning:</strong> Prompt'un içine, istediğiniz göreve ve çıktı formatına dair birkaç örnek (girdi-çıktı çifti) eklemek. Model bu örneklerden öğrenerek benzer bir görevi daha iyi yerine getirir.</li>
                <li><strong>Retrieval Augmented Generation (RAG):</strong> Modelin kendi iç bilgisine ek olarak, harici bir bilgi kaynağından (örneğin bir veritabanı veya doküman seti) ilgili bilgileri alıp yanıtını bu bilgilere dayandırmasını sağlamak. (Bu genellikle bir sistem mimarisi gerektirir.)</li>
                <li><strong>Prompt Chaining / Decomposition:</strong> Karmaşık bir görevi daha küçük, yönetilebilir alt görevlere bölmek ve her alt görev için ayrı promptlar kullanarak sonuçları birleştirmek.</li>
            </ul>
        </section>

        <footer class="text-center mt-12 py-6 border-t border-gray-300">
            <p class="text-sm text-gray-500">&copy; <span id="currentYear"></span> Kapsamlı Yapay Zeka Prompt Kılavuzu. Tüm hakları saklıdır.</p>
        </footer>

    </div>

    <button id="scrollToTopBtn" title="Yukarı çık">
        &uarr;
    </button>

    <script>
        // Get current year for footer
        document.getElementById('currentYear').textContent = new Date().getFullYear();

        // Scroll to top button functionality
        const scrollToTopBtn = document.getElementById('scrollToTopBtn');
        
        window.onscroll = function() {
            if (document.body.scrollTop > 100 || document.documentElement.scrollTop > 100) {
                scrollToTopBtn.style.display = "block";
            } else {
                scrollToTopBtn.style.display = "none";
            }
        };

        scrollToTopBtn.onclick = function() {
            window.scrollTo({top: 0, behavior: 'smooth'});
        };

        // Gemini API Integration
        const enhancePromptBtn = document.getElementById('enhancePromptBtn');
        const draftPromptInput = document.getElementById('draftPromptInput');
        const enhancedPromptOutput = document.getElementById('enhancedPromptOutput');
        const enhancerLoading = document.getElementById('enhancerLoading');
        const enhancerError = document.getElementById('enhancerError');

        const suggestPromptsBtn = document.getElementById('suggestPromptsBtn');
        const scenarioInput = document.getElementById('scenarioInput');
        const suggestedPromptsOutput = document.getElementById('suggestedPromptsOutput');
        const suggesterLoading = document.getElementById('suggesterLoading');
        const suggesterError = document.getElementById('suggesterError');
        
        const apiKey = ""; // API anahtarı boş bırakılacak, Canvas ortamı sağlayacak.

        async function callGemini(promptText, loadingElement, outputElement, errorElement) {
            loadingElement.style.display = 'block';
            outputElement.style.display = 'none';
            errorElement.style.display = 'none';
            outputElement.textContent = ''; // Clear previous output
            errorElement.textContent = ''; // Clear previous error

            try {
                let chatHistory = [{ role: "user", parts: [{ text: promptText }] }];
                const payload = { contents: chatHistory };
                // Model adını güncelledim, en son flash modelini kullanmak daha iyi olabilir.
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
                
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    const errorData = await response.json();
                    console.error('API Error Data:', errorData); // Hata detayını konsola yazdır
                    throw new Error(errorData.error ? errorData.error.message : `API isteği başarısız oldu, durum: ${response.status}`);
                }

                const result = await response.json();

                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const text = result.candidates[0].content.parts[0].text;
                    outputElement.textContent = text;
                    outputElement.style.display = 'block';
                } else {
                    console.error('Unexpected response structure:', result);
                    // Kullanıcıya daha anlaşılır bir mesaj gösterilebilir
                    let errorMessageText = 'Yanıtta beklenen içerik bulunamadı.';
                    if (result.promptFeedback && result.promptFeedback.blockReason) {
                        errorMessageText += ` Engelleme nedeni: ${result.promptFeedback.blockReason}`;
                         if (result.promptFeedback.safetyRatings) {
                            errorMessageText += ` Güvenlik değerlendirmeleri: ${JSON.stringify(result.promptFeedback.safetyRatings)}`;
                        }
                    }
                    throw new Error(errorMessageText);
                }
            } catch (err) {
                console.error("Gemini API call failed:", err);
                errorElement.textContent = `Bir hata oluştu: ${err.message}. Lütfen API anahtarınızın doğru yapılandırıldığından ve model adının geçerli olduğundan emin olun. Konsolu kontrol edin.`;
                errorElement.style.display = 'block';
            } finally {
                loadingElement.style.display = 'none';
            }
        }

        enhancePromptBtn.addEventListener('click', () => {
            const userDraftPrompt = draftPromptInput.value.trim();
            if (!userDraftPrompt) {
                enhancerError.textContent = 'Lütfen iyileştirmek için bir prompt girin.';
                enhancerError.style.display = 'block';
                return;
            }

            const metaPromptForEnhancer = `Sen, Gemini başta olmak üzere çeşitli yapay zeka modelleri (metin üretimi, kod üretimi, görüntü oluşturma vb. yapabilen) için etkili promptlar oluşturma konusunda bir uzmansın. Bir kullanıcı bir prompt taslağı sunacak. Görevin, bu promptu daha açık, daha spesifik hale getirmek ve yapay zeka modelinden iyi bir yanıt alma olasılığını artırmak için geliştirmektir. Bunu yaparken, genel iyi prompt yazma ilkelerini (netlik, bağlam sağlama, istenen çıktıyı belirtme, rol atama, adım adım düşünme isteme gibi) göz önünde bulundur. Geliştirilmiş promptu doğrudan sun.

Kullanıcının prompt taslağı: "${userDraftPrompt}"`;
            
            callGemini(metaPromptForEnhancer, enhancerLoading, enhancedPromptOutput, enhancerError);
        });

        suggestPromptsBtn.addEventListener('click', () => {
            const userScenario = scenarioInput.value.trim();
            if (!userScenario) {
                suggesterError.textContent = 'Lütfen prompt önerileri için bir senaryo veya görev açıklaması girin.';
                suggesterError.style.display = 'block';
                return;
            }
            
            const metaPromptForSuggester = `Sen, kullanıcıların Gemini ve diğer yapay zeka modelleri için etkili promptlar bulmalarına veya oluşturmalarına yardımcı olan bir yapay zeka asistanısın. Kullanıcı bir senaryo, görev veya elde etmek istediği sonuç türünü açıklayacak. Buna dayanarak, görevin 2-3 örnek prompt önermektir. Bu promptlar, genel prompt mühendisliği tekniklerinden ve farklı yapay zeka yeteneklerinden (örn: metin özetleme, yaratıcı içerik yazma, kod parçacığı oluşturma, bir resmi tarif etme, çeviri yapma, fikir üretme) ilham almalıdır. Promptlar pratik, açık olmalı ve kullanıcının yapay zeka modelinden ne istediğini net bir şekilde belirtmelidir. Her önerilen promptu yeni bir satırda, başına '-' işareti koyarak ve sonunda bir boşluk bırakarak sun.

Kullanıcının senaryo/görev açıklaması: "${userScenario}"`;

            callGemini(metaPromptForSuggester, suggesterLoading, suggestedPromptsOutput, suggesterError);
        });

    </script>
</body>
</html>
