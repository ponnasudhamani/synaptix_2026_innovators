<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PulseIQ Pro — Advanced Health Intelligence</title>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,700;1,9..144,300&family=Instrument+Sans:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --cream:#F5F0E8;--cream2:#EDE8DC;--cream3:#E2DBCC;
  --ink:#1A1410;--ink2:#3D3530;--ink3:#6B5E56;
  --teal:#0A7B6C;--teal2:#0D9982;--teal-lt:#E0F4F1;--teal-mid:#B8E8E2;
  --amber:#C97B1A;--amber-lt:#FEF3E2;
  --red:#C0392B;--red-lt:#FDECEA;--red-mid:#F5C6C2;
  --green:#1A7B4A;--green-lt:#E6F4EE;
  --blue:#1A5C9C;--blue-lt:#E6EEF8;
  --purple:#7B1A9C;--purple-lt:#F3E6F8;
  --orange:#B85A00;
  --border:rgba(26,20,16,.1);--border2:rgba(26,20,16,.18);
  --shadow:0 1px 3px rgba(26,20,16,.08),0 4px 12px rgba(26,20,16,.05);
  --shadow-lg:0 4px 16px rgba(26,20,16,.1),0 12px 40px rgba(26,20,16,.06);
  --r:12px;--r2:8px;
  --ff-head:'Fraunces',Georgia,serif;--ff-body:'Instrument Sans',system-ui,sans-serif;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{font-size:15px;scroll-behavior:smooth}
body{background:var(--cream);color:var(--ink);font-family:var(--ff-body);min-height:100vh;-webkit-font-smoothing:antialiased}

/* ═══ LAYOUT ═══ */
.app-shell{display:flex;min-height:100vh}
.nav{width:224px;flex-shrink:0;background:var(--ink);display:flex;flex-direction:column;position:sticky;top:0;height:100vh;overflow:hidden}
.nav-brand{padding:26px 22px 20px;border-bottom:1px solid rgba(255,255,255,.08)}
.nav-brand-name{font-family:var(--ff-head);font-size:1.4rem;font-weight:700;color:#fff;letter-spacing:-.01em}
.nav-brand-sub{font-size:.68rem;color:rgba(255,255,255,.38);margin-top:2px;letter-spacing:.06em;text-transform:uppercase}
.nav-patient{margin:14px 12px;padding:11px;background:rgba(255,255,255,.06);border-radius:var(--r2);display:flex;align-items:center;gap:9px;cursor:pointer;transition:background .15s}
.nav-patient:hover{background:rgba(255,255,255,.1)}
.nav-avatar{width:34px;height:34px;border-radius:50%;background:var(--teal2);display:flex;align-items:center;justify-content:center;font-family:var(--ff-head);font-size:.85rem;font-weight:700;color:#fff;flex-shrink:0}
.nav-patient-name{font-size:.8rem;font-weight:600;color:#fff;line-height:1.2}
.nav-patient-id{font-size:.66rem;color:rgba(255,255,255,.38)}
.nav-links{flex:1;padding:8px 10px;display:flex;flex-direction:column;gap:2px;overflow-y:auto}
.nav-link{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:var(--r2);color:rgba(255,255,255,.55);font-size:.8rem;font-weight:500;cursor:pointer;transition:all .15s;border:none;background:none;width:100%;text-align:left}
.nav-link:hover{color:#fff;background:rgba(255,255,255,.07)}
.nav-link.active{color:#fff;background:var(--teal)}
.nav-link .icon{font-size:.95rem;width:20px;text-align:center;flex-shrink:0}
.nav-badge{margin-left:auto;padding:1px 7px;border-radius:20px;background:var(--red);color:#fff;font-size:.6rem;font-weight:700;display:none}
.nav-badge.show{display:block}
.nav-section-label{font-size:.6rem;color:rgba(255,255,255,.25);letter-spacing:.08em;text-transform:uppercase;padding:14px 12px 4px;font-weight:600}
.nav-footer{padding:14px 12px;border-top:1px solid rgba(255,255,255,.08);display:flex;flex-direction:column;gap:8px}
.live-chip{display:flex;align-items:center;gap:8px;padding:7px 11px;background:rgba(10,123,108,.22);border:1px solid rgba(10,123,108,.38);border-radius:var(--r2);font-size:.7rem;color:var(--teal2);font-weight:600}
.live-dot{width:7px;height:7px;border-radius:50%;background:var(--teal2);box-shadow:0 0 6px var(--teal2);animation:livepulse 1.8s ease-in-out infinite;flex-shrink:0}
.mic-chip{display:flex;align-items:center;gap:8px;padding:7px 11px;background:rgba(123,26,156,.22);border:1px solid rgba(123,26,156,.38);border-radius:var(--r2);font-size:.7rem;color:#c46be8;font-weight:600;cursor:pointer;transition:all .2s}
.mic-chip:hover{background:rgba(123,26,156,.35)}
.mic-chip.listening{background:rgba(123,26,156,.4);border-color:rgba(123,26,156,.8)}
.mic-dot{width:7px;height:7px;border-radius:50%;background:#c46be8;box-shadow:0 0 6px #c46be8;flex-shrink:0}
@keyframes livepulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.7)}}
.main-content{flex:1;overflow:hidden;display:flex;flex-direction:column}
.page{display:none;flex:1;overflow-y:auto}
.page.active{display:flex;flex-direction:column}
.page-header{padding:26px 30px 0;display:flex;align-items:flex-start;justify-content:space-between;flex-shrink:0}
.page-title{font-family:var(--ff-head);font-size:1.75rem;font-weight:500;color:var(--ink);letter-spacing:-.02em;line-height:1.2}
.page-subtitle{font-size:.8rem;color:var(--ink3);margin-top:4px}
.page-actions{display:flex;align-items:center;gap:8px}
.btn{padding:8px 16px;border-radius:var(--r2);font-family:var(--ff-body);font-size:.8rem;font-weight:600;cursor:pointer;transition:all .15s;border:none;display:inline-flex;align-items:center;gap:6px}
.btn-primary{background:var(--teal);color:#fff}
.btn-primary:hover{background:var(--teal2)}
.btn-danger{background:var(--red);color:#fff}
.btn-danger:hover{background:#a93226}
.btn-ghost{background:transparent;border:1.5px solid var(--border2);color:var(--ink2)}
.btn-ghost:hover{border-color:var(--ink3);background:var(--cream2)}
.btn-sm{padding:5px 11px;font-size:.74rem}
.btn-purple{background:var(--purple);color:#fff}
.btn-purple:hover{background:#9b22c2}

/* ═══ MONITOR PAGE ═══ */
.monitor-body{padding:22px 30px 30px;display:grid;grid-template-columns:1fr 310px;gap:18px;flex:1}
.hri-hero{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:26px;display:flex;align-items:center;gap:28px;grid-column:1/-1;position:relative;overflow:hidden}
.hri-hero::before{content:'';position:absolute;right:-60px;top:-60px;width:250px;height:250px;border-radius:50%;background:var(--teal-lt);opacity:.45}
.hri-gauge-box{position:relative;flex-shrink:0}
.hri-score-num{position:absolute;top:50%;left:50%;transform:translate(-50%,-44%);font-family:var(--ff-head);font-size:2.8rem;font-weight:700;line-height:1;transition:color .5s}
.hri-score-label{position:absolute;bottom:16%;left:50%;transform:translateX(-50%);font-size:.62rem;font-weight:600;color:var(--ink3);letter-spacing:.08em;text-transform:uppercase;white-space:nowrap}
.hri-hero-info{flex:1;position:relative;z-index:1}
.hri-status-badge{display:inline-flex;align-items:center;gap:7px;padding:5px 14px;border-radius:20px;font-size:.76rem;font-weight:700;letter-spacing:.04em;margin-bottom:10px;transition:all .4s}
.hri-hero-title{font-family:var(--ff-head);font-size:1.4rem;font-weight:500;color:var(--ink);line-height:1.3;margin-bottom:7px}
.hri-hero-desc{font-size:.82rem;color:var(--ink3);line-height:1.6;max-width:440px}
.hri-meta{display:flex;gap:20px;margin-top:14px;flex-wrap:wrap}
.hri-meta-item{display:flex;flex-direction:column;gap:2px}
.hri-meta-val{font-family:var(--ff-head);font-size:1.05rem;font-weight:500;color:var(--ink)}
.hri-meta-lbl{font-size:.65rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.06em}

/* Signal grid */
.signal-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;grid-column:1}
.sig-card{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:14px 16px 12px;position:relative;overflow:hidden;transition:box-shadow .2s,border-color .3s}
.sig-card:hover{box-shadow:var(--shadow-lg)}
.sig-card.alert-anim{border-color:var(--red);animation:card-pulse 2s ease infinite}
@keyframes card-pulse{0%,100%{box-shadow:var(--shadow)}50%{box-shadow:0 0 0 3px rgba(192,57,43,.15),var(--shadow-lg)}}
.sig-card-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.sig-icon{width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:.9rem;flex-shrink:0}
.sig-status-dot{width:7px;height:7px;border-radius:50%;background:var(--green)}
.sig-name{font-size:.68rem;font-weight:600;color:var(--ink3);letter-spacing:.04em;text-transform:uppercase;margin-bottom:1px}
.sig-val-row{display:flex;align-items:baseline;gap:4px;margin-bottom:8px}
.sig-val{font-family:var(--ff-head);font-size:1.8rem;font-weight:500;line-height:1;transition:color .3s}
.sig-unit{font-size:.72rem;color:var(--ink3);font-weight:500}
.sig-range{font-size:.65rem;color:var(--ink3);margin-bottom:6px}
.sig-bar-track{height:4px;border-radius:2px;background:var(--cream2);overflow:hidden}
.sig-bar-fill{height:100%;border-radius:2px;transition:width .4s ease,background .4s}
.sig-mini-wrap{height:34px;margin-top:7px}
canvas.sig-mini{display:block;width:100%;height:34px}
.sig-trend{font-size:.62rem;color:var(--ink3);margin-top:5px;display:flex;align-items:center;gap:3px}

/* Right column */
.monitor-right{display:flex;flex-direction:column;gap:12px}
.alert-banner{border-radius:var(--r);padding:14px;background:#fff;border:1px solid var(--border);box-shadow:var(--shadow);display:none}
.alert-banner.show{display:block}
.alert-banner-top{display:flex;align-items:center;gap:8px;margin-bottom:5px}
.alert-banner-icon{font-size:1.1rem}
.alert-banner-level{font-size:.72rem;font-weight:700;letter-spacing:.06em;text-transform:uppercase}
.alert-banner-time{font-size:.65rem;color:var(--ink3);margin-left:auto}
.alert-banner-msg{font-size:.78rem;color:var(--ink2);line-height:1.5}
.alert-banner-signals{display:flex;gap:5px;flex-wrap:wrap;margin-top:8px}
.signal-chip{padding:2px 8px;border-radius:20px;font-size:.65rem;font-weight:600;background:var(--cream2);color:var(--ink2)}
.widget{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:16px}
.widget-title{font-size:.7rem;font-weight:600;color:var(--ink3);letter-spacing:.06em;text-transform:uppercase;margin-bottom:10px;display:flex;align-items:center;justify-content:space-between}
.corr-heatmap{display:grid;gap:3px}
.corr-cell{aspect-ratio:1;border-radius:4px;display:flex;align-items:center;justify-content:center;font-size:.5rem;font-weight:700;transition:all .5s;cursor:default}
.corr-row-label{font-size:.55rem;color:var(--ink3);display:flex;align-items:center;justify-content:center;font-weight:600}
.corr-col-labels{gap:3px;margin-top:3px}
.corr-col-label{font-size:.52rem;color:var(--ink3);text-align:center;font-weight:600}
.scenario-btns{display:grid;grid-template-columns:1fr 1fr;gap:5px;margin-top:8px}
.scenario-btn{padding:6px 7px;border-radius:var(--r2);font-size:.7rem;font-weight:600;cursor:pointer;border:1.5px solid var(--border);background:var(--cream);color:var(--ink2);transition:all .15s;text-align:center}
.scenario-btn:hover{border-color:var(--teal);color:var(--teal);background:var(--teal-lt)}
.scenario-btn.active{border-color:var(--teal);background:var(--teal);color:#fff}
.scenario-btn.full{grid-column:1/-1}

/* ═══ MIC ANALYSIS WIDGET ═══ */
.mic-widget{background:linear-gradient(135deg,#2D1B42,#1A1028);border-radius:var(--r);border:1px solid rgba(196,107,232,.25);box-shadow:var(--shadow);padding:16px;position:relative;overflow:hidden}
.mic-widget::before{content:'';position:absolute;top:-40px;right:-40px;width:120px;height:120px;border-radius:50%;background:rgba(196,107,232,.08)}
.mic-widget-title{font-size:.7rem;font-weight:600;color:rgba(255,255,255,.6);letter-spacing:.06em;text-transform:uppercase;margin-bottom:10px;display:flex;align-items:center;gap:8px}
.mic-widget-title span{color:#c46be8}
.mic-visualizer{height:42px;background:rgba(255,255,255,.04);border-radius:8px;overflow:hidden;margin-bottom:10px;position:relative}
.mic-canvas{display:block;width:100%;height:42px}
.mic-detections{display:flex;flex-direction:column;gap:4px}
.mic-det-row{display:flex;align-items:center;justify-content:space-between;padding:5px 9px;border-radius:6px;background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.06)}
.mic-det-label{font-size:.7rem;color:rgba(255,255,255,.7);display:flex;align-items:center;gap:5px}
.mic-det-conf{font-size:.7rem;font-weight:700;color:#c46be8}
.mic-det-bar{flex:1;height:4px;background:rgba(255,255,255,.08);border-radius:2px;margin:0 10px;overflow:hidden}
.mic-det-fill{height:100%;border-radius:2px;background:linear-gradient(90deg,#7B1A9C,#c46be8);transition:width .5s ease}
.mic-start-btn{width:100%;padding:8px;border:none;border-radius:8px;background:rgba(123,26,156,.5);border:1px solid rgba(196,107,232,.35);color:#c46be8;font-size:.75rem;font-weight:600;cursor:pointer;transition:all .2s;font-family:var(--ff-body);margin-top:8px;display:flex;align-items:center;justify-content:center;gap:6px}
.mic-start-btn:hover{background:rgba(123,26,156,.7)}
.mic-start-btn.active{background:rgba(192,57,43,.5);border-color:rgba(192,57,43,.6);color:#f0a0a0}

/* ═══ STEP COUNT CARD ═══ */
.steps-ring-container{display:flex;align-items:center;gap:14px;margin-top:2px}
.steps-info{flex:1}
.steps-val{font-family:var(--ff-head);font-size:2rem;font-weight:600;color:var(--teal);line-height:1}
.steps-goal{font-size:.7rem;color:var(--ink3);margin-top:2px}
.steps-badges{display:flex;gap:4px;flex-wrap:wrap;margin-top:7px}
.steps-badge{padding:2px 8px;border-radius:12px;font-size:.64rem;font-weight:600}

/* ═══ FEVER / BODY TEMP GAUGE ═══ */
.fever-card{background:linear-gradient(135deg,#fff8ee,#fff);border-radius:var(--r);border:1px solid rgba(201,123,26,.2);box-shadow:var(--shadow);padding:16px}
.fever-zones{display:flex;gap:4px;margin:10px 0;height:8px;border-radius:4px;overflow:hidden}
.fever-zone{flex:1;transition:opacity .3s}
.fever-zone.active-zone{position:relative;box-shadow:0 0 8px currentColor}
.fever-arrow{width:0;height:0;border-left:6px solid transparent;border-right:6px solid transparent;transition:margin-left .5s ease}
.fever-labels{display:flex;justify-content:space-between;font-size:.58rem;color:var(--ink3);margin-top:4px}
.fever-status{display:inline-flex;align-items:center;gap:6px;padding:4px 12px;border-radius:20px;font-size:.74rem;font-weight:700;margin-top:8px}

/* ═══ ALERTS PAGE ═══ */
.alerts-body{padding:22px 30px 40px;display:flex;flex-direction:column;gap:18px}
.alert-stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:12px}
.stat-card{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:16px 18px}
.stat-card-val{font-family:var(--ff-head);font-size:1.9rem;font-weight:500;line-height:1;color:var(--ink);margin-bottom:3px}
.stat-card-lbl{font-size:.7rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em}
.alert-filter-row{display:flex;align-items:center;gap:7px;flex-wrap:wrap}
.filter-chip{padding:5px 12px;border-radius:20px;font-size:.73rem;font-weight:600;cursor:pointer;border:1.5px solid var(--border);background:#fff;color:var(--ink2);transition:all .15s}
.filter-chip.active{border-color:var(--teal);background:var(--teal-lt);color:var(--teal)}
.filter-chip:hover{border-color:var(--teal)}
.alert-list{display:flex;flex-direction:column;gap:9px}
.alert-row{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:14px 18px;display:flex;align-items:flex-start;gap:14px;cursor:pointer;transition:box-shadow .15s}
.alert-row:hover{box-shadow:var(--shadow-lg)}
.alert-row-icon{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0;margin-top:2px}
.alert-row-body{flex:1;min-width:0}
.alert-row-top{display:flex;align-items:center;gap:7px;margin-bottom:3px}
.alert-row-level{font-size:.68rem;font-weight:700;letter-spacing:.06em;text-transform:uppercase;padding:2px 8px;border-radius:20px}
.alert-row-hri{font-size:.7rem;font-weight:700;color:var(--ink2)}
.alert-row-time{margin-left:auto;font-size:.7rem;color:var(--ink3)}
.alert-row-title{font-size:.85rem;font-weight:600;color:var(--ink);margin-bottom:2px}
.alert-row-desc{font-size:.75rem;color:var(--ink3);line-height:1.5}
.alert-row-signals{display:flex;gap:5px;flex-wrap:wrap;margin-top:7px}

/* ═══ HISTORY PAGE ═══ */
.history-body{padding:22px 30px 40px;display:flex;flex-direction:column;gap:18px}
.history-tabs{display:flex;gap:0;background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:4px;width:fit-content}
.history-tab{padding:6px 18px;border-radius:var(--r2);font-size:.78rem;font-weight:600;cursor:pointer;color:var(--ink3);border:none;background:none;transition:all .15s}
.history-tab.active{background:var(--teal);color:#fff}
.history-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.history-card{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:18px}
.history-card-full{grid-column:1/-1}
.history-card-title{font-family:var(--ff-head);font-size:.95rem;font-weight:500;color:var(--ink);margin-bottom:3px}
.history-card-sub{font-size:.72rem;color:var(--ink3);margin-bottom:14px}
canvas.history-chart{display:block;width:100%;border-radius:6px}
.trend-indicators{display:grid;grid-template-columns:repeat(3,1fr);gap:9px;margin-top:12px}
.trend-item{padding:11px;background:var(--cream);border-radius:var(--r2);text-align:center}
.trend-val{font-family:var(--ff-head);font-size:1.25rem;font-weight:500;color:var(--ink);margin-bottom:2px}
.trend-lbl{font-size:.65rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em}
.pattern-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
.pattern-card{padding:12px;border-radius:var(--r2);border:1px solid var(--border)}
.pattern-card-title{font-size:.76rem;font-weight:600;color:var(--ink);margin-bottom:3px}
.pattern-card-body{font-size:.7rem;color:var(--ink3);line-height:1.5}
.daily-summary{display:flex;flex-direction:column;gap:7px}
.day-row{display:flex;align-items:center;gap:10px;padding:9px 12px;background:var(--cream);border-radius:var(--r2)}
.day-label{font-size:.78rem;font-weight:600;color:var(--ink);width:80px;flex-shrink:0}
.day-bar-track{flex:1;height:8px;border-radius:4px;background:var(--cream2);overflow:hidden}
.day-bar-fill{height:100%;border-radius:4px;transition:width 1s ease}
.day-score{font-size:.76rem;font-weight:700;width:32px;text-align:right;flex-shrink:0}
.day-events{font-size:.68rem;color:var(--ink3);width:80px;text-align:right;flex-shrink:0}

/* ═══ SETTINGS PAGE ═══ */
.settings-body{padding:22px 30px 40px;display:grid;grid-template-columns:300px 1fr;gap:20px;align-items:start}
.settings-nav{display:flex;flex-direction:column;gap:4px}
.settings-nav-item{padding:10px 14px;border-radius:var(--r2);font-size:.82rem;font-weight:500;cursor:pointer;border:none;background:none;text-align:left;color:var(--ink2);transition:all .15s;font-family:var(--ff-body);display:flex;align-items:center;gap:8px}
.settings-nav-item:hover{background:var(--cream2);color:var(--ink)}
.settings-nav-item.active{background:var(--teal-lt);color:var(--teal);font-weight:600}
.settings-content{display:flex;flex-direction:column;gap:16px}
.settings-card{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:22px}
.settings-card-title{font-family:var(--ff-head);font-size:1.05rem;font-weight:500;color:var(--ink);margin-bottom:4px}
.settings-card-sub{font-size:.75rem;color:var(--ink3);margin-bottom:18px;line-height:1.5}
.settings-section{display:none}
.settings-section.active{display:block}
.form-group{margin-bottom:16px}
.form-label{font-size:.72rem;font-weight:600;color:var(--ink2);text-transform:uppercase;letter-spacing:.05em;margin-bottom:6px;display:flex;justify-content:space-between;align-items:center}
.form-input{width:100%;padding:9px 13px;border-radius:var(--r2);border:1.5px solid var(--border2);font-family:var(--ff-body);font-size:.85rem;color:var(--ink);background:#fff;transition:border-color .15s}
.form-input:focus{outline:none;border-color:var(--teal)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.form-select{width:100%;padding:9px 13px;border-radius:var(--r2);border:1.5px solid var(--border2);font-family:var(--ff-body);font-size:.85rem;color:var(--ink);background:#fff;cursor:pointer}
.form-select:focus{outline:none;border-color:var(--teal)}

/* Sensor status cards */
.sensor-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-bottom:18px}
.sensor-card{border-radius:var(--r2);border:1.5px solid var(--border);padding:14px;display:flex;align-items:flex-start;gap:10px;transition:all .2s;cursor:pointer}
.sensor-card:hover{border-color:var(--teal);box-shadow:var(--shadow)}
.sensor-card.connected{border-color:var(--teal);background:var(--teal-lt)}
.sensor-card.error{border-color:var(--red);background:var(--red-lt)}
.sensor-card.searching{border-color:var(--amber);background:var(--amber-lt)}
.sensor-icon{font-size:1.4rem;flex-shrink:0}
.sensor-name{font-size:.82rem;font-weight:600;color:var(--ink);margin-bottom:2px}
.sensor-desc{font-size:.7rem;color:var(--ink3)}
.sensor-status{font-size:.68rem;font-weight:700;margin-top:6px;display:inline-flex;align-items:center;gap:4px}
.sensor-status.ok{color:var(--teal)}
.sensor-status.err{color:var(--red)}
.sensor-status.search{color:var(--amber)}
.sensor-dot{width:6px;height:6px;border-radius:50%;display:inline-block}

/* Toggle switch */
.toggle-row{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border)}
.toggle-row:last-child{border-bottom:none}
.toggle-label{font-size:.82rem;color:var(--ink2);font-weight:500}
.toggle-desc{font-size:.7rem;color:var(--ink3);margin-top:2px}
.toggle{position:relative;width:40px;height:22px;flex-shrink:0}
.toggle input{opacity:0;width:0;height:0}
.slider{position:absolute;cursor:pointer;top:0;left:0;right:0;bottom:0;background:var(--cream3);border-radius:22px;transition:.3s}
.slider:before{content:'';position:absolute;height:16px;width:16px;left:3px;bottom:3px;background:#fff;border-radius:50%;transition:.3s;box-shadow:0 1px 3px rgba(0,0,0,.2)}
input:checked+.slider{background:var(--teal)}
input:checked+.slider:before{transform:translateX(18px)}

/* Range slider */
.range-row{display:flex;align-items:center;gap:12px}
.range-slider{-webkit-appearance:none;flex:1;height:5px;border-radius:3px;background:var(--cream2);outline:none}
.range-slider::-webkit-slider-thumb{-webkit-appearance:none;width:18px;height:18px;border-radius:50%;background:var(--teal);cursor:pointer;box-shadow:0 1px 4px rgba(0,0,0,.2)}
.range-val{font-size:.82rem;font-weight:600;color:var(--teal);width:50px;text-align:right}

/* Connection panel */
.conn-input-row{display:flex;gap:8px;align-items:flex-end}
.conn-status-bar{padding:10px 14px;border-radius:var(--r2);background:var(--cream);font-size:.78rem;color:var(--ink3);display:flex;align-items:center;gap:8px;margin-top:10px}
.protocol-tabs{display:flex;gap:4px;margin-bottom:16px}
.proto-tab{padding:6px 14px;border-radius:var(--r2);font-size:.76rem;font-weight:600;cursor:pointer;border:1.5px solid var(--border);background:#fff;color:var(--ink3);transition:all .15s}
.proto-tab.active{border-color:var(--teal);background:var(--teal-lt);color:var(--teal)}

/* ═══ PROFILE PAGE ═══ */
.profile-body{padding:22px 30px 40px;display:grid;grid-template-columns:300px 1fr;gap:20px;align-items:start}
.profile-card{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:26px;text-align:center}
.profile-avatar-lg{width:80px;height:80px;border-radius:50%;background:var(--teal);display:flex;align-items:center;justify-content:center;font-family:var(--ff-head);font-size:1.9rem;font-weight:700;color:#fff;margin:0 auto 14px;cursor:pointer;transition:opacity .2s}
.profile-avatar-lg:hover{opacity:.85}
.profile-name{font-family:var(--ff-head);font-size:1.45rem;font-weight:500;color:var(--ink);margin-bottom:3px}
.profile-id{font-size:.7rem;color:var(--ink3);margin-bottom:18px}
.profile-stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-top:14px}
.profile-stat{padding:9px;background:var(--cream);border-radius:var(--r2);text-align:left}
.profile-stat-val{font-family:var(--ff-head);font-size:1.05rem;font-weight:500;color:var(--ink);margin-bottom:1px}
.profile-stat-lbl{font-size:.62rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em}
.profile-right{display:flex;flex-direction:column;gap:14px}
.info-section{background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:20px 22px}
.info-section-title{font-family:var(--ff-head);font-size:.95rem;font-weight:500;color:var(--ink);margin-bottom:12px;padding-bottom:9px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
.info-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.info-item{display:flex;flex-direction:column;gap:2px}
.info-label{font-size:.65rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em}
.info-value{font-size:.85rem;font-weight:500;color:var(--ink)}
.baseline-bars{display:flex;flex-direction:column;gap:9px}
.baseline-row{display:flex;align-items:center;gap:9px}
.baseline-sig-name{font-size:.72rem;color:var(--ink2);width:120px;flex-shrink:0;font-weight:500}
.baseline-track{flex:1;height:6px;background:var(--cream2);border-radius:3px;overflow:hidden}
.baseline-fill{height:100%;border-radius:3px}
.baseline-val{font-size:.7rem;font-weight:600;color:var(--ink2);width:70px;text-align:right;flex-shrink:0;font-family:var(--ff-head)}

/* Edit modal */
.modal-overlay{position:fixed;inset:0;background:rgba(26,20,16,.5);z-index:200;display:none;align-items:center;justify-content:center;backdrop-filter:blur(4px)}
.modal-overlay.show{display:flex}
.modal{background:#fff;border-radius:var(--r);box-shadow:var(--shadow-lg);padding:28px;width:560px;max-width:95vw;max-height:90vh;overflow-y:auto;animation:fadein .25s ease}
.modal-title{font-family:var(--ff-head);font-size:1.3rem;font-weight:500;color:var(--ink);margin-bottom:4px}
.modal-sub{font-size:.78rem;color:var(--ink3);margin-bottom:22px}
.modal-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:22px;padding-top:16px;border-top:1px solid var(--border)}

/* ═══ TOAST ═══ */
.toast{position:fixed;top:18px;right:18px;z-index:1000;background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow-lg);padding:13px 16px;max-width:310px;display:flex;gap:11px;align-items:flex-start;transform:translateX(360px);transition:transform .3s cubic-bezier(0.34,1.56,0.64,1)}
.toast.show{transform:translateX(0)}
.toast-icon{font-size:1.1rem;flex-shrink:0;margin-top:1px}
.toast-title{font-size:.8rem;font-weight:700;color:var(--ink);margin-bottom:2px}
.toast-msg{font-size:.72rem;color:var(--ink3);line-height:1.4}
.toast-close{margin-left:auto;flex-shrink:0;background:none;border:none;cursor:pointer;color:var(--ink3);font-size:.95rem;padding:0}

/* Misc */
.divider{height:1px;background:var(--border);margin:4px 0}
.empty-state{text-align:center;padding:38px;color:var(--ink3);font-size:.82rem}
.empty-state-icon{font-size:2.4rem;margin-bottom:11px;opacity:.5}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--cream3);border-radius:3px}
@keyframes fadein{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.fadein{animation:fadein .35s ease both}
@keyframes pulse-border{0%,100%{border-color:rgba(196,107,232,.3)}50%{border-color:rgba(196,107,232,.9)}}
.waveform-bar{display:inline-block;width:3px;border-radius:2px;background:#c46be8;margin:0 1px;transition:height .1s ease;transform-origin:bottom center}

@media(max-width:1200px){.signal-grid{grid-template-columns:repeat(3,1fr)}}
@media(max-width:1000px){.signal-grid{grid-template-columns:repeat(2,1fr)}.monitor-body{grid-template-columns:1fr 270px}}
@media(max-width:820px){.nav{width:60px}.nav-brand-name,.nav-brand-sub,.nav-patient,.nav-link span:not(.icon),.live-chip span,.mic-chip span,.nav-section-label{display:none}.nav-link{justify-content:center;padding:11px}.monitor-body{grid-template-columns:1fr;padding:16px}.monitor-right{display:none}.signal-grid{grid-template-columns:repeat(2,1fr)}.page-header{padding:18px 16px 0}.settings-body,.profile-body{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="app-shell">

<!-- ═══ NAV ═══ -->
<nav class="nav">
  <div class="nav-brand">
    <div class="nav-brand-name">PulseIQ <span style="font-size:.7rem;color:var(--teal2);font-family:var(--ff-body);font-weight:600">PRO</span></div>
    <div class="nav-brand-sub">Health Intelligence</div>
  </div>
  <div class="nav-patient" onclick="openEditModal()">
    <div class="nav-avatar" id="nav-avatar">AK</div>
    <div>
      <div class="nav-patient-name" id="nav-name">Alex Kumar</div>
      <div class="nav-patient-id" id="nav-pid">PHM-2841 · Edit ✏️</div>
    </div>
  </div>
  <div class="nav-links">
    <div class="nav-section-label">Monitoring</div>
    <button class="nav-link active" onclick="showPage('monitor',this)"><span class="icon">💓</span><span>Live Monitor</span></button>
    <button class="nav-link" onclick="showPage('alerts',this)"><span class="icon">🔔</span><span>Alerts</span><span class="nav-badge" id="alert-nav-badge">0</span></button>
    <button class="nav-link" onclick="showPage('history',this)"><span class="icon">📈</span><span>History</span></button>
    <div class="nav-section-label">Tools</div>
    <button class="nav-link" onclick="showPage('mic',this)"><span class="icon">🎙️</span><span>Behaviour AI</span></button>
    <button class="nav-link" onclick="showPage('wellness',this)"><span class="icon">🏃</span><span>Wellness</span></button>
    <div class="nav-section-label">Account</div>
    <button class="nav-link" onclick="showPage('profile',this)"><span class="icon">👤</span><span>My Profile</span></button>
    <button class="nav-link" onclick="showPage('settings',this)"><span class="icon">⚙️</span><span>Settings</span></button>
  </div>
  <div class="nav-footer">
    <div class="live-chip" id="sensor-chip"><div class="live-dot"></div><span id="sensor-chip-text">Sensors active</span></div>
    <div class="mic-chip" id="nav-mic-btn" onclick="toggleMicFromNav()"><div class="mic-dot" id="nav-mic-dot" style="animation:none"></div><span id="nav-mic-text">Mic off</span></div>
  </div>
</nav>

<div class="main-content">

<!-- ═══════════ PAGE: LIVE MONITOR ═══════════ -->
<div class="page active" id="page-monitor">
  <div class="page-header">
    <div>
      <div class="page-title">Live Monitor</div>
      <div class="page-subtitle" id="monitor-time">Updating now — 10 Hz sampling</div>
    </div>
    <div class="page-actions">
      <button class="btn btn-ghost btn-sm" onclick="togglePause()" id="pause-btn">⏸ Pause</button>
      <button class="btn btn-primary btn-sm" onclick="resetAll()">↺ Reset</button>
    </div>
  </div>

  <div class="monitor-body">
    <!-- HRI Hero -->
    <div class="hri-hero fadein">
      <div class="hri-gauge-box">
        <canvas id="hri-canvas" width="160" height="160" style="display:block"></canvas>
        <div class="hri-score-num" id="hri-num">0</div>
        <div class="hri-score-label">HRI SCORE</div>
      </div>
      <div class="hri-hero-info">
        <div class="hri-status-badge" id="hri-badge">● Normal</div>
        <div class="hri-hero-title" id="hri-title">All signals within your personal baseline</div>
        <div class="hri-hero-desc" id="hri-desc">Your multi-signal correlation patterns are stable.</div>
        <div class="hri-meta">
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-maha">0.0</span><span class="hri-meta-lbl">Deviation Score</span></div>
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-lstm">0.0</span><span class="hri-meta-lbl">Pattern Score</span></div>
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-samples">0</span><span class="hri-meta-lbl">Samples</span></div>
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-uptime">0s</span><span class="hri-meta-lbl">Session</span></div>
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-steps" style="color:var(--teal)">0</span><span class="hri-meta-lbl">Steps Today</span></div>
          <div class="hri-meta-item"><span class="hri-meta-val" id="meta-fever" style="color:var(--amber)">36.8°</span><span class="hri-meta-lbl">Body Temp</span></div>
        </div>
      </div>
    </div>

    <!-- Signal Cards -->
    <div class="signal-grid" id="signal-grid"></div>

    <!-- Right column -->
    <div class="monitor-right">
      <div class="alert-banner" id="active-alert-banner">
        <div class="alert-banner-top">
          <span class="alert-banner-icon" id="ab-icon">⚠️</span>
          <span class="alert-banner-level" id="ab-level">Elevated</span>
          <span class="alert-banner-time" id="ab-time"></span>
        </div>
        <div class="alert-banner-msg" id="ab-msg">Alert message here</div>
        <div class="alert-banner-signals" id="ab-signals"></div>
      </div>
      <!-- Correlation -->
      <div class="widget">
        <div class="widget-title">Signal Correlations <span style="font-size:.58rem;font-weight:400;color:var(--ink3)">Pearson r</span></div>
        <div class="corr-heatmap" id="corr-heatmap"></div>
        <div class="corr-col-labels" id="corr-col-labels" style="display:grid;gap:3px;margin-top:3px"></div>
      </div>
      <!-- Scenarios -->
      <div class="widget">
        <div class="widget-title">Demo Scenarios</div>
        <div class="scenario-btns">
          <button class="scenario-btn full active" onclick="setScenario('normal',this)">✓ Normal</button>
          <button class="scenario-btn" onclick="setScenario('cardiac',this)">❤️ Cardiac</button>
          <button class="scenario-btn" onclick="setScenario('hypoxia',this)">🫁 Hypoxia</button>
          <button class="scenario-btn" onclick="setScenario('infection',this)">🦠 Infection</button>
          <button class="scenario-btn" onclick="setScenario('fever',this)">🌡️ High Fever</button>
          <button class="scenario-btn" onclick="setScenario('overexertion',this)">⚡ Overexertion</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: ALERTS ═══════════ -->
<div class="page" id="page-alerts">
  <div class="page-header">
    <div><div class="page-title">Alerts</div><div class="page-subtitle">Your health event log and notifications</div></div>
    <div class="page-actions"><button class="btn btn-ghost btn-sm" onclick="clearAlerts()">Clear All</button></div>
  </div>
  <div class="alerts-body fadein">
    <div class="alert-stats-row">
      <div class="stat-card"><div class="stat-card-val" id="astat-total">0</div><div class="stat-card-lbl">Total Alerts</div></div>
      <div class="stat-card"><div class="stat-card-val" id="astat-critical" style="color:var(--red)">0</div><div class="stat-card-lbl">Critical / Emergency</div></div>
      <div class="stat-card"><div class="stat-card-val" id="astat-high" style="color:var(--amber)">0</div><div class="stat-card-lbl">High Risk</div></div>
      <div class="stat-card"><div class="stat-card-val" id="astat-resolved" style="color:var(--green)">0</div><div class="stat-card-lbl">Resolved</div></div>
    </div>
    <div class="alert-filter-row">
      <span style="font-size:.73rem;color:var(--ink3);font-weight:600">Filter:</span>
      <button class="filter-chip active" onclick="filterAlerts('all',this)">All</button>
      <button class="filter-chip" onclick="filterAlerts('emergency',this)">Emergency</button>
      <button class="filter-chip" onclick="filterAlerts('critical',this)">Critical</button>
      <button class="filter-chip" onclick="filterAlerts('high',this)">High</button>
      <button class="filter-chip" onclick="filterAlerts('elevated',this)">Elevated</button>
      <button class="filter-chip" onclick="filterAlerts('fever',this)">🌡️ Fever</button>
      <button class="filter-chip" onclick="filterAlerts('behaviour',this)">🎙️ Behaviour</button>
    </div>
    <div class="alert-list" id="alert-list">
      <div class="empty-state"><div class="empty-state-icon">🔔</div>No alerts yet.</div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: HISTORY ═══════════ -->
<div class="page" id="page-history">
  <div class="page-header">
    <div><div class="page-title">History & Analytics</div><div class="page-subtitle">Your health patterns over time</div></div>
    <div class="page-actions">
      <div class="history-tabs">
        <button class="history-tab active" onclick="setHistoryTab('7d',this)">7 Days</button>
        <button class="history-tab" onclick="setHistoryTab('30d',this)">30 Days</button>
        <button class="history-tab" onclick="setHistoryTab('90d',this)">3 Months</button>
      </div>
    </div>
  </div>
  <div class="history-body fadein">
    <div class="history-grid">
      <div class="history-card history-card-full">
        <div class="history-card-title">Health Risk Index — Trend</div>
        <div class="history-card-sub">Daily average HRI with risk band overlay</div>
        <canvas class="history-chart" id="hri-trend-chart" height="120"></canvas>
        <div class="trend-indicators">
          <div class="trend-item"><div class="trend-val" id="tr-avg" style="color:var(--teal)">—</div><div class="trend-lbl">Avg HRI</div></div>
          <div class="trend-item"><div class="trend-val" id="tr-peak" style="color:var(--red)">—</div><div class="trend-lbl">Peak HRI</div></div>
          <div class="trend-item"><div class="trend-val" id="tr-events" style="color:var(--amber)">—</div><div class="trend-lbl">Alert Events</div></div>
        </div>
      </div>
      <div class="history-card">
        <div class="history-card-title">Signal Averages</div>
        <div class="history-card-sub">7-day mean vs. your personal baseline</div>
        <canvas class="history-chart" id="sig-avg-chart" height="160"></canvas>
      </div>
      <div class="history-card">
        <div class="history-card-title">Fever & Temperature</div>
        <div class="history-card-sub">Body temperature trend with fever threshold</div>
        <canvas class="history-chart" id="temp-trend-chart" height="160"></canvas>
      </div>
      <div class="history-card">
        <div class="history-card-title">Daily Steps</div>
        <div class="history-card-sub">Step count vs. goal (10,000 steps)</div>
        <canvas class="history-chart" id="steps-chart" height="160"></canvas>
      </div>
      <div class="history-card">
        <div class="history-card-title">AI Pattern Insights</div>
        <div class="history-card-sub">Detected correlation patterns this week</div>
        <div class="pattern-grid" id="pattern-grid"></div>
      </div>
      <div class="history-card history-card-full">
        <div class="history-card-title">Daily Summary</div>
        <div class="history-card-sub">HRI score and events per day</div>
        <div class="daily-summary" id="daily-summary"></div>
      </div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: BEHAVIOUR AI (MIC) ═══════════ -->
<div class="page" id="page-mic">
  <div class="page-header">
    <div>
      <div class="page-title">Behaviour AI</div>
      <div class="page-subtitle">Real-time microphone analysis for health behaviour detection</div>
    </div>
    <div class="page-actions">
      <button class="btn btn-purple btn-sm" id="mic-main-btn" onclick="toggleMic()">🎙️ Start Listening</button>
    </div>
  </div>
  <div style="padding:22px 30px 40px;display:grid;grid-template-columns:1fr 1fr;gap:20px">
    <!-- Live analysis panel -->
    <div style="display:flex;flex-direction:column;gap:16px">
      <div class="settings-card">
        <div class="settings-card-title">Live Audio Analysis</div>
        <div class="settings-card-sub">AI listens for behavioural patterns including smoking, coughing, drinking, and stress indicators</div>
        <div style="background:#1A1028;border-radius:var(--r2);padding:16px;margin-bottom:14px">
          <div style="font-size:.68rem;color:#c46be8;font-weight:600;text-transform:uppercase;letter-spacing:.06em;margin-bottom:8px;display:flex;align-items:center;gap:6px">
            <div class="live-dot" id="mic-vis-dot" style="background:#c46be8;box-shadow:0 0 6px #c46be8;animation:none"></div>
            Audio Waveform
          </div>
          <canvas id="mic-waveform" style="width:100%;height:60px;display:block;border-radius:6px"></canvas>
        </div>
        <div style="display:flex;flex-direction:column;gap:8px" id="behaviour-detections">
          <!-- Populated by JS -->
        </div>
        <div style="margin-top:14px;padding:12px;background:var(--cream);border-radius:var(--r2)">
          <div style="font-size:.7rem;color:var(--ink3);font-weight:600;margin-bottom:6px">🤖 AI Interpretation</div>
          <div style="font-size:.82rem;color:var(--ink2);line-height:1.6" id="mic-ai-text">Start listening to receive real-time behavioural analysis.</div>
        </div>
      </div>
      <!-- Session stats -->
      <div class="settings-card">
        <div class="settings-card-title">Session Statistics</div>
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:4px">
          <div style="text-align:center;padding:12px;background:var(--cream);border-radius:var(--r2)">
            <div style="font-family:var(--ff-head);font-size:1.5rem;font-weight:500;color:var(--purple)" id="mic-detections-count">0</div>
            <div style="font-size:.64rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em">Detections</div>
          </div>
          <div style="text-align:center;padding:12px;background:var(--cream);border-radius:var(--r2)">
            <div style="font-family:var(--ff-head);font-size:1.5rem;font-weight:500;color:var(--red)" id="mic-cough-count">0</div>
            <div style="font-size:.64rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em">Coughs</div>
          </div>
          <div style="text-align:center;padding:12px;background:var(--cream);border-radius:var(--r2)">
            <div style="font-family:var(--ff-head);font-size:1.5rem;font-weight:500;color:var(--amber)" id="mic-session-time">0m</div>
            <div style="font-size:.64rem;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em">Session</div>
          </div>
        </div>
      </div>
    </div>
    <!-- Detection log -->
    <div class="settings-card">
      <div class="settings-card-title">Detection Log</div>
      <div class="settings-card-sub">All detected behavioural events with timestamps</div>
      <div style="display:flex;flex-direction:column;gap:7px;max-height:480px;overflow-y:auto" id="mic-log">
        <div class="empty-state" style="padding:24px"><div class="empty-state-icon">🎙️</div>No events detected yet.</div>
      </div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: WELLNESS / STEPS / FEVER ═══════════ -->
<div class="page" id="page-wellness">
  <div class="page-header">
    <div><div class="page-title">Wellness</div><div class="page-subtitle">Activity, fever monitoring, and health goals</div></div>
    <div class="page-actions">
      <button class="btn btn-ghost btn-sm" onclick="addSteps()">+ Add Steps</button>
    </div>
  </div>
  <div style="padding:22px 30px 40px;display:grid;grid-template-columns:1fr 1fr 1fr;gap:18px">
    <!-- Step counter card -->
    <div class="settings-card" style="grid-column:1/-1">
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:16px;align-items:center">
        <div>
          <div style="font-size:.7rem;font-weight:600;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px">Today's Steps</div>
          <div class="steps-val" id="wellness-steps">0</div>
          <div class="steps-goal" id="wellness-steps-goal">Goal: 10,000 · 0%</div>
          <div class="steps-badges" id="steps-badges"></div>
        </div>
        <div style="grid-column:2/4">
          <div style="font-size:.68rem;color:var(--ink3);font-weight:600;margin-bottom:6px">Progress</div>
          <div style="height:14px;background:var(--cream2);border-radius:7px;overflow:hidden;margin-bottom:6px">
            <div id="steps-progress-bar" style="height:100%;border-radius:7px;background:linear-gradient(90deg,var(--teal),var(--teal2));transition:width .5s ease;width:0%"></div>
          </div>
          <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px">
            <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
              <div style="font-family:var(--ff-head);font-size:1rem;color:var(--teal)" id="ws-calories">0</div>
              <div style="font-size:.62rem;color:var(--ink3)">Calories</div>
            </div>
            <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
              <div style="font-family:var(--ff-head);font-size:1rem;color:var(--blue)" id="ws-distance">0.0</div>
              <div style="font-size:.62rem;color:var(--ink3)">km</div>
            </div>
            <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
              <div style="font-family:var(--ff-head);font-size:1rem;color:var(--amber)" id="ws-active">0</div>
              <div style="font-size:.62rem;color:var(--ink3)">Active min</div>
            </div>
            <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
              <div style="font-family:var(--ff-head);font-size:1rem;color:var(--purple)" id="ws-floors">0</div>
              <div style="font-size:.62rem;color:var(--ink3)">Floors</div>
            </div>
          </div>
        </div>
        <div style="text-align:center">
          <canvas id="steps-donut" width="120" height="120" style="display:block;margin:0 auto"></canvas>
        </div>
      </div>
    </div>

    <!-- Fever / Body temp card -->
    <div class="settings-card" style="grid-column:1/3">
      <div class="settings-card-title">🌡️ Fever Monitor</div>
      <div class="settings-card-sub">Real-time body temperature with clinical zone classification</div>
      <div style="display:flex;align-items:center;gap:20px;margin-bottom:16px">
        <div>
          <div style="font-family:var(--ff-head);font-size:3.5rem;font-weight:500;line-height:1" id="fever-big-val">36.8</div>
          <div style="font-size:.85rem;color:var(--ink3)">°C body temperature</div>
          <div class="fever-status" id="fever-status-badge" style="background:var(--green-lt);color:var(--green)">✓ Normal</div>
        </div>
        <div style="flex:1">
          <div style="font-size:.68rem;font-weight:600;color:var(--ink3);text-transform:uppercase;letter-spacing:.05em;margin-bottom:8px">Temperature Zone</div>
          <div class="fever-zones">
            <div class="fever-zone" style="background:#1A7B4A;flex:1" title="Hypothermic <36°C"></div>
            <div class="fever-zone" style="background:#0A7B6C;flex:1.5" title="Sub-normal 36-36.5°C"></div>
            <div class="fever-zone" style="background:#2196F3;flex:2" title="Normal 36.5-37.5°C"></div>
            <div class="fever-zone" style="background:#C97B1A;flex:1.5" title="Low-grade 37.5-38°C"></div>
            <div class="fever-zone" style="background:#E67E22;flex:1.5" title="Fever 38-39°C"></div>
            <div class="fever-zone" style="background:#C0392B;flex:1" title="High Fever 39-40°C"></div>
            <div class="fever-zone" style="background:#8B0000;flex:0.5" title="Hyperpyrexia >40°C"></div>
          </div>
          <div class="fever-labels">
            <span>&lt;36</span><span>36.5</span><span>37</span><span>37.5</span><span>38</span><span>39</span><span>40+</span>
          </div>
          <!-- Arrow indicator -->
          <div style="position:relative;height:14px;margin-top:2px">
            <div id="fever-arrow" style="position:absolute;top:0;font-size:.8rem;transition:left .5s ease">🔺</div>
          </div>
        </div>
      </div>
      <!-- Temp history mini chart -->
      <canvas id="fever-mini-chart" style="width:100%;height:60px;display:block" height="60"></canvas>
      <!-- Stats row -->
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-top:14px">
        <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
          <div style="font-family:var(--ff-head);font-size:1rem;color:var(--blue)" id="temp-min">36.6</div>
          <div style="font-size:.62rem;color:var(--ink3)">Today Min</div>
        </div>
        <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
          <div style="font-family:var(--ff-head);font-size:1rem;color:var(--red)" id="temp-max">36.9</div>
          <div style="font-size:.62rem;color:var(--ink3)">Today Max</div>
        </div>
        <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
          <div style="font-family:var(--ff-head);font-size:1rem;color:var(--ink)" id="temp-avg">36.8</div>
          <div style="font-size:.62rem;color:var(--ink3)">Average</div>
        </div>
        <div style="text-align:center;padding:8px;background:var(--cream);border-radius:8px">
          <div style="font-family:var(--ff-head);font-size:1rem;color:var(--amber)" id="temp-trend-val">Stable</div>
          <div style="font-size:.62rem;color:var(--ink3)">Trend</div>
        </div>
      </div>
    </div>

    <!-- Goals card -->
    <div class="settings-card">
      <div class="settings-card-title">Daily Goals</div>
      <div style="display:flex;flex-direction:column;gap:12px;margin-top:8px">
        <div>
          <div style="display:flex;justify-content:space-between;font-size:.78rem;margin-bottom:5px"><span style="font-weight:600">👣 Steps</span><span id="g-steps">0 / 10,000</span></div>
          <div style="height:8px;background:var(--cream2);border-radius:4px;overflow:hidden"><div id="gbar-steps" style="height:100%;background:var(--teal);border-radius:4px;transition:width .5s;width:0%"></div></div>
        </div>
        <div>
          <div style="display:flex;justify-content:space-between;font-size:.78rem;margin-bottom:5px"><span style="font-weight:600">💧 Water (glasses)</span><span id="g-water">0 / 8</span></div>
          <div style="height:8px;background:var(--cream2);border-radius:4px;overflow:hidden"><div id="gbar-water" style="height:100%;background:var(--blue);border-radius:4px;transition:width .5s;width:0%"></div></div>
        </div>
        <div>
          <div style="display:flex;justify-content:space-between;font-size:.78rem;margin-bottom:5px"><span style="font-weight:600">🔥 Calories</span><span id="g-calories">0 / 2200</span></div>
          <div style="height:8px;background:var(--cream2);border-radius:4px;overflow:hidden"><div id="gbar-calories" style="height:100%;background:var(--orange);border-radius:4px;transition:width .5s;width:0%"></div></div>
        </div>
        <div>
          <div style="display:flex;justify-content:space-between;font-size:.78rem;margin-bottom:5px"><span style="font-weight:600">😴 Sleep (hrs)</span><span id="g-sleep">7.5 / 8</span></div>
          <div style="height:8px;background:var(--cream2);border-radius:4px;overflow:hidden"><div id="gbar-sleep" style="height:100%;background:var(--purple);border-radius:4px;transition:width .5s;width:93.75%"></div></div>
        </div>
        <div style="border-top:1px solid var(--border);padding-top:12px;display:flex;flex-direction:column;gap:6px">
          <button class="btn btn-primary btn-sm" style="width:100%;justify-content:center" onclick="addWater()">💧 + Glass of Water</button>
          <button class="btn btn-ghost btn-sm" style="width:100%;justify-content:center" onclick="addSteps()">👣 + Log Steps</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: PROFILE ═══════════ -->
<div class="page" id="page-profile">
  <div class="page-header">
    <div><div class="page-title">My Profile</div><div class="page-subtitle">Personal details and physiological baseline</div></div>
    <div class="page-actions"><button class="btn btn-primary btn-sm" onclick="openEditModal()">✏️ Edit Profile</button></div>
  </div>
  <div class="profile-body fadein">
    <div class="profile-card">
      <div class="profile-avatar-lg" id="profile-avatar-lg" onclick="openEditModal()">AK</div>
      <div class="profile-name" id="profile-name">Alex Kumar</div>
      <div class="profile-id" id="profile-id">Patient ID: PHM-2841 · Joined Jan 2024</div>
      <div class="divider"></div>
      <div style="text-align:left;display:flex;flex-direction:column;gap:7px;margin-top:8px">
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Age</span><span style="font-weight:600" id="p-age">34 years</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Gender</span><span style="font-weight:600" id="p-gender">Male</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Height</span><span style="font-weight:600" id="p-height">175 cm</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Weight</span><span style="font-weight:600" id="p-weight">72 kg</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">BMI</span><span style="font-weight:600" id="p-bmi">23.5</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Blood Type</span><span style="font-weight:600" id="p-blood">A+</span></div>
        <div style="display:flex;justify-content:space-between;font-size:.8rem"><span style="color:var(--ink3)">Device</span><span style="font-weight:600">ESP32 v2.1</span></div>
      </div>
      <div class="profile-stats-grid">
        <div class="profile-stat"><div class="profile-stat-val" id="ps-days">14</div><div class="profile-stat-lbl">Days Active</div></div>
        <div class="profile-stat"><div class="profile-stat-val" id="ps-alerts">0</div><div class="profile-stat-lbl">Alerts Total</div></div>
        <div class="profile-stat"><div class="profile-stat-val" style="color:var(--teal)">98.5%</div><div class="profile-stat-lbl">Baseline Fit</div></div>
        <div class="profile-stat"><div class="profile-stat-val" style="color:var(--green)">Good</div><div class="profile-stat-lbl">Status</div></div>
      </div>
    </div>
    <div class="profile-right">
      <div class="info-section">
        <div class="info-section-title">Medical Information <button class="btn btn-ghost btn-sm" onclick="openEditModal('medical')">Edit</button></div>
        <div class="info-grid">
          <div class="info-item"><span class="info-label">Conditions</span><span class="info-value" id="p-conditions">None listed</span></div>
          <div class="info-item"><span class="info-label">Medications</span><span class="info-value" id="p-medications">None listed</span></div>
          <div class="info-item"><span class="info-label">Allergies</span><span class="info-value" id="p-allergies">Penicillin</span></div>
          <div class="info-item"><span class="info-label">Emergency Contact</span><span class="info-value" id="p-emergency">+91 98765 43210</span></div>
          <div class="info-item"><span class="info-label">Physician</span><span class="info-value" id="p-physician">Dr. R. Sharma</span></div>
          <div class="info-item"><span class="info-label">Last Check-up</span><span class="info-value" id="p-checkup">Nov 2024</span></div>
        </div>
      </div>
      <div class="info-section">
        <div class="info-section-title">Personal Physiological Baseline</div>
        <p style="font-size:.75rem;color:var(--ink3);margin-bottom:12px;line-height:1.5">Learned from your first 14 days of monitoring. Used to calculate your personalized HRI.</p>
        <div class="baseline-bars" id="baseline-bars"></div>
      </div>
      <div class="info-section">
        <div class="info-section-title">Wearable Device</div>
        <div class="info-grid">
          <div class="info-item"><span class="info-label">Hardware</span><span class="info-value">ESP32 WROOM-32</span></div>
          <div class="info-item"><span class="info-label">Firmware</span><span class="info-value">v2.1.4</span></div>
          <div class="info-item"><span class="info-label">Sample Rate</span><span class="info-value">10 Hz</span></div>
          <div class="info-item"><span class="info-label">Battery</span><span class="info-value" id="p-battery">87% (Est. 9hr)</span></div>
          <div class="info-item"><span class="info-label">Sensors</span><span class="info-value">MAX30105, AD8232, DS18B20, GSR, MPU6050</span></div>
          <div class="info-item"><span class="info-label">Protocol</span><span class="info-value" id="p-protocol">BLE 5.0 + MQTT</span></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ═══════════ PAGE: SETTINGS ═══════════ -->
<div class="page" id="page-settings">
  <div class="page-header">
    <div><div class="page-title">Settings</div><div class="page-subtitle">Sensor connections, alerts, thresholds, and preferences</div></div>
  </div>
  <div class="settings-body fadein">
    <!-- Settings nav -->
    <div>
      <div style="background:#fff;border-radius:var(--r);border:1px solid var(--border);box-shadow:var(--shadow);padding:8px">
        <div class="settings-nav">
          <button class="settings-nav-item active" onclick="showSettingsSection('sensors',this)">📡 Sensor Connections</button>
          <button class="settings-nav-item" onclick="showSettingsSection('thresholds',this)">📊 Alert Thresholds</button>
          <button class="settings-nav-item" onclick="showSettingsSection('notifications',this)">🔔 Notifications</button>
          <button class="settings-nav-item" onclick="showSettingsSection('display',this)">🎨 Display & UI</button>
          <button class="settings-nav-item" onclick="showSettingsSection('data',this)">💾 Data & Privacy</button>
          <button class="settings-nav-item" onclick="showSettingsSection('about',this)">ℹ️ About</button>
        </div>
      </div>
    </div>
    <!-- Settings content -->
    <div class="settings-content">

      <!-- SENSORS -->
      <div class="settings-section active" id="ss-sensors">
        <div class="settings-card">
          <div class="settings-card-title">Sensor Connections</div>
          <div class="settings-card-sub">Manage and configure your wearable sensors. Click a sensor card to toggle its connection state.</div>
          <div class="sensor-grid" id="sensor-grid"></div>
          <div style="font-size:.78rem;font-weight:600;color:var(--ink2);margin-bottom:10px">Connection Protocol</div>
          <div class="protocol-tabs">
            <button class="proto-tab active" id="proto-ble" onclick="setProto('ble',this)">📶 BLE 5.0</button>
            <button class="proto-tab" id="proto-wifi" onclick="setProto('wifi',this)">📡 Wi-Fi MQTT</button>
            <button class="proto-tab" id="proto-usb" onclick="setProto('usb',this)">🔌 USB Serial</button>
            <button class="proto-tab" id="proto-demo" onclick="setProto('demo',this)">🧪 Demo Mode</button>
          </div>
          <div style="margin-top:12px">
            <div class="form-group">
              <div class="form-label">Device Address / Host</div>
              <div class="conn-input-row">
                <input class="form-input" id="conn-addr" placeholder="e.g. ESP32-PulseIQ or 192.168.1.100" style="flex:1">
                <button class="btn btn-primary btn-sm" onclick="simulateConnect()">Connect</button>
              </div>
            </div>
            <div class="conn-status-bar" id="conn-status">
              <div class="live-dot"></div>
              <span>Demo mode active — simulated sensor data streaming at 10 Hz</span>
            </div>
          </div>
        </div>
      </div>

      <!-- THRESHOLDS -->
      <div class="settings-section" id="ss-thresholds">
        <div class="settings-card">
          <div class="settings-card-title">Alert Thresholds</div>
          <div class="settings-card-sub">Customize alert trigger values for each vital sign. Changes take effect immediately.</div>
          <div id="threshold-settings"></div>
        </div>
      </div>

      <!-- NOTIFICATIONS -->
      <div class="settings-section" id="ss-notifications">
        <div class="settings-card">
          <div class="settings-card-title">Notification Settings</div>
          <div class="settings-card-sub">Control how and when PulseIQ notifies you about health events.</div>
          <div>
            <div class="toggle-row">
              <div><div class="toggle-label">Alert Sounds</div><div class="toggle-desc">Play audio for critical alerts</div></div>
              <label class="toggle"><input type="checkbox" checked id="notif-sound"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Browser Notifications</div><div class="toggle-desc">Show system notifications for high-risk events</div></div>
              <label class="toggle"><input type="checkbox" id="notif-browser"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Fever Alerts</div><div class="toggle-desc">Notify when temperature exceeds 37.8°C</div></div>
              <label class="toggle"><input type="checkbox" checked id="notif-fever"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Behaviour Detection Alerts</div><div class="toggle-desc">Alert when smoking or coughing is detected</div></div>
              <label class="toggle"><input type="checkbox" checked id="notif-behaviour"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Step Goal Reminder</div><div class="toggle-desc">Remind when 75% of daily goal not reached by 7pm</div></div>
              <label class="toggle"><input type="checkbox" checked id="notif-steps"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Daily Health Summary</div><div class="toggle-desc">Receive daily summary at 9pm</div></div>
              <label class="toggle"><input type="checkbox" id="notif-summary"><span class="slider"></span></label>
            </div>
          </div>
          <div class="form-group" style="margin-top:18px">
            <div class="form-label">Alert Cooldown (minutes) <span id="cooldown-val" style="color:var(--teal)">4 min</span></div>
            <div class="range-row">
              <input type="range" class="range-slider" min="1" max="30" value="4" id="cooldown-slider" oninput="document.getElementById('cooldown-val').textContent=this.value+' min'">
            </div>
          </div>
        </div>
      </div>

      <!-- DISPLAY -->
      <div class="settings-section" id="ss-display">
        <div class="settings-card">
          <div class="settings-card-title">Display & UI</div>
          <div class="settings-card-sub">Customize the appearance and layout of your dashboard.</div>
          <div>
            <div class="toggle-row">
              <div><div class="toggle-label">Mini Waveforms</div><div class="toggle-desc">Show sparkline charts on signal cards</div></div>
              <label class="toggle"><input type="checkbox" checked id="disp-mini"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Correlation Heatmap</div><div class="toggle-desc">Show real-time correlation matrix</div></div>
              <label class="toggle"><input type="checkbox" checked id="disp-corr"><span class="slider"></span></label>
            </div>
            <div class="toggle-row">
              <div><div class="toggle-label">Animated HRI Gauge</div><div class="toggle-desc">Animate the health risk gauge needle</div></div>
              <label class="toggle"><input type="checkbox" checked id="disp-gauge"><span class="slider"></span></label>
            </div>
          </div>
          <div class="form-group" style="margin-top:18px">
            <div class="form-label">Temperature Unit</div>
            <select class="form-select" id="temp-unit" onchange="updateTempUnit()">
              <option value="C">Celsius (°C)</option>
              <option value="F">Fahrenheit (°F)</option>
            </select>
          </div>
          <div class="form-group">
            <div class="form-label">Step Goal <span id="step-goal-val" style="color:var(--teal)">10,000</span></div>
            <div class="range-row">
              <input type="range" class="range-slider" min="2000" max="20000" step="500" value="10000" id="step-goal-slider" oninput="updateStepGoal(this.value)">
            </div>
          </div>
        </div>
      </div>

      <!-- DATA -->
      <div class="
