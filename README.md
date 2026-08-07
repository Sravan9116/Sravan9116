# Sravan — AI OS Portfolio — Build Log

This is a **progress snapshot**, not the final deliverable. It packages
everything generated so far into one file so you can review or copy it.

**Status:**
- [x] Design system + full stylesheet (`styles.css` below)
- [x] Section markup for all 9 sections + hero + nav + footer (`body.html` below)
- [ ] `main.js` — cursor, Three.js particles, typing effect, scroll reveals,
      data-driven Skills/Projects/Research/Leadership/Journey content, drone
      animation, GitHub stats wiring, AI-core companion
- [ ] Final assembly into one working, self-contained `index.html` (with your
      two photos embedded) — this is what actually opens in a browser

I'm continuing straight on to the remaining pieces after this — the working
site will follow in this same reply.

---

## `styles.css`

```css
/* ==========================================================================
   SRAVAN — AI OS PORTFOLIO
   Design tokens: void #05050d / panel #0d0e22 / blue #00d4ff / violet #a855f7
   / cyan #2de2c6 / paper #f3f5ff — display: Space Grotesk, body: Inter,
   utility/data: JetBrains Mono
   ========================================================================== */

:root{
  --c-void:#05050d;
  --c-void-2:#090a17;
  --c-panel:#0d0e22;
  --c-panel-2:#13152e;
  --c-blue:#00d4ff;
  --c-blue-dim:#0891b2;
  --c-violet:#a855f7;
  --c-violet-dim:#7c3aed;
  --c-cyan:#2de2c6;
  --c-paper:#f3f5ff;
  --c-mist:#9aa3c7;
  --c-mist-dim:#5c6389;

  --glass-bg:rgba(255,255,255,.045);
  --glass-bg-hi:rgba(255,255,255,.08);
  --glass-brd:rgba(255,255,255,.10);
  --glass-brd-hi:rgba(255,255,255,.24);

  --grad-signal:linear-gradient(135deg,var(--c-blue),var(--c-violet));
  --grad-signal-2:linear-gradient(135deg,var(--c-cyan),var(--c-blue));

  --glow-blue:0 0 1px rgba(0,212,255,.9),0 0 30px rgba(0,212,255,.35);
  --glow-violet:0 0 1px rgba(168,85,247,.9),0 0 30px rgba(168,85,247,.35);
  --glow-cyan:0 0 1px rgba(45,226,198,.9),0 0 30px rgba(45,226,198,.3);

  --font-display:'Space Grotesk',sans-serif;
  --font-body:'Inter',sans-serif;
  --font-mono:'JetBrains Mono',monospace;

  --ease-out:cubic-bezier(.16,.84,.44,1);
  --ease-soft:cubic-bezier(.22,.61,.36,1);

  --container:1240px;
  --radius-sm:10px;
  --radius-md:18px;
  --radius-lg:28px;
  --radius-full:999px;

  --nav-h:76px;
}

*,*::before,*::after{box-sizing:border-box;}
html{scroll-behavior:smooth;background:var(--c-void);}
body{
  margin:0;
  background:var(--c-void);
  color:var(--c-paper);
  font-family:var(--font-body);
  font-size:16px;
  line-height:1.6;
  -webkit-font-smoothing:antialiased;
  overflow-x:hidden;
  cursor:none;
}
@media (hover:none),(pointer:coarse){ body{ cursor:auto; } }

img{max-width:100%;display:block;}
a{color:inherit;text-decoration:none;}
ul{margin:0;padding:0;list-style:none;}
h1,h2,h3,h4,p{margin:0;}
button{font:inherit;color:inherit;background:none;border:none;cursor:none;}
@media (hover:none),(pointer:coarse){ button{cursor:pointer;} }
svg{display:block;}

::selection{background:var(--c-violet);color:#fff;}

.container{
  width:100%;
  max-width:var(--container);
  margin:0 auto;
  padding:0 32px;
}
section{position:relative;padding:160px 0;}
@media (max-width:768px){ section{padding:110px 0;} }

.eyebrow{
  display:inline-flex;
  align-items:center;
  gap:10px;
  font-family:var(--font-mono);
  font-size:.78rem;
  letter-spacing:.14em;
  text-transform:uppercase;
  color:var(--c-cyan);
  margin-bottom:22px;
}
.eyebrow::before{
  content:'';
  width:7px;height:7px;border-radius:50%;
  background:var(--c-cyan);
  box-shadow:0 0 10px var(--c-cyan),0 0 20px var(--c-cyan);
  animation:pulseDot 2.2s ease-in-out infinite;
}
@keyframes pulseDot{0%,100%{opacity:1;transform:scale(1);}50%{opacity:.4;transform:scale(.7);}}

.section-title{
  font-family:var(--font-display);
  font-weight:700;
  font-size:clamp(2.1rem,4.6vw,3.6rem);
  letter-spacing:-.01em;
  line-height:1.08;
  margin-bottom:18px;
}
.section-title .accent{
  background:var(--grad-signal);
  -webkit-background-clip:text;
  background-clip:text;
  color:transparent;
}
.section-lede{
  max-width:640px;
  color:var(--c-mist);
  font-size:1.05rem;
  line-height:1.7;
  margin-bottom:64px;
}

/* ---------- glass / panel primitives ---------- */
.glass{
  background:var(--glass-bg);
  border:1px solid var(--glass-brd);
  border-radius:var(--radius-md);
  backdrop-filter:blur(18px) saturate(140%);
  -webkit-backdrop-filter:blur(18px) saturate(140%);
  position:relative;
  transition:border-color .4s var(--ease-out),transform .4s var(--ease-out),box-shadow .4s var(--ease-out);
}
.glass:hover{border-color:var(--glass-brd-hi);}

.corner-frame{position:relative;}
.corner-frame::before,.corner-frame::after{
  content:'';
  position:absolute;
  width:16px;height:16px;
  border:1.5px solid var(--c-blue);
  opacity:.55;
  transition:opacity .3s var(--ease-out);
}
.corner-frame::before{top:-1px;left:-1px;border-right:none;border-bottom:none;}
.corner-frame::after{bottom:-1px;right:-1px;border-left:none;border-top:none;}
.corner-frame:hover::before,.corner-frame:hover::after{opacity:1;}

/* ---------- buttons ---------- */
.btn{
  display:inline-flex;
  align-items:center;
  gap:10px;
  font-family:var(--font-mono);
  font-size:.86rem;
  letter-spacing:.04em;
  padding:15px 30px;
  border-radius:var(--radius-full);
  position:relative;
  isolation:isolate;
  overflow:hidden;
}
.btn-primary{
  background:var(--grad-signal);
  color:#040410;
  font-weight:600;
  box-shadow:0 0 0 1px rgba(255,255,255,.12) inset,0 12px 30px -10px rgba(0,212,255,.5);
}
.btn-primary:hover{box-shadow:0 0 0 1px rgba(255,255,255,.2) inset,0 16px 38px -8px rgba(168,85,247,.6);}
.btn-ghost{
  border:1px solid var(--glass-brd-hi);
  color:var(--c-paper);
  background:rgba(255,255,255,.02);
}
.btn-ghost:hover{border-color:var(--c-blue);color:var(--c-blue);}
.btn-sm{padding:10px 20px;font-size:.76rem;}

/* ---------- chips ---------- */
.chip{
  display:inline-flex;
  align-items:center;
  gap:8px;
  font-family:var(--font-mono);
  font-size:.74rem;
  letter-spacing:.03em;
  padding:7px 14px;
  border-radius:var(--radius-full);
  border:1px solid var(--glass-brd);
  color:var(--c-mist);
  background:rgba(255,255,255,.03);
}

/* ---------- custom cursor ---------- */
#cursor-dot,#cursor-ring{
  position:fixed;top:0;left:0;
  border-radius:50%;
  pointer-events:none;
  z-index:9999;
  transform:translate(-50%,-50%);
  will-change:transform;
}
#cursor-dot{
  width:6px;height:6px;
  background:var(--c-cyan);
  box-shadow:0 0 8px var(--c-cyan);
}
#cursor-ring{
  width:34px;height:34px;
  border:1px solid rgba(0,212,255,.5);
  transition:width .25s var(--ease-out),height .25s var(--ease-out),border-color .25s,background .25s;
}
#cursor-ring.is-active{
  width:64px;height:64px;
  border-color:var(--c-violet);
  background:rgba(168,85,247,.08);
}
@media (hover:none),(pointer:coarse){ #cursor-dot,#cursor-ring{display:none;} }

/* ---------- nav ---------- */
#site-nav{
  position:fixed;top:0;left:0;right:0;
  height:var(--nav-h);
  z-index:500;
  display:flex;align-items:center;
  padding:0 32px;
  transition:background .4s,border-color .4s,backdrop-filter .4s;
  border-bottom:1px solid transparent;
}
#site-nav.is-scrolled{
  background:rgba(5,5,13,.72);
  backdrop-filter:blur(16px);
  -webkit-backdrop-filter:blur(16px);
  border-bottom-color:var(--glass-brd);
}
.nav-inner{width:100%;max-width:var(--container);margin:0 auto;display:flex;align-items:center;justify-content:space-between;}
.nav-logo{font-family:var(--font-mono);font-size:.95rem;letter-spacing:.04em;display:flex;align-items:center;gap:10px;}
.nav-logo .dot{width:8px;height:8px;border-radius:50%;background:var(--c-cyan);box-shadow:0 0 10px var(--c-cyan);}
.nav-links{display:flex;gap:6px;}
.nav-links a{
  font-family:var(--font-mono);
  font-size:.72rem;
  letter-spacing:.08em;
  text-transform:uppercase;
  color:var(--c-mist);
  padding:9px 15px;
  border-radius:var(--radius-full);
  transition:color .3s,background .3s;
}
.nav-links a:hover,.nav-links a.is-active{color:var(--c-paper);background:rgba(255,255,255,.06);}
.nav-toggle{display:none;width:40px;height:40px;border:1px solid var(--glass-brd-hi);border-radius:10px;align-items:center;justify-content:center;color:var(--c-paper);}
@media (max-width:900px){
  .nav-links{position:fixed;top:var(--nav-h);left:0;right:0;flex-direction:column;background:rgba(6,6,16,.97);backdrop-filter:blur(20px);padding:18px 24px 28px;gap:4px;border-bottom:1px solid var(--glass-brd);transform:translateY(-8px);opacity:0;pointer-events:none;transition:opacity .3s,transform .3s;}
  .nav-links.is-open{opacity:1;transform:translateY(0);pointer-events:auto;}
  .nav-links a{padding:12px 6px;}
  .nav-toggle{display:flex;}
}

/* ---------- progress bar ---------- */
#scroll-progress{position:fixed;top:0;left:0;height:2px;width:0%;background:var(--grad-signal);z-index:600;box-shadow:0 0 10px var(--c-blue);}


/* ==========================================================================
   HERO
   ========================================================================== */
#hero{
  min-height:100svh;
  display:flex;
  align-items:center;
  padding:calc(var(--nav-h) + 40px) 0 80px;
  overflow:hidden;
}
#hero-bg{position:absolute;inset:0;z-index:0;background:radial-gradient(ellipse 80% 60% at 50% 0%,#0d0f2a 0%,var(--c-void) 60%);}
#three-canvas{position:absolute;inset:0;z-index:1;opacity:.85;}
.aurora{position:absolute;inset:-10%;z-index:1;filter:blur(60px);pointer-events:none;mix-blend-mode:screen;}
.aurora span{position:absolute;border-radius:50%;opacity:.55;}
.aurora span:nth-child(1){width:42vw;height:42vw;top:-10%;left:-8%;background:radial-gradient(circle,rgba(0,212,255,.5),transparent 70%);animation:auroraFloat1 22s ease-in-out infinite;}
.aurora span:nth-child(2){width:38vw;height:38vw;top:10%;right:-10%;background:radial-gradient(circle,rgba(168,85,247,.45),transparent 70%);animation:auroraFloat2 26s ease-in-out infinite;}
.aurora span:nth-child(3){width:34vw;height:34vw;bottom:-12%;left:30%;background:radial-gradient(circle,rgba(45,226,198,.4),transparent 70%);animation:auroraFloat3 30s ease-in-out infinite;}
@keyframes auroraFloat1{0%,100%{transform:translate(0,0) scale(1);}50%{transform:translate(6vw,4vw) scale(1.15);}}
@keyframes auroraFloat2{0%,100%{transform:translate(0,0) scale(1);}50%{transform:translate(-5vw,6vw) scale(1.1);}}
@keyframes auroraFloat3{0%,100%{transform:translate(0,0) scale(1);}50%{transform:translate(4vw,-5vw) scale(1.2);}}

.grid-floor{
  position:absolute;left:0;right:0;bottom:0;height:46%;z-index:1;
  background-image:linear-gradient(rgba(0,212,255,.14) 1px,transparent 1px),linear-gradient(90deg,rgba(0,212,255,.14) 1px,transparent 1px);
  background-size:44px 44px;
  transform:perspective(340px) rotateX(62deg);
  transform-origin:bottom;
  -webkit-mask-image:linear-gradient(to top,rgba(0,0,0,.9),transparent 92%);
  mask-image:linear-gradient(to top,rgba(0,0,0,.9),transparent 92%);
  animation:gridMove 6s linear infinite;
}
@keyframes gridMove{from{background-position:0 0,0 0;}to{background-position:0 44px,0 0;}}

#mouse-glow{position:fixed;width:520px;height:520px;border-radius:50%;pointer-events:none;z-index:2;background:radial-gradient(circle,rgba(0,212,255,.10),transparent 65%);transform:translate(-50%,-50%);will-change:transform;}

.hero-inner{position:relative;z-index:3;display:grid;grid-template-columns:1.05fr .95fr;gap:56px;align-items:center;width:100%;}
@media (max-width:980px){.hero-inner{grid-template-columns:1fr;gap:64px;text-align:center;}}

.hero-copy .eyebrow{justify-content:flex-start;}
@media (max-width:980px){.hero-copy .eyebrow{justify-content:center;}}

.hero-name{
  font-family:var(--font-display);
  font-weight:700;
  font-size:clamp(2.4rem,5.4vw,4.3rem);
  line-height:1.04;
  letter-spacing:-.015em;
  margin-bottom:22px;
}
.hero-name .grad{background:var(--grad-signal);-webkit-background-clip:text;background-clip:text;color:transparent;}

.terminal{
  border:1px solid var(--glass-brd);
  border-radius:var(--radius-md);
  background:rgba(8,9,20,.55);
  padding:22px 26px;
  max-width:560px;
  backdrop-filter:blur(14px);
}
@media (max-width:980px){.terminal{margin:0 auto;}}
.terminal-bar{display:flex;align-items:center;gap:8px;margin-bottom:16px;}
.terminal-bar span{width:9px;height:9px;border-radius:50%;background:var(--c-mist-dim);}
.terminal-bar .lbl{margin-left:8px;font-family:var(--font-mono);font-size:.7rem;color:var(--c-mist-dim);letter-spacing:.06em;}
#typed-line{
  font-family:var(--font-mono);
  font-size:1rem;
  line-height:1.75;
  color:var(--c-paper);
  min-height:130px;
  white-space:pre-wrap;
}
#typed-line .caret{display:inline-block;width:2px;height:1em;background:var(--c-cyan);margin-left:2px;vertical-align:-2px;animation:caretBlink 1s step-end infinite;}
@keyframes caretBlink{0%,49%{opacity:1;}50%,100%{opacity:0;}}

.hero-ctas{display:flex;gap:16px;margin-top:34px;flex-wrap:wrap;}
@media (max-width:980px){.hero-ctas{justify-content:center;}}

.scroll-cue{
  position:absolute;bottom:36px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:10px;
  font-family:var(--font-mono);font-size:.68rem;letter-spacing:.16em;color:var(--c-mist-dim);
  z-index:3;
}
.scroll-cue .line{width:1px;height:34px;background:linear-gradient(var(--c-blue),transparent);animation:scrollCue 2s ease-in-out infinite;}
@keyframes scrollCue{0%{transform:scaleY(0);transform-origin:top;}50%{transform:scaleY(1);transform-origin:top;}51%{transform-origin:bottom;}100%{transform:scaleY(0);transform-origin:bottom;}}

/* ---------- hologram pod (signature element) ---------- */
.pod-wrap{position:relative;width:min(400px,80vw);margin:0 auto;aspect-ratio:4/5;}
.pod-ring{
  position:absolute;inset:-26px;
  border-radius:38% 38% 42% 42%/48% 48% 40% 40%;
  background:conic-gradient(from 0deg,var(--c-blue),var(--c-violet),var(--c-cyan),var(--c-blue));
  padding:2px;
  -webkit-mask:linear-gradient(#000,#000) content-box,linear-gradient(#000,#000);
  -webkit-mask-composite:xor;
  mask-composite:exclude;
  animation:podSpin 14s linear infinite;
  opacity:.85;
}
@keyframes podSpin{to{transform:rotate(360deg);}}
.pod-frame{
  position:absolute;inset:0;
  border-radius:38% 38% 42% 42%/48% 48% 40% 40%;
  overflow:hidden;
  border:1px solid rgba(255,255,255,.14);
  box-shadow:0 0 60px -10px rgba(0,212,255,.35),0 0 120px -20px rgba(168,85,247,.3);
  animation:podBreathe 5s ease-in-out infinite;
  transform-style:preserve-3d;
  will-change:transform;
}
@keyframes podBreathe{0%,100%{transform:scale(1);}50%{transform:scale(1.018);}}
.pod-frame img{width:100%;height:100%;object-fit:cover;object-position:center 18%;filter:saturate(1.05) contrast(1.04);}
.pod-scan{position:absolute;inset:0;background:repeating-linear-gradient(0deg,rgba(0,212,255,.09) 0px,rgba(0,212,255,.09) 1px,transparent 2px,transparent 4px);mix-blend-mode:overlay;pointer-events:none;}
.pod-sweep{position:absolute;left:0;right:0;height:36%;background:linear-gradient(180deg,transparent,rgba(45,226,198,.22),transparent);animation:podSweep 4.5s ease-in-out infinite;pointer-events:none;}
@keyframes podSweep{0%{top:-40%;}100%{top:104%;}}
.pod-vignette{position:absolute;inset:0;background:linear-gradient(180deg,rgba(5,5,13,0) 55%,rgba(5,5,13,.75) 100%);pointer-events:none;}

.pod-tag{
  position:absolute;
  font-family:var(--font-mono);
  font-size:.68rem;
  letter-spacing:.05em;
  padding:6px 12px;
  border-radius:var(--radius-full);
  border:1px solid var(--glass-brd-hi);
  background:rgba(8,9,20,.7);
  backdrop-filter:blur(8px);
  white-space:nowrap;
  animation:tagFloat 6s ease-in-out infinite;
}
.pod-tag:nth-child(1){top:2%;left:-14%;animation-delay:0s;}
.pod-tag:nth-child(2){top:22%;right:-20%;animation-delay:.7s;}
.pod-tag:nth-child(3){top:52%;left:-22%;animation-delay:1.4s;}
.pod-tag:nth-child(4){bottom:16%;right:-16%;animation-delay:2.1s;}
.pod-tag:nth-child(5){bottom:-4%;left:6%;animation-delay:2.8s;}
@keyframes tagFloat{0%,100%{transform:translateY(0);}50%{transform:translateY(-9px);}}
@media (max-width:980px){.pod-tag{display:none;}}
@media (max-width:640px){.pod-wrap{width:min(300px,72vw);}}


/* ==========================================================================
   ABOUT
   ========================================================================== */
.about-grid{display:grid;grid-template-columns:.86fr 1.14fr;gap:28px;align-items:start;}
@media (max-width:940px){.about-grid{grid-template-columns:1fr;}}

.about-portrait{padding:14px;}
.about-portrait .frame{border-radius:calc(var(--radius-lg) - 8px);overflow:hidden;aspect-ratio:1/1;position:relative;}
.about-portrait img{width:100%;height:100%;object-fit:cover;filter:grayscale(.15) contrast(1.05);}
.about-portrait .frame::after{content:'';position:absolute;inset:0;background:linear-gradient(160deg,rgba(0,212,255,.22),transparent 45%,rgba(168,85,247,.22));mix-blend-mode:overlay;}
.about-portrait .caption{display:flex;justify-content:space-between;align-items:center;padding:16px 6px 4px;font-family:var(--font-mono);font-size:.72rem;color:var(--c-mist-dim);letter-spacing:.04em;}

.about-cards{display:grid;grid-template-columns:1fr 1fr;gap:20px;}
@media (max-width:600px){.about-cards{grid-template-columns:1fr;}}
.about-card{padding:26px 26px 24px;grid-column:span 1;}
.about-card.span-2{grid-column:span 2;}
@media (max-width:600px){.about-card.span-2{grid-column:span 1;}}
.about-card h3{font-family:var(--font-display);font-size:1.1rem;margin-bottom:12px;display:flex;align-items:center;gap:10px;}
.about-card h3 svg{width:18px;height:18px;color:var(--c-blue);}
.about-card p{color:var(--c-mist);font-size:.92rem;line-height:1.7;}
.about-card .row{display:flex;justify-content:space-between;font-size:.86rem;padding:9px 0;border-bottom:1px dashed var(--glass-brd);color:var(--c-mist);}
.about-card .row:last-child{border-bottom:none;}
.about-card .row b{color:var(--c-paper);font-weight:500;text-align:right;}
.about-card .interest-tags{display:flex;flex-wrap:wrap;gap:8px;}

.stat-row{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;margin-top:28px;}
@media (max-width:700px){.stat-row{grid-template-columns:repeat(2,1fr);}}
.stat{padding:22px 18px;text-align:center;}
.stat .num{font-family:var(--font-display);font-size:2.1rem;font-weight:700;background:var(--grad-signal);-webkit-background-clip:text;background-clip:text;color:transparent;}
.stat .lbl{font-family:var(--font-mono);font-size:.68rem;letter-spacing:.06em;color:var(--c-mist-dim);text-transform:uppercase;margin-top:6px;}

/* ==========================================================================
   SKILLS
   ========================================================================== */
.skill-tabs{display:flex;gap:10px;margin-bottom:36px;flex-wrap:wrap;}
.skill-tab{
  font-family:var(--font-mono);font-size:.76rem;letter-spacing:.04em;
  padding:11px 20px;border-radius:var(--radius-full);
  border:1px solid var(--glass-brd);color:var(--c-mist);
  transition:all .3s var(--ease-out);
}
.skill-tab.is-active{color:#040410;background:var(--grad-signal);border-color:transparent;font-weight:600;}
.skill-tab:not(.is-active):hover{border-color:var(--glass-brd-hi);color:var(--c-paper);}

.skill-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(148px,1fr));gap:16px;}
.skill-card{
  padding:22px 14px;
  display:flex;flex-direction:column;align-items:center;gap:12px;
  text-align:center;
  opacity:0;transform:translateY(16px) scale(.96);
}
.skill-card.is-in{opacity:1;transform:none;transition:opacity .5s var(--ease-out),transform .5s var(--ease-out);}
.skill-card:hover{transform:translateY(-6px);box-shadow:0 16px 40px -18px rgba(0,212,255,.35);}
.skill-ic{width:38px;height:38px;display:flex;align-items:center;justify-content:center;}
.skill-ic img{width:34px;height:34px;filter:drop-shadow(0 0 10px rgba(0,212,255,.35));}
.skill-badge{
  width:38px;height:38px;border-radius:10px;
  display:flex;align-items:center;justify-content:center;
  font-family:var(--font-display);font-weight:700;font-size:.9rem;
  background:var(--grad-signal);color:#040410;
}
.skill-card .name{font-size:.82rem;color:var(--c-mist);}
.skill-card:hover .name{color:var(--c-paper);}


/* ==========================================================================
   PROJECTS
   ========================================================================== */
.project-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:24px;}
.project-card{
  overflow:hidden;
  cursor:none;
  opacity:0;transform:translateY(24px);
}
@media (hover:none),(pointer:coarse){.project-card{cursor:pointer;}}
.project-card.is-in{opacity:1;transform:none;transition:opacity .6s var(--ease-out),transform .6s var(--ease-out);}
.project-cover{position:relative;aspect-ratio:16/10;overflow:hidden;}
.project-cover svg{width:100%;height:100%;display:block;transition:transform .6s var(--ease-out);}
.project-card:hover .project-cover svg{transform:scale(1.06);}
.project-cover .idx{position:absolute;top:14px;left:14px;font-family:var(--font-mono);font-size:.7rem;color:rgba(255,255,255,.65);background:rgba(5,5,13,.5);padding:4px 10px;border-radius:var(--radius-full);backdrop-filter:blur(6px);}
.project-body{padding:22px 24px 24px;}
.project-body h3{font-family:var(--font-display);font-size:1.18rem;margin-bottom:8px;}
.project-body .tagline{font-size:.68rem;font-family:var(--font-mono);color:var(--c-cyan);letter-spacing:.06em;text-transform:uppercase;margin-bottom:10px;}
.project-body p{color:var(--c-mist);font-size:.88rem;line-height:1.65;margin-bottom:16px;}
.project-stack{display:flex;flex-wrap:wrap;gap:7px;margin-bottom:18px;}
.project-stack span{font-family:var(--font-mono);font-size:.68rem;color:var(--c-mist);padding:4px 10px;border:1px solid var(--glass-brd);border-radius:var(--radius-full);}
.project-links{display:flex;gap:10px;}
.project-links a{
  display:inline-flex;align-items:center;gap:6px;
  font-family:var(--font-mono);font-size:.72rem;color:var(--c-mist);
  padding:8px 14px;border:1px solid var(--glass-brd);border-radius:var(--radius-full);
  transition:color .3s,border-color .3s;
}
.project-links a:hover{color:var(--c-blue);border-color:var(--c-blue);}
.project-links svg{width:13px;height:13px;}

/* modal */
#project-modal{
  position:fixed;inset:0;z-index:1000;
  display:flex;align-items:center;justify-content:center;
  padding:24px;
  opacity:0;pointer-events:none;
  transition:opacity .35s var(--ease-out);
}
#project-modal.is-open{opacity:1;pointer-events:auto;}
#project-modal .backdrop{position:absolute;inset:0;background:rgba(4,4,10,.78);backdrop-filter:blur(6px);}
#project-modal .modal-panel{
  position:relative;z-index:1;max-width:640px;width:100%;max-height:82vh;overflow-y:auto;
  background:var(--c-panel);border:1px solid var(--glass-brd-hi);border-radius:var(--radius-lg);
  padding:36px;
  transform:translateY(24px) scale(.97);
  transition:transform .4s var(--ease-out);
}
#project-modal.is-open .modal-panel{transform:none;}
#project-modal .modal-close{position:absolute;top:20px;right:20px;width:36px;height:36px;border-radius:50%;border:1px solid var(--glass-brd-hi);display:flex;align-items:center;justify-content:center;}
#project-modal .modal-close svg{width:15px;height:15px;}
#project-modal h3{font-family:var(--font-display);font-size:1.6rem;margin-bottom:6px;padding-right:40px;}
#project-modal .tagline{font-family:var(--font-mono);font-size:.72rem;color:var(--c-cyan);text-transform:uppercase;letter-spacing:.06em;margin-bottom:20px;}
#project-modal .desc{color:var(--c-mist);font-size:.95rem;line-height:1.75;margin-bottom:22px;}
#project-modal .feat-title{font-family:var(--font-mono);font-size:.7rem;letter-spacing:.08em;text-transform:uppercase;color:var(--c-mist-dim);margin-bottom:12px;}
#project-modal .feat-list{display:grid;gap:10px;margin-bottom:24px;}
#project-modal .feat-list li{display:flex;gap:10px;font-size:.88rem;color:var(--c-paper);align-items:flex-start;}
#project-modal .feat-list li svg{width:15px;height:15px;color:var(--c-cyan);flex-shrink:0;margin-top:2px;}

/* ==========================================================================
   DRONE SHOWCASE
   ========================================================================== */
#drone{background:radial-gradient(ellipse 70% 50% at 50% 30%,rgba(0,212,255,.06),transparent 70%);}
.drone-stage{
  position:relative;
  height:min(70vh,560px);
  border-radius:var(--radius-lg);
  overflow:hidden;
  background:linear-gradient(180deg,var(--c-void-2),#08091a);
}
.drone-stage .grid-floor{height:60%;opacity:.7;}
.drone-stage svg{position:absolute;inset:0;width:100%;height:100%;}
#drone-hud{position:absolute;top:20px;left:20px;right:20px;display:flex;justify-content:space-between;font-family:var(--font-mono);font-size:.68rem;color:var(--c-cyan);letter-spacing:.06em;pointer-events:none;}
#drone-hud span{background:rgba(5,6,15,.5);padding:5px 11px;border-radius:var(--radius-full);border:1px solid rgba(45,226,198,.25);}
.drone-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;margin-top:24px;}
@media (max-width:700px){.drone-stats{grid-template-columns:1fr;}}
.drone-stat{padding:20px;text-align:center;}
.drone-stat .num{font-family:var(--font-display);font-weight:700;font-size:1.8rem;color:var(--c-cyan);}
.drone-stat .lbl{font-family:var(--font-mono);font-size:.68rem;color:var(--c-mist-dim);letter-spacing:.05em;margin-top:4px;text-transform:uppercase;}
.drone-stat .note{font-family:var(--font-mono);font-size:.6rem;color:var(--c-mist-dim);opacity:.6;margin-top:2px;}


/* ==========================================================================
   JOURNEY TIMELINE
   ========================================================================== */
.timeline{position:relative;max-width:760px;margin:0 auto;padding-left:0;}
.timeline-track{position:absolute;left:19px;top:6px;bottom:6px;width:2px;background:var(--glass-brd);}
.timeline-track .fill{position:absolute;top:0;left:0;width:100%;height:0%;background:linear-gradient(180deg,var(--c-blue),var(--c-violet),var(--c-cyan));box-shadow:0 0 12px rgba(0,212,255,.6);}
.timeline-item{position:relative;padding:0 0 46px 58px;opacity:0;transform:translateX(-14px);}
.timeline-item.is-in{opacity:1;transform:none;transition:opacity .5s var(--ease-out),transform .5s var(--ease-out);}
.timeline-item:last-child{padding-bottom:0;}
.timeline-node{position:absolute;left:11px;top:2px;width:18px;height:18px;border-radius:50%;background:var(--c-void);border:2px solid var(--c-mist-dim);transition:border-color .4s,box-shadow .4s;}
.timeline-item.is-in .timeline-node{border-color:var(--c-blue);box-shadow:0 0 14px rgba(0,212,255,.6);}
.timeline-item .step{font-family:var(--font-mono);font-size:.68rem;color:var(--c-mist-dim);letter-spacing:.08em;}
.timeline-item h4{font-family:var(--font-display);font-size:1.15rem;margin:4px 0 6px;}
.timeline-item p{color:var(--c-mist);font-size:.88rem;line-height:1.65;max-width:520px;}
.timeline-item.is-future h4{color:var(--c-cyan);}

/* ==========================================================================
   RESEARCH / LEADERSHIP (shared card grid)
   ========================================================================== */
.tile-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px;}
.tile{padding:28px 26px;opacity:0;transform:translateY(18px);}
.tile.is-in{opacity:1;transform:none;transition:opacity .5s var(--ease-out),transform .5s var(--ease-out);}
.tile .tile-ic{width:42px;height:42px;border-radius:12px;background:rgba(0,212,255,.08);border:1px solid rgba(0,212,255,.2);display:flex;align-items:center;justify-content:center;margin-bottom:16px;}
.tile .tile-ic svg{width:20px;height:20px;color:var(--c-blue);}
.tile h4{font-family:var(--font-display);font-size:1.05rem;margin-bottom:8px;}
.tile p{color:var(--c-mist);font-size:.86rem;line-height:1.65;}

/* ==========================================================================
   GITHUB
   ========================================================================== */
.gh-top{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:20px;margin-bottom:32px;}
.gh-handle{font-family:var(--font-mono);color:var(--c-cyan);font-size:.95rem;}
.gh-stats-imgs{display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:20px;}
@media (max-width:760px){.gh-stats-imgs{grid-template-columns:1fr;}}
.gh-stats-imgs .glass{padding:6px;overflow:hidden;}
.gh-stats-imgs img{width:100%;border-radius:calc(var(--radius-md) - 6px);display:block;}
.gh-counters{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;}
@media (max-width:700px){.gh-counters{grid-template-columns:repeat(2,1fr);}}
.gh-counters .stat .num{font-size:1.7rem;}
.gh-fallback{padding:40px;text-align:center;color:var(--c-mist);font-family:var(--font-mono);font-size:.85rem;}

/* ==========================================================================
   CONTACT
   ========================================================================== */
#contact .container{max-width:920px;}
.contact-panel{padding:56px;text-align:center;position:relative;overflow:hidden;}
.contact-panel::before{content:'';position:absolute;inset:0;background:var(--aurora, radial-gradient(circle at 50% 0%,rgba(0,212,255,.12),transparent 60%));pointer-events:none;}
.contact-panel h2{font-family:var(--font-display);font-size:clamp(1.9rem,4vw,2.8rem);margin-bottom:16px;}
.contact-panel p{color:var(--c-mist);max-width:480px;margin:0 auto 36px;}
.contact-socials{display:flex;justify-content:center;gap:14px;flex-wrap:wrap;margin-bottom:30px;}
.social-btn{
  width:52px;height:52px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  border:1px solid var(--glass-brd-hi);
  transition:transform .3s var(--ease-out),border-color .3s,box-shadow .3s;
}
.social-btn svg{width:20px;height:20px;}
.social-btn:hover{transform:translateY(-4px);border-color:var(--c-blue);box-shadow:0 10px 24px -8px rgba(0,212,255,.5);}
.contact-loc{font-family:var(--font-mono);font-size:.78rem;color:var(--c-mist-dim);display:flex;align-items:center;justify-content:center;gap:8px;}
.contact-loc svg{width:14px;height:14px;}

/* ==========================================================================
   FOOTER
   ========================================================================== */
footer{padding:44px 0 36px;border-top:1px solid var(--glass-brd);}
.footer-inner{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:16px;font-family:var(--font-mono);font-size:.72rem;color:var(--c-mist-dim);}
.footer-inner .back-top{display:flex;align-items:center;gap:8px;border:1px solid var(--glass-brd);padding:9px 16px;border-radius:var(--radius-full);}
.footer-inner .back-top svg{width:12px;height:12px;}

/* ==========================================================================
   AI CORE COMPANION
   ========================================================================== */
#ai-core{
  position:fixed;right:22px;bottom:22px;z-index:400;
  display:flex;align-items:center;gap:12px;
  font-family:var(--font-mono);
}
#ai-core .core-label{
  font-size:.68rem;color:var(--c-mist);letter-spacing:.03em;
  background:rgba(9,10,23,.72);border:1px solid var(--glass-brd);
  padding:8px 13px;border-radius:var(--radius-full);
  backdrop-filter:blur(10px);
  opacity:0;transform:translateX(6px);
  transition:opacity .35s var(--ease-out),transform .35s var(--ease-out);
  white-space:nowrap;
}
#ai-core.is-active .core-label{opacity:1;transform:none;}
#ai-core .core-orb{
  position:relative;width:50px;height:50px;border-radius:50%;
  background:radial-gradient(circle at 35% 30%,#1a1c3a,#07081a 70%);
  border:1px solid var(--glass-brd-hi);
  display:flex;align-items:center;justify-content:center;
  box-shadow:0 0 30px -6px rgba(0,212,255,.5);
  animation:coreBreathe 3.2s ease-in-out infinite;
}
@keyframes coreBreathe{0%,100%{box-shadow:0 0 22px -6px rgba(0,212,255,.45);}50%{box-shadow:0 0 34px -4px rgba(168,85,247,.55);}}
#ai-core .core-orb svg{width:20px;height:20px;color:var(--c-cyan);transition:color .4s;}
#ai-core .core-ring{position:absolute;inset:-6px;border-radius:50%;border:1px solid rgba(0,212,255,.35);animation:coreSpin 8s linear infinite;}
@keyframes coreSpin{to{transform:rotate(360deg);}}
@media (max-width:640px){#ai-core{right:14px;bottom:14px;}#ai-core .core-label{display:none;}#ai-core .core-orb{width:44px;height:44px;}}

/* ==========================================================================
   REDUCED MOTION
   ========================================================================== */
@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.01ms !important;animation-iteration-count:1 !important;transition-duration:.01ms !important;scroll-behavior:auto !important;}
}

/* ==========================================================================
   RESPONSIVE (global refinements)
   ========================================================================== */
@media (max-width:640px){
  .container{padding:0 20px;}
  .about-grid,.project-grid{gap:18px;}
}
```

---

## `body.html` (section markup — goes inside `<body>`)

```html
  <div id="cursor-dot"></div>
  <div id="cursor-ring"></div>
  <div id="scroll-progress"></div>
  <div id="mouse-glow"></div>

  <nav id="site-nav">
    <div class="nav-inner">
      <a href="#hero" class="nav-logo"><span class="dot"></span>SRAVAN.SYS</a>
      <div class="nav-links" id="nav-links">
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#projects">Projects</a>
        <a href="#drone">Drone</a>
        <a href="#journey">Journey</a>
        <a href="#research">Research</a>
        <a href="#github">GitHub</a>
        <a href="#contact">Contact</a>
      </div>
      <button class="nav-toggle" id="nav-toggle" aria-label="Toggle menu">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 6h18M3 12h18M3 18h18"/></svg>
      </button>
    </div>
  </nav>

  <!-- ============================= HERO ============================= -->
  <section id="hero">
    <div id="hero-bg"></div>
    <canvas id="three-canvas"></canvas>
    <div class="aurora"><span></span><span></span><span></span></div>
    <div class="grid-floor"></div>

    <div class="container hero-inner">
      <div class="hero-copy">
        <p class="eyebrow">AI OPERATING SYSTEM // BOOT SEQUENCE COMPLETE</p>
        <h1 class="hero-name">Vundela Sravan<br><span class="grad">Sri Siva Kumar Reddy</span></h1>
        <div class="terminal corner-frame">
          <div class="terminal-bar"><span></span><span></span><span></span><span class="lbl">guide.exe — running</span></div>
          <p id="typed-line"></p>
        </div>
        <div class="hero-ctas">
          <a href="#about" class="btn btn-primary magnetic" data-cursor="big">Start Journey <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M13 6l6 6-6 6"/></svg></a>
          <a href="#projects" class="btn btn-ghost magnetic" data-cursor="big">View Projects</a>
        </div>
      </div>

      <div class="hero-avatar">
        <div class="pod-wrap">
          <div class="pod-ring"></div>
          <div class="pod-frame magnetic-tilt" id="pod-frame">
            <img src="__HERO_IMG__" alt="Sravan — portrait">
            <div class="pod-scan"></div>
            <div class="pod-sweep"></div>
            <div class="pod-vignette"></div>
          </div>
          <span class="pod-tag" style="border-color:rgba(0,212,255,.4);color:var(--c-blue);">Artificial Intelligence</span>
          <span class="pod-tag" style="border-color:rgba(168,85,247,.4);color:var(--c-violet);">Computer Vision</span>
          <span class="pod-tag" style="border-color:rgba(45,226,198,.4);color:var(--c-cyan);">Robotics</span>
          <span class="pod-tag" style="border-color:rgba(0,212,255,.4);color:var(--c-blue);">Embedded Systems</span>
          <span class="pod-tag" style="border-color:rgba(168,85,247,.4);color:var(--c-violet);">Full-Stack</span>
        </div>
      </div>
    </div>

    <div class="scroll-cue"><span>SCROLL</span><span class="line"></span></div>
  </section>

  <!-- ============================= ABOUT ============================= -->
  <section id="about">
    <div class="container">
      <p class="eyebrow">SYS.01 — ABOUT ME</p>
      <h2 class="section-title">Engineering systems that <span class="accent">understand the world</span>, not just compute it.</h2>
      <p class="section-lede">Computer Science Engineering student building at the intersection of intelligence and hardware — where a model doesn't just predict, it sees, flies, and responds.</p>

      <div class="about-grid">
        <div class="glass about-portrait corner-frame">
          <div class="frame"><img src="__ABOUT_IMG__" alt="Sravan, close portrait" loading="lazy"></div>
          <div class="caption"><span>SRAVAN.JPG</span><span>NAGERCOIL, IN</span></div>
        </div>

        <div class="about-cards">
          <div class="glass about-card">
            <h3><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M22 10 12 5 2 10l10 5 10-5Z"/><path d="M6 12v5c0 1.5 3 3 6 3s6-1.5 6-3v-5"/></svg>Education</h3>
            <div class="row"><span>University</span><b>Amrita Vishwa Vidyapeetham</b></div>
            <div class="row"><span>Campus</span><b>Nagercoil</b></div>
            <div class="row"><span>Degree</span><b>B.Tech, CSE</b></div>
            <div class="row"><span>Status</span><b>3rd Year · 5th Semester</b></div>
          </div>

          <div class="glass about-card">
            <h3><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4"/><circle cx="12" cy="12" r=".6" fill="currentColor"/></svg>Mission</h3>
            <p>Build intelligent systems that improve human lives through AI, Robotics, Computer Vision, and Embedded Systems.</p>
          </div>

          <div class="glass about-card span-2">
            <h3><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M13 2 3 14h7l-1 8 10-12h-7l1-8Z"/></svg>Focus Areas</h3>
            <div class="interest-tags">
              <span class="chip">Artificial Intelligence</span>
              <span class="chip">Machine Learning</span>
              <span class="chip">Deep Learning</span>
              <span class="chip">Computer Vision</span>
              <span class="chip">Robotics</span>
              <span class="chip">Embedded Systems</span>
              <span class="chip">Drone Technology</span>
              <span class="chip">IoT</span>
              <span class="chip">Full Stack Dev</span>
              <span class="chip">Cloud Computing</span>
              <span class="chip">Open Source</span>
              <span class="chip">Research</span>
            </div>
          </div>
        </div>
      </div>

      <div class="stat-row" id="about-stats">
        <div class="glass stat"><div class="num" data-count="10">0</div><div class="lbl">Projects Built</div></div>
        <div class="glass stat"><div class="num" data-count="12">0</div><div class="lbl">Technologies Used</div></div>
        <div class="glass stat"><div class="num" data-count="8">0</div><div class="lbl">Focus Domains</div></div>
        <div class="glass stat"><div class="num" data-count="3">0</div><div class="lbl">Year of Study</div></div>
      </div>
    </div>
  </section>

  <!-- ============================= SKILLS ============================= -->
  <section id="skills">
    <div class="container">
      <p class="eyebrow">SYS.02 — SKILLS</p>
      <h2 class="section-title">The <span class="accent">stack</span> behind the systems.</h2>
      <p class="section-lede">Languages, frameworks, and tools I reach for when turning an idea into something that runs, detects, and responds.</p>

      <div class="skill-tabs" id="skill-tabs"></div>
      <div class="skill-grid" id="skill-grid"></div>
    </div>
  </section>

  <!-- ============================= PROJECTS ============================= -->
  <section id="projects">
    <div class="container">
      <p class="eyebrow">SYS.03 — PROJECTS</p>
      <h2 class="section-title">Ten systems, <span class="accent">one obsession</span>.</h2>
      <p class="section-lede">From license-plate recognition on a Raspberry Pi to a climate digital twin — each project is a step in the same direction. Tap a card for the full brief.</p>
      <div class="project-grid" id="project-grid"></div>
    </div>
  </section>

  <!-- ============================= DRONE SHOWCASE ============================= -->
  <section id="drone">
    <div class="container">
      <p class="eyebrow">SYS.04 — DRONE INTELLIGENCE</p>
      <h2 class="section-title">Watching traffic <span class="accent">from above</span>.</h2>
      <p class="section-lede">A look at the AI Drone Traffic Monitoring System in action — helmet detection, plate recognition, and emergency-vehicle alerts, staged as a live scan.</p>

      <div class="glass drone-stage corner-frame" id="drone-stage">
        <div class="grid-floor"></div>
        <div id="drone-hud"><span>CAM_01 // LIVE-DEMO</span><span id="drone-clock">00:00:00</span></div>
        <svg id="drone-svg" viewBox="0 0 1000 560" preserveAspectRatio="xMidYMid slice"></svg>
      </div>

      <div class="drone-stats">
        <div class="glass drone-stat"><div class="num" data-count="128">0</div><div class="lbl">Vehicles Tracked</div><div class="note">demo data</div></div>
        <div class="glass drone-stat"><div class="num" data-count="24">0</div><div class="lbl">Helmet Violations Flagged</div><div class="note">demo data</div></div>
        <div class="glass drone-stat"><div class="num" data-count="3">0</div><div class="lbl">Emergency Vehicles Detected</div><div class="note">demo data</div></div>
      </div>
    </div>
  </section>

  <!-- ============================= JOURNEY ============================= -->
  <section id="journey">
    <div class="container">
      <p class="eyebrow">SYS.05 — JOURNEY</p>
      <h2 class="section-title">How <span class="accent">programming</span> became a mission.</h2>
      <p class="section-lede">Every stage built on the last — a straight line from first lines of code to what comes next.</p>
      <div class="timeline" id="timeline">
        <div class="timeline-track"><div class="fill" id="timeline-fill"></div></div>
      </div>
    </div>
  </section>

  <!-- ============================= RESEARCH ============================= -->
  <section id="research">
    <div class="container">
      <p class="eyebrow">SYS.06 — RESEARCH</p>
      <h2 class="section-title">Where I want to go <span class="accent">deeper</span>.</h2>
      <p class="section-lede">Areas I'm actively reading, experimenting, and building toward.</p>
      <div class="tile-grid" id="research-grid"></div>
    </div>
  </section>

  <!-- ============================= LEADERSHIP ============================= -->
  <section id="leadership">
    <div class="container">
      <p class="eyebrow">SYS.07 — LEADERSHIP</p>
      <h2 class="section-title">Beyond the <span class="accent">codebase</span>.</h2>
      <p class="section-lede">Add your specific roles, clubs, and events here — this section is wired and ready.</p>
      <div class="tile-grid" id="leadership-grid"></div>
    </div>
  </section>

  <!-- ============================= GITHUB ============================= -->
  <section id="github">
    <div class="container">
      <p class="eyebrow">SYS.08 — GITHUB</p>
      <h2 class="section-title">Commits, not <span class="accent">claims</span>.</h2>
      <div class="gh-top">
        <span class="gh-handle" id="gh-handle-label">@your-username</span>
        <a href="#" id="gh-profile-link" class="btn btn-ghost btn-sm magnetic" target="_blank" rel="noopener">View Full Profile →</a>
      </div>
      <div class="gh-stats-imgs" id="gh-stats-imgs">
        <div class="glass"><img id="gh-stats-img" alt="GitHub stats" loading="lazy"></div>
        <div class="glass"><img id="gh-lang-img" alt="Top languages" loading="lazy"></div>
      </div>
      <div class="glass" style="padding:6px;overflow:hidden;">
        <img id="gh-streak-img" alt="GitHub streak" loading="lazy" style="width:100%;border-radius:calc(var(--radius-md) - 6px);display:block;">
      </div>
    </div>
  </section>

  <!-- ============================= CONTACT ============================= -->
  <section id="contact">
    <div class="container">
      <div class="glass contact-panel corner-frame">
        <p class="eyebrow" style="justify-content:center;">SYS.09 — CONTACT</p>
        <h2>Let's build something <span class="accent" style="background:var(--grad-signal);-webkit-background-clip:text;background-clip:text;color:transparent;">intelligent</span>.</h2>
        <p>Open to collaborations, internships, and conversations about AI, robotics, and everything in between.</p>
        <div class="contact-socials" id="contact-socials"></div>
        <div class="contact-loc"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>Nagercoil, Tamil Nadu, India</div>
      </div>
    </div>
  </section>

  <footer>
    <div class="container footer-inner">
      <span>© <span id="year"></span> Sravan Reddy. Built as an AI OS, not a template.</span>
      <a href="#hero" class="back-top">Back to top <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 19V5M5 12l7-7 7 7"/></svg></a>
    </div>
  </footer>

  <div id="ai-core">
    <span class="core-label" id="core-label">Exploring the hero</span>
    <div class="core-orb"><div class="core-ring"></div><svg id="core-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6"><circle cx="12" cy="12" r="3"/><path d="M12 2v4M12 18v4M4.9 4.9l2.8 2.8M16.3 16.3l2.8 2.8M2 12h4M18 12h4M4.9 19.1l2.8-2.8M16.3 7.7l2.8-2.8"/></svg></div>
  </div>

  <div id="project-modal">
    <div class="backdrop" data-close="1"></div>
    <div class="modal-panel">
      <button class="modal-close" id="modal-close"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M6 6l12 12M18 6 6 18"/></svg></button>
      <div id="modal-body"></div>
    </div>
  </div>
```
