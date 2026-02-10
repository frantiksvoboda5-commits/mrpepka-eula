<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="utf-8" />
  <title>Pravidla — MrPepka Events</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="color-scheme" content="dark">
  <style>
    :root{
      --bg-1: #070707;
      --bg-2: #111111;
      --card: linear-gradient(135deg,#151515,#252525);
      --accent: #ff4250;
      --accent-2: #ff9b2e;
      --muted: #bfbfbf;
      --glass: rgba(255,255,255,0.03);
      --ok: #65d17a;
      --danger: #ff6b6b;
      --radius: 16px;
      --pad: 28px;
      --maxw: 1200px;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", "Courier New", monospace;
      --ui-font: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      padding:44px;
      font-family:var(--ui-font);
      color:#eaeaea;
      background: radial-gradient(1200px 600px at 10% 10%, rgba(255,66,80,0.04), transparent),
                  linear-gradient(180deg,var(--bg-1),var(--bg-2));
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      display:flex;
      justify-content:center;
    }

    .wrap{
      width:100%;
      max-width:var(--maxw);
    }

    header{
      text-align:center;
      margin-bottom:28px;
    }

    .logo{
      display:inline-flex;
      align-items:center;
      gap:12px;
      justify-content:center;
      margin-bottom:8px;
    }

    .badge{
      background:linear-gradient(90deg,var(--accent),var(--accent-2));
      color:white;
      padding:8px 12px;
      border-radius:999px;
      font-weight:800;
      box-shadow:0 6px 30px rgba(255,66,80,0.12);
    }

    h1{
      margin:6px 0 4px;
      font-size:2.6rem;
      color:var(--accent);
      letter-spacing:0.6px;
      text-shadow: 0 10px 40px rgba(255,66,80,0.12);
    }

    .subtitle{
      color:var(--accent-2);
      font-weight:700;
      margin-bottom:6px;
    }

    .kicker{
      color:var(--muted);
      font-size:0.95rem;
      margin-bottom:22px;
    }

    /* layout: big grid with distributed boxes */
    .grid{
      display:grid;
      grid-template-columns: 1fr 360px;
      gap:22px;
      align-items:start;
    }

    @media (max-width:980px){
      .grid{grid-template-columns:1fr; padding:0 8px}
    }

    /* main column */
    .main{
      display:flex;
      flex-direction:column;
      gap:20px;
    }

    .side{
      position:relative;
      display:flex;
      flex-direction:column;
      gap:20px;
    }

    /* card */
    .card{
      background:var(--card);
      border-radius:var(--radius);
      padding:var(--pad);
      border:1px solid rgba(255,255,255,0.03);
      box-shadow: 0 14px 50px rgba(0,0,0,0.7);
      overflow:hidden;
      transition:transform .22s ease, box-shadow .22s ease;
    }

    .card:hover{ transform:translateY(-6px); box-shadow:0 30px 90px rgba(255,66,80,0.08) }

    h2{
      margin:0 0 10px 0;
      font-size:1.2rem;
      color:var(--accent-2);
      display:flex;
      gap:12px;
      align-items:center;
    }

    .lead{
      color:#f5f5f5;
      font-weight:700;
      margin-bottom:12px;
    }

    p{ margin:0 0 12px 0; line-height:1.7; color:#e6e6e6 }
    ul{ margin:0 0 12px 20px; padding:0; line-height:1.7 }
    li{ margin-bottom:10px }

    .chip{
      display:inline-block;
      padding:6px 10px;
      border-radius:999px;
      background:linear-gradient(90deg, rgba(255,66,80,0.08), rgba(255,155,46,0.04));
      color:var(--accent);
      font-weight:700;
      border:1px solid rgba(255,66,80,0.04);
      margin-right:8px;
    }

    /* visual separators */
    .divider{ height:2px; background:linear-gradient(90deg, transparent, rgba(255,155,46,0.16), transparent); margin:18px 0; border-radius:6px }

    /* long scroll blocks */
    .long{
      max-height:520px;
      overflow:auto;
      padding-right:6px;
    }
    .long::-webkit-scrollbar{ width:9px }
    .long::-webkit-scrollbar-thumb{ background:rgba(255,66,80,0.25); border-radius:8px }

    /* highlight / important */
    .important{
      display:inline-block;
      background:rgba(255,66,80,0.12);
      color:#ffd6d6;
      padding:8px 12px;
      border-radius:10px;
      font-weight:800;
      margin-bottom:10px;
    }

    .callout{
      border-radius:12px;
      padding:12px 14px;
      background:linear-gradient(90deg, rgba(255,155,46,0.03), rgba(255,66,80,0.02));
      border:1px solid rgba(255,155,46,0.04);
      color:var(--muted);
      margin:10px 0;
    }

    /* list bullets with icons */
    .bullet{ display:flex; gap:12px; align-items:flex-start; margin-bottom:10px }
    .bullet .ico{ width:34px; height:34px; border-radius:10px; display:inline-grid; place-items:center; color:white; font-weight:800; box-shadow:0 6px 24px rgba(0,0,0,0.6) }
    .ico.good{ background:linear-gradient(90deg,var(--ok), #46c16a) }
    .ico.warn{ background:linear-gradient(90deg,var(--accent), var(--accent-2)) }
    .ico.info{ background:linear-gradient(90deg,#5ab7ff,#7ad0ff) }
    .ico.danger{ background:linear-gradient(90deg,var(--danger), #ff8b8b) }

    /* side widgets */
    .side .mini{ padding:14px; background:linear-gradient(135deg,#141414,#1b1b1b); border-radius:12px; border:1px solid rgba(255,255,255,0.02) }
    .side .mini a{ color:var(--accent-2); font-weight:800; text-decoration:none }
    .small-meta{ color:var(--muted); font-size:0.95rem; margin-top:8px }

    footer{ margin-top:28px; text-align:center; color:var(--muted); font-size:0.95rem }

    /* subtle heading icon */
    .hicon{ font-size:20px; display:inline-block; width:26px; text-align:center }

    /* fancy accept box for future (visual only) */
    .accept{
      display:flex;
      gap:12px;
      align-items:center;
      margin-top:12px;
    }
    .btn{
      background:linear-gradient(90deg,var(--accent),var(--accent-2));
      color:white;
      padding:10px 14px;
      border-radius:10px;
      font-weight:800;
      border:none;
      cursor:pointer;
      box-shadow:0 10px 30px rgba(255,66,80,0.12);
      text-decoration:none;
    }
    .btn.ghost{
      background:transparent;
      border:1px solid rgba(255,255,255,0.04);
      color:var(--muted);
      font-weight:700;
    }

    /* responsive tweaks */
    @media (max-width:520px){
      .badge{padding:6px 10px}
      .hicon{font-size:18px}
      .chip{padding:5px 8px}
    }
  </style>
</head>
<body>
  <div class="wrap">

    <header>
      <div class="logo">
        <div class="badge">MrPepka Events</div>
      </div>
      <h1>📜 Oficiální pravidla a podmínky</h1>
      <div class="subtitle">Tvrdě, jasně, viditelně — vytvořil: <strong>lukyczxd</strong></div>
      <div class="kicker">Připojením souhlasíš se všemi podmínkami níže. Dobré věci jsou nahoře, tvrdá realita dole — čti obě části.</div>
    </header>

    <div class="grid">
      <!-- MAIN COLUMN -->
      <div class="main">

        <!-- Welcome / Quick summary -->
        <section class="card">
          <h2><span class="hicon">👋</span> Vítej na MrPepka Events</h2>
          <div class="lead">Krátké shrnutí — rychle a jasně</div>
          <div class="long">
            <p>MrPepka Events jsou eventové servery zaměřené na soutěže, speciální herní mechaniky a komunitní akce. Na tomto serveru probíhají eventy s aktivní správou — administrace zasahuje, mění a spravuje dění v reálném čase tak, aby eventy byly dynamické a nezapomenutelné.</p>

            <div class="callout">
              <strong>Krátce:</strong> chceme akci, adrenalin a zábavu.
            </div>

            <div style="display:flex; gap:10px; flex-wrap:wrap; margin-top:10px">
              <span class="chip">🎮 Eventy</span>
              <span class="chip">⚙️ Admin zásahy</span>
              <span class="chip">🔐 Data & bezpečnost</span>
              <span class="chip">📣 Support: Discord</span>
            </div>
          </div>
        </section>

        <!-- Benefits expanded -->
        <section class="card">
          <h2><span class="hicon">🏆</span> Co získáš</h2>
          <div class="lead"></div>
          <div class="long">
            <p>Na MrPepka Events nejsou eventy jen jednorázovky — máme plánovaný obsah, série turnajů a speciální akce. Níže popisujeme hlavní benefitové oblasti, abys věděl, do čeho jdeš.</p>

            <div class="bullet"><div class="ico good">✨</div><div><strong>Pravidelné eventy:</strong> týdenní i měsíční soutěže, tematické dny, build-challenge, PvP tourney a speciální sezónní eventy. Každý event má vlastní pravidla a vlastní systém odměn.</div></div>

            <div class="bullet"><div class="ico good">🎁</div><div><strong>Odměny:</strong> kosmetika, unikátní role na Discordu, interní valuta/nebo body do speciálních obchodů, šance na VIP přístup k exkluzivním eventům. Odměny nejsou garantované — jsou nástrojem motivace a ocenění.</div></div>

            <div class="bullet"><div class="ico good">🤝</div><div><strong>Komunita a networking:</strong> konkurenceschopná, ale aktivní komunita. Možnost potkat hráče se zkušenostmi, najít parťáky do týmů a zapojit se do organizace eventů.</div></div>

            <div style="margin-top:12px">
              <p>Tento blok je nahoře záměrně: pokud jdeš do rizika (viz sekce níže), alespoň víš, co za to můžeš získat.</p>
            </div>
          </div>
        </section>

        <!-- How events run -->
        <section class="card">
          <h2><span class="hicon">🎪</span> Jak probíhají eventy</h2>
          <div class="lead"></div>
          <div class="long">
            <p>Eventy řídí administrace: zveřejnění pravidel, start, monitoring průběhu, vyhodnocení výsledků a případné následné zásahy. Admini mohou pravidla doplnit, upravit nebo event přerušit v případě technického problému či podezřelého chování.</p>

            <ul>
              <li>Event může mít registraci — někdy jsou sloty limitovány.</li>
              <li>Administrace zveřejní primární pravidla; doplňující pravidla mohou být upravena během akce.</li>
              <li>Výsledky a odměny jsou předmětem rozhodnutí adminů.</li>
            </ul>

            <p>Pokud se účastníš, bereš na vědomí, že průběh nemusí být statický — je to součást provozního modelu MrPepka Events.</p>
          </div>
        </section>

        <!-- Admin powers (very explicit) -->
        <section class="card">
          <h2><span class="hicon">⚠️</span> Pravomoci administrace — detailně</h2>
          <div class="lead">Administrace může jednat rychle a bez předchozího souhlasu</div>
          <div class="long">
            <p>Připojením na server bereš na vědomí, že administrace zásahuje do hry z libovolného důvodu nebo bez uvedení veřejného důvodu. To zahrnuje, ale není omezeno na:</p>

            <div class="bullet"><div class="ico warn">🔧</div><div><strong>Kick / Mute / Ban / Crash:</strong> administrace může okamžitě udělit kick, mute nebo ban (dočasný i trvalý) anebo provést bezpečné ukončení relace (tzv. crash) hráče. Zásah může být proveden s veřejným odůvodněním nebo bez něj.</div></div>

            <div class="bullet"><div class="ico warn">📦</div><div><strong>Úprava herního stavu:</strong> úprava inventáře, změna pozice, odpočítání/provádění resetů progresu nebo statistik.</div></div>

            <div class="bullet"><div class="ico warn">🛡️</div><div><strong>Pluginové zásahy:</strong> administrátoři mohou spouštět pluginy určené k testování, monitoringu, omezení nebo odpojení klienta.</div></div>

            <p style="margin-top:10px">Administrace se snaží postupovat rozumně. Nicméně přijetím těchto pravidel přijímáš i možnost, že administrace zasáhne i bez veřejného vysvětlení. Pokud s tím nesouhlasíš — nehraješ na serveru.</p>

            <div class="callout">V případě omylu nebo pokud si myslíš, že došlo k chybě, <strong>vytvoř ticket</strong> na Discordu: <a href="https://discord.gg/ZRjNTBqEDN" target="_blank" rel="noopener noreferrer" style="color:var(--accent-2); font-weight:800">discord.gg/ZRjNTBqEDN</a>. Ke každému ticketu přistupujeme individuálně.</div>

            <p class="small-meta">Poznámka: Ticket není zárukou zrušení sankce — je to nástroj pro komunikaci a možnou korekci.</p>
          </div>
        </section>

        <!-- Data & privacy -->
        <section class="card">
          <h2><span class="hicon">🔐</span> Ochrana a zpracování údajů</h2>
          <div class="lead">Co sbíráme a proč</div>
          <div class="long">
            <p>Pro bezpečný a stabilní provoz serveru je nezbytné zpracovávat určité technické údaje. Tyto údaje slouží pro prevenci zneužití, vyšetřování incidentů a zlepšení stability.</p>

            <ul>
              <li>🌐 IP adresa, čas připojení, herní nickname a UUID</li>
              <li>📊 Telemetrie spojení (základní informace o ping, ztrátě paketů apod.)</li>
              <li>🔒 Hesla jsou u nás šifrovaná / hashovaná — administrace k nim nemá přístup v čitelné podobě</li>
            </ul>

            <p>Data nejsou prodávána. Sdílíme je pouze s oprávněnými osobami nebo službami nezbytnými k provozu a ochraně serveru.</p>
          </div>
        </section>

        <!-- Rules & punishments very long -->
        <section class="card">
          <h2><span class="hicon">📜</span> Chování, sankce & procesy (velmi rozvedené)</h2>
          <div class="lead"></div>
          <div class="long">
            <p>Chování: na serveru se očekává základní slušnost. Záměrné poškozování zážitku ostatních (griefing, trolling, doxxing, opakované obtěžování) bude postihováno.</p>

            <p>Proces: menší incidenty řeší administrace operativně. U větších incidentů admini mohou požadovat logy nebo záznamy (replay), ale nejsou povinni detailně vysvětlovat každé rozhodnutí.</p>

            <h3 style="margin-top:12px; color:#ffd0c9">Možné sankce</h3>
            <ul>
              <li>📣 Varování</li>
              <li>⏳ Dočasný ban (hodiny / dny)</li>
              <li>⛔ Trvalý ban nebo chrash clienta (i bezdůvodně)</li>
              <li>📦 Reset inventáře / ztráta odměn</li>
              <li>🛠️ Technické zásahy (omezení, odpojení klienta)</li>
            </ul>

            <h4 style="margin-top:12px">Příklady z praxe</h4>
            <div class="bullet"><div class="ico info">A</div><div><strong>Příklad A:</strong> Hráč opakovaně griefuje — postup: varování → dočasný ban → při opakovaném porušení trvalý ban.</div></div>
            <div class="bullet"><div class="ico info">B</div><div><strong>Příklad B:</strong> Spor v eventu — admin přezkoumá logy a rozhodne; rozhodnutí je konečné.</div></div>
            <div class="bullet"><div class="ico info">C</div><div><strong>Příklad C:</strong> Exploit/cheat — reset inventáře, zákaz účasti v eventu a další sankce dle situace.</div></div>

            <p>Odvolání: lze podat přes Discord ticket. Každý případ posuzujeme individuálně, ale odvolání není automatická garance zrušení sankce.</p>

          </div>
        </section>

        <!-- Final hard block: responsibility -->
        <section class="card crash">
          <h2><span class="hicon">🚨</span> Pády, ztráty & nulová odpovědnost — konec (čti) </h2>
          <div class="lead important">Vše níže je tvá odpovědnost. Tohle je poslední a nejsilnější varování.</div>
          <div class="long" style="max-height:760px; padding-right:10px">
            <p><strong>Stručně:</strong> Připojením na MrPepka Events přijímáš, že administrace, majitel nebo provozovatel serveru nenesou žádnou odpovědnost za škody, ztráty nebo následky vzniklé během hraní či eventů.</p>

            <h4 style="color:#ffd6d6">Co to znamená (konkrétně)</h4>
            <ol>
              <li>💥 Pád klienta (crash) či nečekané ukončení hry — ztráta relace, neuložené změny.</li>
              <li>🎞️ Ztráta replayů, nahrávek nebo jiných záznamů pořízených během eventu.</li>
              <li>🧾 Ztráta inventáře, XP, progressu v důsledku zásahu nebo chyby.</li>
              <li>⚠️ Výkonové problémy (lag, FPS dropy, výpadky) — vše na vlastní riziko.</li>
              <li>🔌 Administrativní odpojení / bezpečný crash provedený ze strany adminů.</li>
              <li>🛑 Žádné finanční ani jiné náhrady za způsobené škody.</li>
            </ol>

            <p style="margin-top:10px">Pokud je pro tebe zásadní úplná garance ochrany progresu nebo dat, nedoporučujeme se účastnit našich eventů.</p>

            <div class="callout" style="margin-top:14px">
              <strong>Postup při omylu:</strong> vytvoř ticket na Discordu a popiš situaci. Link: <a href="https://discord.gg/ZRjNTBqEDN" target="_blank" rel="noopener noreferrer" style="color:var(--accent-2); font-weight:800">discord.gg/ZRjNTBqEDN</a>. V ticketu uveď co nejvíce důkazů (screenshots, timecode, popis incidentu).
            </div>

            <p style="margin-top:14px; color:#ffd0d0"><strong>Varování:</strong> tato sekce není pokynem k úmyslnému poškozování hráčů. Jde o právní a provozní ujednání — administrace se snaží být fér, ale provoz serveru má prioritu.</p>

            <p style="font-weight:800; margin-top:18px">Dobré věci jsou nahoře. Tvrdá realita je dole. Čti obě.</p>
          </div>
        </section>

      </div> <!-- /main -->

      <!-- SIDE COLUMN -->
      <aside class="side">

        <!-- Quick rules summary -->
        <div class="card side-mini mini">
          <h2><span class="hicon">⚡</span> Rychlá shrnutí</h2>
          <div style="font-weight:700; margin-bottom:8px">Nejdůležitější body</div>
          <div class="small-meta">
            <ul style="margin:6px 0 0 18px">
              <li>Administrátoři mohou zasáhnout kdykoli, i bez důvodu</li>
              <li>Žádná náhrada za ztráty</li>
              <li>Pro testy a eventy mohou admini použít pluginy a nástroje</li>
              <li>Omyl? Vytvoř ticket na Discordu</li>
            </ul>
          </div>
        </div>

        <!-- Discord / Support -->
        <div class="card side-mini mini">
          <h2><span class="hicon">📣</span> Support & kontakt</h2>
          <div class="lead">Potřebuješ pomoct? Nahlásit chybu?</div>
          <div>
            <p>Nejrychlejší cesta k řešení je náš Discord — založ ticket a popiš incident detailně.</p>
            <div style="display:flex; gap:10px; align-items:center; margin-top:8px">
              <a class="btn" href="https://discord.gg/ZRjNTBqEDN" target="_blank" rel="noopener noreferrer">➡️ Otevřít Discord / Ticket</a>
              <a class="btn ghost" href="#" onclick="alert('Použij Discord link pro ticket');return false">Jak podat ticket?</a>
            </div>
            <div class="small-meta" style="margin-top:10px">Uveď nick, čas incidentu a co se stalo — ušetří to čas oběma stranám.</div>
          </div>
        </div>

        <!-- Mini FAQ -->
        <div class="card side-mini mini">
          <h2><span class="hicon">❓</span> Často kladené otázky</h2>
          <div class="long" style="max-height:220px">
            <p><strong>Q:</strong> Můžou admini opravdu crashnout klient? <br><strong>A:</strong> Ano — administrace může provést bezpečné odpojení nebo zásah.</p>
            <p><strong>Q:</strong> Co když mám důkazy? <br><strong>A:</strong> Otevři ticket na Discordu, přilož důkazy (screenshoty, replay).</p>
            <p><strong>Q:</strong> Dávají se náhrady? <br><strong>A:</strong> Ne, pravidla explicitně uvádějí, že neneseme odpovědnost.</p>
          </div>
        </div>

      </aside>
    </div> <!-- /grid -->

    <footer>
      <div>Poslední aktualizace: 2026 • MrPepka Events • Vytvořil: <strong>lukyczxd</strong></div>
      <div style="margin-top:6px">© MrPepka Events 2026</div>
    </footer>

  </div> <!-- /wrap -->
</body>
</html>
