<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
<meta name="theme-color" content="#4A8C6F"/>
<title>Dompetku</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;500;600;700;800;900&display=swap" rel="stylesheet"/>
<style>
:root {
  --green:     #4A8C6F;
  --green-dk:  #3A7060;
  --green-lt:  #E8F5EE;
  --green-tab: rgba(255,255,255,0.25);
  --orange:    #F5A623;
  --orange-lt: #FEF6E4;
  --bg:        #F0F2F0;
  --card:      #FFFFFF;
  --border:    #E8EDE8;
  --text:      #1A1A1A;
  --text2:     #555;
  --sub:       #AAA;
  --red:       #E74C3C;
  --blue:      #3498DB;
  --font:      'Nunito', sans-serif;
  --safe-top:  env(safe-area-inset-top, 0px);
  --safe-bot:  env(safe-area-inset-bottom, 0px);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{min-height:100%;background:var(--bg);color:var(--text);font-family:var(--font);overscroll-behavior:none;}

/* ══════════════════════════════
   SCREENS
══════════════════════════════ */
.screen{display:none;flex-direction:column;min-height:100dvh;}
.screen.active{display:flex;}

/* ══════════════════════════════
   HOME SCREEN
══════════════════════════════ */

/* GREEN HEADER */
.home-header{
  background:var(--green);
  padding:calc(var(--safe-top)+14px) 20px 0;
  position:sticky;top:0;z-index:50;
}
.hh-top{
  display:flex;align-items:center;justify-content:space-between;
  margin-bottom:12px;
}
.hh-menu{
  background:none;border:none;cursor:pointer;
  display:flex;flex-direction:column;gap:4px;padding:4px;
}
.hh-menu span{display:block;width:22px;height:2px;background:#fff;border-radius:2px;}
.hh-title{font-size:14px;font-weight:700;color:rgba(255,255,255,0.9);letter-spacing:1px;text-transform:uppercase;}
.hh-icon-btn{background:none;border:none;cursor:pointer;color:#fff;font-size:22px;}

.saldo-wrap{text-align:center;padding-bottom:16px;}
.saldo-lbl{font-size:12px;font-weight:600;color:rgba(255,255,255,0.7);letter-spacing:1.5px;text-transform:uppercase;margin-bottom:4px;}
.saldo-val{
  font-size:32px;font-weight:900;color:#fff;letter-spacing:-0.5px;
  display:flex;align-items:center;justify-content:center;gap:8px;
}
.saldo-edit{font-size:18px;cursor:pointer;opacity:.7;}

/* PENGELUARAN / PEMASUKAN TABS */
.type-tabs{
  display:grid;grid-template-columns:1fr 1fr;
  border-top:1px solid rgba(255,255,255,0.2);
}
.type-tab{
  padding:12px;text-align:center;
  font-size:13px;font-weight:800;letter-spacing:0.5px;
  color:rgba(255,255,255,0.6);cursor:pointer;
  border-bottom:3px solid transparent;
  transition:color .15s,border-color .15s;
  text-transform:uppercase;
  background:none;border-left:none;border-right:none;border-top:none;
  font-family:var(--font);
}
.type-tab.active{color:#fff;border-bottom:3px solid #fff;}

/* ══════════════════════════════
   CONTENT AREA
══════════════════════════════ */
.home-content{flex:1;overflow-y:auto;padding-bottom:calc(80px + var(--safe-bot));}

/* PERIOD TABS */
.period-card{
  background:var(--card);
  margin:14px 14px 0;border-radius:14px;
  box-shadow:0 2px 10px rgba(0,0,0,0.07);
  overflow:hidden;
}
.period-tabs{
  display:flex;border-bottom:1px solid var(--border);
  padding:0 8px;
}
.period-tab{
  flex:1;padding:12px 4px;text-align:center;
  font-size:13px;font-weight:700;color:var(--sub);
  cursor:pointer;border-bottom:2px solid transparent;
  transition:color .13s,border-color .13s;
  background:none;border-left:none;border-right:none;border-top:none;
  font-family:var(--font);
}
.period-tab.active{color:var(--green);border-bottom:2px solid var(--green);}

.period-nav{
  display:flex;align-items:center;justify-content:center;
  gap:20px;padding:10px 16px;
  border-bottom:1px solid var(--border);
}
.period-arr{
  background:none;border:none;cursor:pointer;
  font-size:20px;color:var(--sub);padding:4px 8px;
}
.period-date{font-size:14px;font-weight:700;color:var(--text);text-decoration:underline;}

/* DONUT CHART */
.donut-wrap{
  display:flex;flex-direction:column;align-items:center;
  padding:16px 16px 8px;
  position:relative;
}
.donut-svg{width:180px;height:180px;}
.donut-center{
  position:absolute;
  top:50%;left:50%;transform:translate(-50%,-50%);
  text-align:center;pointer-events:none;
  margin-top:8px;
}
.donut-total{font-size:20px;font-weight:900;color:var(--text);}
.donut-lbl{font-size:11px;color:var(--sub);font-weight:600;}

/* FAB inside card */
.fab-in-card{
  position:absolute;bottom:16px;right:16px;
  width:44px;height:44px;
  background:var(--orange);border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:22px;color:#fff;cursor:pointer;
  box-shadow:0 4px 12px rgba(245,166,35,.4);
  border:none;font-family:var(--font);font-weight:800;
  transition:transform .12s;
}
.fab-in-card:active{transform:scale(.92);}

/* CATEGORY LIST */
.cat-rows{padding:8px 14px 14px;}
.cat-row{
  display:flex;align-items:center;
  padding:12px 14px;background:var(--card);
  border-radius:12px;margin-bottom:8px;
  box-shadow:0 1px 6px rgba(0,0,0,0.05);
  gap:12px;
}
.cat-row-icon{
  width:40px;height:40px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:18px;flex-shrink:0;
}
.cat-row-name{flex:1;font-size:14px;font-weight:700;color:var(--text);}
.cat-row-pct{font-size:13px;color:var(--sub);margin-right:12px;}
.cat-row-val{font-size:14px;font-weight:700;color:var(--text);}

/* ══════════════════════════════
   TRANSAKSI SCREEN
══════════════════════════════ */
.tx-header{
  background:var(--green);
  padding:calc(var(--safe-top)+14px) 20px 0;
  position:sticky;top:0;z-index:50;
}
.txh-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;}
.txh-title{font-size:15px;font-weight:800;color:#fff;letter-spacing:0.3px;}
.txh-period{display:flex;border-bottom:1px solid rgba(255,255,255,0.2);padding:0 4px;}
.txh-tab{
  flex:1;padding:10px 4px;text-align:center;
  font-size:12px;font-weight:800;color:rgba(255,255,255,0.6);
  cursor:pointer;border-bottom:2px solid transparent;
  transition:all .13s;
  background:none;border-left:none;border-right:none;border-top:none;
  font-family:var(--font);text-transform:uppercase;letter-spacing:.5px;
}
.txh-tab.active{color:#fff;border-bottom:2px solid #fff;}

.tx-content{flex:1;overflow-y:auto;padding:14px 14px calc(80px + var(--safe-bot));}

.tx-total-row{
  display:flex;align-items:center;justify-content:space-between;
  margin-bottom:14px;
}
.tx-total-lbl{font-size:15px;font-weight:800;color:var(--text);}
.tx-sort{
  display:flex;align-items:center;gap:4px;
  font-size:13px;font-weight:600;color:var(--text2);
  background:none;border:none;font-family:var(--font);cursor:pointer;
}

/* TX GROUP */
.tx-group{margin-bottom:14px;}
.tx-group-date{font-size:12px;font-weight:700;color:var(--sub);margin-bottom:8px;}
.tx-item-row{
  display:flex;align-items:center;gap:12px;
  background:var(--card);border-radius:12px;
  padding:12px 14px;margin-bottom:6px;
  box-shadow:0 1px 5px rgba(0,0,0,0.05);
}
.tx-item-ico{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0;}
.tx-item-body{flex:1;min-width:0;}
.tx-item-name{font-size:14px;font-weight:700;color:var(--text);}
.tx-item-note{font-size:12px;color:var(--sub);margin-top:1px;}
.tx-item-amt{font-size:14px;font-weight:800;color:var(--text);white-space:nowrap;}
.tx-item-del{background:none;border:none;color:#DDD;font-size:17px;cursor:pointer;padding:2px 0 2px 8px;transition:color .12s;}
.tx-item-del:active{color:var(--red);}

.tx-empty{text-align:center;padding:48px 20px;color:var(--sub);}
.tx-empty .ei{font-size:44px;margin-bottom:12px;}
.tx-empty p{font-size:14px;line-height:1.8;}

/* ══════════════════════════════
   ADD TRANSACTION SCREEN
══════════════════════════════ */
.add-header{
  background:var(--green);
  padding:calc(var(--safe-top)+14px) 20px 0;
  position:sticky;top:0;z-index:50;
}
.addh-top{display:flex;align-items:center;gap:12px;margin-bottom:0;}
.addh-back{background:none;border:none;color:#fff;font-size:22px;cursor:pointer;padding:4px;}
.addh-title{font-size:15px;font-weight:800;color:#fff;flex:1;text-align:center;}
.add-type-tabs{display:grid;grid-template-columns:1fr 1fr;border-top:1px solid rgba(255,255,255,.2);}
.add-tab{
  padding:12px;text-align:center;
  font-size:13px;font-weight:800;letter-spacing:.5px;text-transform:uppercase;
  color:rgba(255,255,255,.6);cursor:pointer;
  border-bottom:3px solid transparent;transition:all .13s;
  background:none;border-left:none;border-right:none;border-top:none;
  font-family:var(--font);
}
.add-tab.active{color:#fff;border-bottom:3px solid #fff;}

.add-content{flex:1;overflow-y:auto;padding:0 0 calc(80px + var(--safe-bot));}

/* AMOUNT INPUT */
.amount-section{
  background:#fff;padding:24px 24px 16px;
  border-bottom:1px solid var(--border);
  display:flex;align-items:flex-end;justify-content:center;gap:12px;
}
.amt-number{
  font-size:42px;font-weight:900;color:var(--text);
  border:none;outline:none;font-family:var(--font);
  border-bottom:2px solid var(--border);
  background:none;text-align:right;min-width:80px;max-width:160px;
  letter-spacing:-1px;
}
.amt-number:focus{border-bottom-color:var(--green);}

/* CATEGORY SECTION */
.add-section{background:#fff;margin-top:8px;padding:16px 16px 8px;}
.add-sec-lbl{font-size:12px;font-weight:700;color:var(--sub);margin-bottom:12px;letter-spacing:.5px;}
.add-cat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:4px;}
.add-cat-item{
  display:flex;flex-direction:column;align-items:center;gap:6px;
  padding:10px 4px 8px;border-radius:12px;cursor:pointer;
  transition:background .12s;
}
.add-cat-item:active{background:var(--green-lt);}
.add-cat-item.sel .add-cat-circle{background:var(--green) !important;}
.add-cat-item.sel .add-cat-name{color:var(--green);}
.add-cat-circle{
  width:52px;height:52px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:22px;
  transition:transform .12s;
}
.add-cat-item:active .add-cat-circle{transform:scale(.92);}
.add-cat-name{font-size:11px;font-weight:700;color:var(--text2);text-align:center;}

/* DATE & NOTE */
.add-fields{background:#fff;margin-top:8px;}
.add-field{
  display:flex;flex-direction:column;
  padding:14px 20px;border-bottom:1px solid var(--border);
}
.add-field-lbl{font-size:12px;font-weight:700;color:var(--sub);margin-bottom:4px;}
.add-field input{
  background:none;border:none;outline:none;
  font-family:var(--font);font-size:15px;font-weight:600;color:var(--text);
}
.add-field input::placeholder{color:#CCC;}

/* TAMBAH BUTTON */
.tambah-btn-wrap{padding:16px 20px;}
.tambah-btn{
  width:100%;background:var(--orange);color:var(--text);
  border:none;border-radius:50px;padding:16px;
  font-family:var(--font);font-size:16px;font-weight:800;
  cursor:pointer;transition:opacity .12s,transform .12s;
  box-shadow:0 4px 16px rgba(245,166,35,.35);
}
.tambah-btn:active{opacity:.88;transform:scale(.98);}

/* ══════════════════════════════
   BOTTOM NAV
══════════════════════════════ */
.bottom-nav{
  position:fixed;bottom:0;left:0;right:0;
  height:calc(64px + var(--safe-bot));
  padding-bottom:var(--safe-bot);
  background:rgba(255,255,255,0.97);
  backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);
  border-top:1px solid var(--border);
  display:flex;align-items:flex-start;justify-content:space-around;
  z-index:100;padding-top:10px;
}
.nav-btn{display:flex;flex-direction:column;align-items:center;gap:3px;background:none;border:none;color:#BBB;cursor:pointer;padding:4px 20px;font-family:var(--font);transition:color .12s;}
.nav-btn.active{color:var(--green);}
.nav-btn svg{width:22px;height:22px;}
.nav-lbl{font-size:10px;font-weight:700;}

/* ══════════════════════════════
   TOAST
══════════════════════════════ */
.toast{position:fixed;top:calc(var(--safe-top)+14px);left:50%;transform:translateX(-50%) translateY(-80px);background:#222;color:#fff;font-size:13px;font-weight:700;padding:10px 20px;border-radius:20px;white-space:nowrap;z-index:999;transition:transform .3s cubic-bezier(.34,1.56,.64,1);box-shadow:0 4px 20px rgba(0,0,0,.2);pointer-events:none;}
.toast.show{transform:translateX(-50%) translateY(0);}

/* ══════════════════════════════
   PENGELUARAN TETAP SCREEN
══════════════════════════════ */
.tetap-header{
  background:var(--green);
  padding:calc(var(--safe-top)+14px) 20px 16px;
  position:sticky;top:0;z-index:50;
}
.tetaph-top{display:flex;align-items:center;justify-content:space-between;}
.tetaph-title{font-size:15px;font-weight:800;color:#fff;}
.tetaph-add{background:rgba(255,255,255,.2);border:none;border-radius:20px;padding:6px 14px;color:#fff;font-family:var(--font);font-size:12px;font-weight:700;cursor:pointer;}

.tetap-content{flex:1;overflow-y:auto;padding:14px 14px calc(80px + var(--safe-bot));}

.prog-card{background:var(--card);border-radius:14px;padding:14px 16px;margin-bottom:12px;box-shadow:0 1px 6px rgba(0,0,0,.06);display:none;align-items:center;gap:12px;}
.pc-text{flex:1;}
.pc-title{font-size:13px;font-weight:700;color:var(--text);}
.pc-sub{font-size:11px;color:var(--sub);margin-top:2px;}
.pc-track{height:5px;background:var(--bg);border-radius:4px;margin-top:7px;overflow:hidden;}
.pc-fill{height:100%;border-radius:4px;background:linear-gradient(90deg,var(--green),#7EC8A0);transition:width .5s ease;}
.pc-count{font-size:20px;font-weight:800;color:var(--green);}

.tetap-list{display:flex;flex-direction:column;gap:8px;}
.tetap-item{background:var(--card);border-radius:12px;padding:12px 14px;display:flex;align-items:center;gap:11px;box-shadow:0 1px 5px rgba(0,0,0,.05);position:relative;transition:opacity .2s;}
.tetap-item.paid{opacity:.45;}
.tetap-item.paid .ti-name{text-decoration:line-through;color:var(--sub);}
.ti-icon{width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;}
.ti-body{flex:1;min-width:0;}
.ti-name{font-size:14px;font-weight:700;color:var(--text);}
.ti-sub{font-size:11px;color:var(--sub);margin-top:1px;}
.ti-right{display:flex;flex-direction:column;align-items:flex-end;gap:5px;flex-shrink:0;}
.ti-amount{font-size:13px;font-weight:800;color:var(--red);}
.pay-btn{background:var(--green);color:#fff;border:none;border-radius:8px;padding:5px 12px;font-family:var(--font);font-size:11px;font-weight:700;cursor:pointer;transition:transform .12s;white-space:nowrap;}
.pay-btn:active{transform:scale(.92);}
.tetap-item.paid .pay-btn{background:#888;pointer-events:none;}
.ti-acts{position:absolute;top:6px;right:8px;display:flex;gap:2px;}
.ti-act{background:none;border:none;color:#CCC;font-size:14px;cursor:pointer;padding:2px 4px;border-radius:5px;transition:color .12s;}
.ti-act:active{color:var(--red);}
.ti-act.ed:active{color:var(--green);}

/* ADD TETAP SHEET */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.3);z-index:200;display:none;align-items:flex-end;backdrop-filter:blur(3px);}
.overlay.open{display:flex;}
.sheet{width:100%;background:#fff;border-radius:22px 22px 0 0;padding:0 20px calc(var(--safe-bot)+24px);max-height:92dvh;overflow-y:auto;transform:translateY(100%);transition:transform .33s cubic-bezier(.32,.72,0,1);box-shadow:0 -4px 28px rgba(0,0,0,.12);}
.overlay.open .sheet{transform:translateY(0);}
.sh-handle{width:36px;height:4px;background:#E0E0E0;border-radius:2px;margin:11px auto 16px;}
.sh-title{font-size:17px;font-weight:800;margin-bottom:4px;color:var(--text);}
.sh-sub{font-size:13px;color:var(--sub);margin-bottom:16px;line-height:1.5;}
.sh-amt-wrap{background:var(--bg);border:1.5px solid var(--border);border-radius:13px;padding:13px 16px;margin-bottom:11px;display:flex;align-items:center;gap:7px;transition:border-color .13s;}
.sh-amt-wrap:focus-within{border-color:var(--green);}
.sh-amt-pre{font-size:16px;font-weight:700;color:var(--sub);}
.sh-amt-inp{flex:1;background:none;border:none;outline:none;font-family:var(--font);font-size:24px;font-weight:800;color:var(--text);letter-spacing:-1px;width:100%;}
.sh-amt-inp::placeholder{color:#DDD;}
.sh-fld-group{display:flex;flex-direction:column;gap:7px;margin-bottom:12px;}
.sh-fld{background:var(--bg);border:1.5px solid var(--border);border-radius:11px;padding:11px 13px;display:flex;flex-direction:column;gap:3px;transition:border-color .13s;}
.sh-fld:focus-within{border-color:var(--green);}
.sh-fld label{font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--sub);}
.sh-fld input{background:none;border:none;outline:none;font-family:var(--font);font-size:14px;font-weight:600;color:var(--text);width:100%;padding:0;}
.sh-cat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin-bottom:14px;}
.sh-cat-opt{display:flex;flex-direction:column;align-items:center;gap:4px;padding:8px 2px;border-radius:11px;border:1.5px solid var(--border);background:var(--bg);cursor:pointer;transition:all .12s;}
.sh-cat-opt:active{transform:scale(.93);}
.sh-cat-opt.sel{border-color:var(--green);background:var(--green-lt);}
.sh-cat-opt .co-i{font-size:20px;line-height:1;}
.sh-cat-opt .co-n{font-size:10px;font-weight:600;color:var(--sub);text-align:center;}
.sh-cat-opt.sel .co-n{color:var(--green);}
.sh-save-btn{width:100%;background:var(--orange);color:var(--text);border:none;border-radius:50px;padding:14px;font-family:var(--font);font-size:15px;font-weight:800;cursor:pointer;transition:opacity .12s;box-shadow:0 4px 12px rgba(245,166,35,.3);}
.sh-save-btn:active{opacity:.88;}

/* SETT */
.sett-header{background:var(--green);padding:calc(var(--safe-top)+14px) 20px 16px;position:sticky;top:0;z-index:50;}
.sett-header-title{font-size:15px;font-weight:800;color:#fff;}
.sett-content{flex:1;overflow-y:auto;padding:14px 14px calc(80px+var(--safe-bot));display:flex;flex-direction:column;gap:10px;}
.sett-card{background:var(--card);border-radius:14px;overflow:hidden;box-shadow:0 1px 5px rgba(0,0,0,.06);}
.sett-row{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .1s;}
.sett-row:last-child{border-bottom:none;}
.sett-row:active{background:var(--bg);}
.sett-lbl{font-size:14px;font-weight:700;color:var(--text);}
.sett-sub2{font-size:11px;color:var(--sub);margin-top:2px;}
.sett-chev{color:#CCC;font-size:17px;}
.danger .sett-lbl{color:var(--red);}
</style>
</head>
<body>

<!-- ══════════════════════════════════
     HOME SCREEN
══════════════════════════════════ -->
<div class="screen active" id="screen-home">
  <div class="home-header">
    <div class="hh-top">
      <button class="hh-menu" onclick="goScreen('sett')">
        <span></span><span></span><span></span>
      </button>
      <span class="hh-title">SALDO</span>
      <button class="hh-icon-btn" onclick="goScreen('transaksi')">☰</button>
    </div>
    <div class="saldo-wrap">
      <div class="saldo-lbl">SALDO</div>
      <div class="saldo-val">
        <span id="homeSaldo">Rp 0</span>
        <span class="saldo-edit">✏️</span>
      </div>
    </div>
    <div class="type-tabs">
      <button class="type-tab active" id="homeTabOut" onclick="setHomeTab('out')">PENGELUARAN</button>
      <button class="type-tab"        id="homeTabInp" onclick="setHomeTab('inp')">PEMASUKAN</button>
    </div>
  </div>

  <div class="home-content">
    <!-- PERIOD CARD with CHART -->
    <div class="period-card">
      <div class="period-tabs">
        <button class="period-tab active" onclick="setPeriod('hari',this)">Hari</button>
        <button class="period-tab"        onclick="setPeriod('minggu',this)">Minggu</button>
        <button class="period-tab"        onclick="setPeriod('bulan',this)">Bulan</button>
        <button class="period-tab"        onclick="setPeriod('tahun',this)">Tahun</button>
      </div>
      <div class="period-nav">
        <button class="period-arr" onclick="shiftPeriod(-1)">‹</button>
        <span class="period-date" id="periodLabel"></span>
        <button class="period-arr" onclick="shiftPeriod(1)">›</button>
      </div>
      <div class="donut-wrap" style="position:relative;min-height:200px;">
        <svg class="donut-svg" viewBox="0 0 180 180" id="donutSvg"></svg>
        <div class="donut-center" id="donutCenter">
          <div class="donut-total" id="donutTotal">Rp 0</div>
          <div class="donut-lbl" id="donutLbl">total</div>
        </div>
        <button class="fab-in-card" onclick="goScreen('add')">+</button>
      </div>
    </div>

    <!-- CATEGORY ROWS -->
    <div class="cat-rows" id="catRows"></div>
  </div>
</div>

<!-- ══════════════════════════════════
     TRANSAKSI SCREEN
══════════════════════════════════ -->
<div class="screen" id="screen-transaksi">
  <div class="tx-header">
    <div class="txh-top">
      <span class="txh-title">Operasi</span>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;border-top:1px solid rgba(255,255,255,.2);">
      <button class="type-tab active" id="txTabOut" onclick="setTxTab('out')">PENGELUARAN</button>
      <button class="type-tab"        id="txTabInp" onclick="setTxTab('inp')">PEMASUKAN</button>
    </div>
    <div class="txh-period">
      <button class="txh-tab active" onclick="setTxPeriod('hari',this)">Hari</button>
      <button class="txh-tab"        onclick="setTxPeriod('minggu',this)">Minggu</button>
      <button class="txh-tab"        onclick="setTxPeriod('bulan',this)">Bulan</button>
      <button class="txh-tab"        onclick="setTxPeriod('tahun',this)">Tahun</button>
      <button class="txh-tab"        onclick="setTxPeriod('semua',this)">Semua</button>
    </div>
  </div>
  <div class="tx-content">
    <div class="tx-total-row">
      <span class="tx-total-lbl" id="txTotalLbl">Total: Rp 0</span>
      <button class="tx-sort">Berdasar tanggal ▾</button>
    </div>
    <div id="txGroups"></div>
  </div>
</div>

<!-- ══════════════════════════════════
     ADD TRANSACTION SCREEN
══════════════════════════════════ -->
<div class="screen" id="screen-add">
  <div class="add-header">
    <div class="addh-top">
      <button class="addh-back" onclick="goBack()">←</button>
      <span class="addh-title">Tambah transaksi</span>
      <span style="width:30px"></span>
    </div>
    <div class="add-type-tabs">
      <button class="add-tab active" id="addTabOut" onclick="setAddTab('out')">PENGELUARAN</button>
      <button class="add-tab"        id="addTabInp" onclick="setAddTab('inp')">PEMASUKAN</button>
    </div>
  </div>
  <div class="add-content">
    <div class="amount-section">
      <input class="amt-number" type="text" id="addAmt" placeholder="0" inputmode="numeric" oninput="fmtAddAmt(this)"/>
    </div>

    <div class="add-section">
      <div class="add-sec-lbl">Kategori</div>
      <div class="add-cat-grid" id="addCatGrid"></div>
    </div>

    <div class="add-fields">
      <div class="add-field">
        <div class="add-field-lbl">Tanggal</div>
        <input type="date" id="addTgl"/>
      </div>
      <div class="add-field">
        <div class="add-field-lbl">Komentar</div>
        <input type="text" id="addNote" placeholder="Komentar"/>
      </div>
    </div>

    <div class="tambah-btn-wrap">
      <button class="tambah-btn" onclick="simpanTx()">Tambah</button>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════
     PENGELUARAN TETAP SCREEN
══════════════════════════════════ -->
<div class="screen" id="screen-tetap">
  <div class="tetap-header">
    <div class="tetaph-top">
      <span class="tetaph-title">📌 Pengeluaran Tetap</span>
      <button class="tetaph-add" onclick="openTetapSheet()">+ Tambah</button>
    </div>
  </div>
  <div class="tetap-content">
    <div class="prog-card" id="progCard">
      <div class="pc-text">
        <div class="pc-title">Progress Pembayaran</div>
        <div class="pc-sub" id="progSub">—</div>
        <div class="pc-track"><div class="pc-fill" id="progFill" style="width:0%"></div></div>
      </div>
      <div class="pc-count" id="progCount">0/0</div>
    </div>
    <div id="tetapContainer"></div>
  </div>
</div>

<!-- ══════════════════════════════════
     PENGATURAN SCREEN
══════════════════════════════════ -->
<div class="screen" id="screen-sett">
  <div class="sett-header"><div class="sett-header-title">⚙️ Pengaturan</div></div>
  <div class="sett-content">
    <div class="sett-card">
      <div class="sett-row" onclick="exportData()"><div><div class="sett-lbl">📤 Export Data</div><div class="sett-sub2">Unduh semua data sebagai file JSON</div></div><span class="sett-chev">›</span></div>
      <div class="sett-row" onclick="importData()"><div><div class="sett-lbl">📥 Import Data</div><div class="sett-sub2">Pulihkan data dari file JSON</div></div><span class="sett-chev">›</span></div>
    </div>
    <div class="sett-card">
      <div class="sett-row danger" onclick="hapusSemua()"><div><div class="sett-lbl">🗑️ Hapus Semua Data</div><div class="sett-sub2">Tidak bisa dibatalkan</div></div><span class="sett-chev">›</span></div>
    </div>
    <p style="font-size:12px;color:var(--sub);text-align:center;padding:10px 0;line-height:1.8;">Data tersimpan di perangkat ini.<br>Gunakan Export/Import untuk pindah ke HP lain.</p>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <button class="nav-btn active" id="nav-home" onclick="goScreen('home')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9.5L12 3l9 6.5V20a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V9.5z"/><path d="M9 21V12h6v9"/></svg>
    <span class="nav-lbl">Beranda</span>
  </button>
  <button class="nav-btn" id="nav-transaksi" onclick="goScreen('transaksi')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M8 6h13M8 12h13M8 18h13M3 6h.01M3 12h.01M3 18h.01"/></svg>
    <span class="nav-lbl">Transaksi</span>
  </button>
  <button class="nav-btn" id="nav-add" onclick="goScreen('add')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="16"/><line x1="8" y1="12" x2="16" y2="12"/></svg>
    <span class="nav-lbl">Tambah</span>
  </button>
  <button class="nav-btn" id="nav-tetap" onclick="goScreen('tetap')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M9 5H7a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2h-2M9 5a2 2 0 0 0 2 2h2a2 2 0 0 0 2-2M9 5a2 2 0 0 1 2-2h2a2 2 0 0 1 2 2"/></svg>
    <span class="nav-lbl">Tetap</span>
  </button>
  <button class="nav-btn" id="nav-sett" onclick="goScreen('sett')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
    <span class="nav-lbl">Pengaturan</span>
  </button>
</nav>

<!-- SHEET PENGELUARAN TETAP -->
<div class="overlay" id="ovTetap" onclick="if(event.target===this)closeTetapSheet()">
  <div class="sheet">
    <div class="sh-handle"></div>
    <div class="sh-title" id="tetapShTitle">Pengeluaran Tetap Baru</div>
    <div class="sh-sub">Tap <b>Bayar</b> saat sudah dibayar — otomatis langsung tercatat.</div>
    <div class="sh-amt-wrap"><span class="sh-amt-pre">Rp</span><input class="sh-amt-inp" type="text" id="tJml" placeholder="0" inputmode="numeric" oninput="fmtInput(this)"/></div>
    <div class="sh-cat-grid" id="tetapCatGrid"></div>
    <div class="sh-fld-group">
      <div class="sh-fld"><label>Nama</label><input type="text" id="tNama" placeholder="cth: Listrik, WiFi, Uang Mama..."/></div>
      <div class="sh-fld"><label>Catatan (opsional)</label><input type="text" id="tCat" placeholder="cth: PLN, Indihome..."/></div>
    </div>
    <button class="sh-save-btn" onclick="simpanTetap()">Simpan</button>
  </div>
</div>

<input type="file" id="fileImport" accept=".json" style="display:none" onchange="handleImport(event)"/>
<div class="toast" id="toast"></div>

<script>
/* ═══════════════════════════════════
   KATEGORI & WARNA DONUT
═══════════════════════════════════ */
const CATS = [
  {k:'Makanan',    i:'🍜', bg:'#4A8C6F', color:'#4A8C6F'},
  {k:'Belanja',    i:'🛍️', bg:'#3498DB', color:'#3498DB'},
  {k:'Transport',  i:'🚗', bg:'#F5A623', color:'#F5A623'},
  {k:'Kesehatan',  i:'💊', bg:'#E74C3C', color:'#E74C3C'},
  {k:'Hiburan',    i:'🎮', bg:'#9B59B6', color:'#9B59B6'},
  {k:'Tagihan',    i:'💡', bg:'#F39C12', color:'#F39C12'},
  {k:'Pendidikan', i:'📚', bg:'#1ABC9C', color:'#1ABC9C'},
  {k:'Gaji',       i:'💼', bg:'#27AE60', color:'#27AE60'},
  {k:'Tabungan',   i:'🏦', bg:'#2980B9', color:'#2980B9'},
  {k:'Keluarga',   i:'👨‍👩‍👧', bg:'#E67E22', color:'#E67E22'},
  {k:'Lainnya',    i:'📦', bg:'#95A5A6', color:'#95A5A6'},
];

const K_TX    = 'dompet_tx_v2';
const K_TETAP = 'dompet_tetap_v3';

let txs   = JSON.parse(localStorage.getItem(K_TX)    || '[]');
let tetap = JSON.parse(localStorage.getItem(K_TETAP) || 'null');
if (!tetap) { tetap={items:[],paid:{}}; localStorage.setItem(K_TETAP,JSON.stringify(tetap)); }

/* STATE */
let homeTab   = 'out';   // out | inp
let homePeriod= 'bulan'; // hari|minggu|bulan|tahun
let periodOff = 0;       // offset dari periode sekarang
let txTab     = 'out';
let txPeriod  = 'bulan';
let addTab    = 'out';
let selAddCat = 'Makanan';
let selTetapCat='Tagihan';
let editingId = null;
let prevScreen= 'home';

/* ═══════════════════════════════════
   INIT
═══════════════════════════════════ */
document.getElementById('addTgl').value = new Date().toISOString().split('T')[0];
buildAddCatGrid();
buildCatGrid('tetapCatGrid', selTetapCat, 'pickTetapCat');
refreshHome();
renderTetap();

/* ═══════════════════════════════════
   NAVIGASI
═══════════════════════════════════ */
function goScreen(id) {
  prevScreen = document.querySelector('.screen.active')?.id?.replace('screen-','') || 'home';
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('screen-'+id).classList.add('active');
  const nb = document.getElementById('nav-'+id);
  if (nb) nb.classList.add('active');
  if (id==='transaksi') renderTxScreen();
  if (id==='tetap')     renderTetap();
}
function goBack() { goScreen(prevScreen || 'home'); }

/* ═══════════════════════════════════
   HOME TABS & PERIOD
═══════════════════════════════════ */
function setHomeTab(t) {
  homeTab=t;
  document.getElementById('homeTabOut').classList.toggle('active',t==='out');
  document.getElementById('homeTabInp').classList.toggle('active',t==='inp');
  periodOff=0; refreshHome();
}
function setPeriod(p, el) {
  homePeriod=p; periodOff=0;
  document.querySelectorAll('.period-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  refreshHome();
}
function shiftPeriod(d) { periodOff+=d; refreshHome(); }

/* ═══════════════════════════════════
   HOME REFRESH
═══════════════════════════════════ */
function refreshHome() {
  // Saldo total
  let inc=0,out=0;
  txs.forEach(t=>t.jenis==='pemasukan'?inc+=t.jumlah:out+=t.jumlah);
  document.getElementById('homeSaldo').textContent=fmt(inc-out);

  // Filter berdasarkan period+tab
  const filtered = filterByPeriod(txs.filter(t=>t.jenis===(homeTab==='out'?'pengeluaran':'pemasukan')), homePeriod, periodOff);

  // Label periode
  document.getElementById('periodLabel').textContent = getPeriodLabel(homePeriod, periodOff);

  // Total
  const total = filtered.reduce((s,t)=>s+t.jumlah,0);
  document.getElementById('donutTotal').textContent = fmt(total);
  document.getElementById('donutLbl').textContent   = homeTab==='out'?'pengeluaran':'pemasukan';

  // Grup per kategori
  const byKat = {};
  filtered.forEach(t=>byKat[t.kategori]=(byKat[t.kategori]||0)+t.jumlah);
  const sorted = Object.entries(byKat).sort((a,b)=>b[1]-a[1]);

  // Donut
  drawDonut(sorted, total);

  // Cat rows
  const rows = document.getElementById('catRows');
  if (!sorted.length) { rows.innerHTML='<p style="color:#AAA;text-align:center;padding:20px;font-size:13px">Tidak ada data untuk periode ini</p>'; return; }
  rows.innerHTML = sorted.map(([k,v])=>{
    const c   = CATS.find(x=>x.k===k)||CATS[CATS.length-1];
    const pct = total ? Math.round(v/total*100) : 0;
    return `<div class="cat-row">
      <div class="cat-row-icon" style="background:${c.bg}">${c.i}</div>
      <span class="cat-row-name">${k}</span>
      <span class="cat-row-pct">${pct}%</span>
      <span class="cat-row-val">${fmt(v)}</span>
    </div>`;
  }).join('');
}

/* ═══════════════════════════════════
   DONUT CHART
═══════════════════════════════════ */
function drawDonut(sorted, total) {
  const svg = document.getElementById('donutSvg');
  const cx=90, cy=90, r=72, stroke=22;
  const circ = 2*Math.PI*r;

  if (!total) {
    svg.innerHTML=`<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#EEE" stroke-width="${stroke}"/>`;
    return;
  }

  let offset = 0;
  const paths = sorted.map(([k,v])=>{
    const c    = CATS.find(x=>x.k===k)||CATS[CATS.length-1];
    const pct  = v/total;
    const dash = pct*circ;
    const gap  = circ - dash;
    const p = `<circle cx="${cx}" cy="${cy}" r="${r}" fill="none"
      stroke="${c.bg}" stroke-width="${stroke}"
      stroke-dasharray="${dash} ${gap}"
      stroke-dashoffset="${-offset}"
      transform="rotate(-90 ${cx} ${cy})"
      style="transition:stroke-dasharray .5s ease"/>`;
    offset += pct*circ;
    return p;
  });
  svg.innerHTML = paths.join('') +
    `<circle cx="${cx}" cy="${cy}" r="${r-stroke/2-2}" fill="white"/>`;
}

/* ═══════════════════════════════════
   TRANSAKSI SCREEN
═══════════════════════════════════ */
function setTxTab(t) {
  txTab=t;
  document.getElementById('txTabOut').classList.toggle('active',t==='out');
  document.getElementById('txTabInp').classList.toggle('active',t==='inp');
  renderTxScreen();
}
function setTxPeriod(p,el) {
  txPeriod=p;
  document.querySelectorAll('.txh-tab').forEach(t=>t.classList.remove('active'));
  el.classList.add('active');
  renderTxScreen();
}
function renderTxScreen() {
  const jenis = txTab==='out'?'pengeluaran':'pemasukan';
  let filtered = txs.filter(t=>t.jenis===jenis);
  if (txPeriod!=='semua') filtered = filterByPeriod(filtered, txPeriod, 0);
  filtered.sort((a,b)=>new Date(b.tanggal)-new Date(a.tanggal));

  const total = filtered.reduce((s,t)=>s+t.jumlah,0);
  document.getElementById('txTotalLbl').textContent = `Total: ${fmt(total)}`;

  // Grup per tanggal
  const byDate = {};
  filtered.forEach(t=>{
    if (!byDate[t.tanggal]) byDate[t.tanggal]=[];
    byDate[t.tanggal].push(t);
  });
  const dates = Object.keys(byDate).sort((a,b)=>new Date(b)-new Date(a));

  const cont = document.getElementById('txGroups');
  if (!dates.length) {
    cont.innerHTML='<div class="tx-empty"><div class="ei">🗒️</div><p>Belum ada transaksi.<br>Tap tombol <b>Tambah</b> di bawah.</p></div>';
    return;
  }
  cont.innerHTML = dates.map(d=>{
    const rows = byDate[d].map(t=>{
      const c=CATS.find(x=>x.k===t.kategori)||CATS[CATS.length-1];
      return `<div class="tx-item-row">
        <div class="tx-item-ico" style="background:${c.bg}">${c.i}</div>
        <div class="tx-item-body">
          <div class="tx-item-name">${t.nama}</div>
          ${t.catatan?`<div class="tx-item-note">${t.catatan}</div>`:''}
        </div>
        <div class="tx-item-amt">${fmt(t.jumlah)}</div>
        <button class="tx-item-del" onclick="hapusTx('${t.id}')">×</button>
      </div>`;
    }).join('');
    return `<div class="tx-group">
      <div class="tx-group-date">${fmtDateLong(d)}</div>
      ${rows}
    </div>`;
  }).join('');
}

/* ═══════════════════════════════════
   ADD TRANSACTION
═══════════════════════════════════ */
function setAddTab(t) {
  addTab=t;
  document.getElementById('addTabOut').classList.toggle('active',t==='out');
  document.getElementById('addTabInp').classList.toggle('active',t==='inp');
}

function buildAddCatGrid() {
  document.getElementById('addCatGrid').innerHTML = CATS.map(c=>`
    <div class="add-cat-item ${c.k===selAddCat?'sel':''}" onclick="pickAddCat('${c.k}')">
      <div class="add-cat-circle" style="background:${c.k===selAddCat?'var(--green)':c.bg}">${c.i}</div>
      <span class="add-cat-name">${c.k}</span>
    </div>`).join('');
}
function pickAddCat(k) { selAddCat=k; buildAddCatGrid(); }

function fmtAddAmt(el) {
  let r=el.value.replace(/\D/g,''); el.dataset.raw=r;
  el.value=r?parseInt(r,10).toLocaleString('id-ID'):'';
}

function simpanTx() {
  const inp = document.getElementById('addAmt');
  const jumlah = parseFloat((inp.dataset.raw||inp.value.replace(/\D/g,'')).trim())||0;
  const tgl    = document.getElementById('addTgl').value;
  const note   = document.getElementById('addNote').value.trim();

  if (!jumlah||jumlah<=0){ toast('⚠️ Jumlah harus diisi!'); return; }
  if (!tgl)               { toast('⚠️ Tanggal harus diisi!'); return; }

  txs.push({
    id: Date.now()+'',
    jenis: addTab==='out'?'pengeluaran':'pemasukan',
    jumlah, nama: selAddCat, kategori: selAddCat,
    tanggal: tgl, catatan: note
  });
  saveTx();

  inp.value=''; inp.dataset.raw='';
  document.getElementById('addNote').value='';
  toast('✅ Tersimpan!');
  refreshHome();
  goScreen('home');
}

/* ═══════════════════════════════════
   PENGELUARAN TETAP
═══════════════════════════════════ */
function buildCatGrid(gid, cur, fn) {
  document.getElementById(gid).innerHTML = CATS.map(c=>`
    <div class="sh-cat-opt ${c.k===cur?'sel':''}" onclick="${fn}('${c.k}')">
      <div class="co-i">${c.i}</div><div class="co-n">${c.k}</div>
    </div>`).join('');
}
function pickTetapCat(k){selTetapCat=k;buildCatGrid('tetapCatGrid',selTetapCat,'pickTetapCat');}

function fmtInput(el){
  let r=el.value.replace(/\D/g,'');el.dataset.raw=r;
  el.value=r?parseInt(r,10).toLocaleString('id-ID'):'';
}
function getRaw(id){
  const el=document.getElementById(id);
  return parseFloat((el.dataset.raw||el.value.replace(/\D/g,'')).trim())||0;
}

function openTetapSheet(id){
  editingId=id||null;
  if(id){
    const item=tetap.items.find(x=>x.id===id);if(!item)return;
    document.getElementById('tetapShTitle').textContent='Edit Pengeluaran Tetap';
    selTetapCat=item.kategori;buildCatGrid('tetapCatGrid',selTetapCat,'pickTetapCat');
    const inp=document.getElementById('tJml');
    inp.dataset.raw=String(item.jumlah);inp.value=item.jumlah.toLocaleString('id-ID');
    document.getElementById('tNama').value=item.nama;
    document.getElementById('tCat').value=item.catatan||'';
  }else{
    document.getElementById('tetapShTitle').textContent='Pengeluaran Tetap Baru';
    selTetapCat='Tagihan';buildCatGrid('tetapCatGrid',selTetapCat,'pickTetapCat');
    const inp=document.getElementById('tJml');inp.value='';inp.dataset.raw='';
    document.getElementById('tNama').value='';document.getElementById('tCat').value='';
  }
  document.getElementById('ovTetap').classList.add('open');
  setTimeout(()=>document.getElementById('tJml').focus(),400);
}
function closeTetapSheet(){document.getElementById('ovTetap').classList.remove('open');editingId=null;}

function simpanTetap(){
  const j=getRaw('tJml'),n=document.getElementById('tNama').value.trim(),
        c=document.getElementById('tCat').value.trim();
  if(!j||j<=0){toast('⚠️ Nominal harus diisi!');return;}
  if(!n){toast('⚠️ Nama harus diisi!');return;}
  if(editingId){
    const idx=tetap.items.findIndex(x=>x.id===editingId);
    if(idx!==-1)tetap.items[idx]={...tetap.items[idx],nama:n,jumlah:j,kategori:selTetapCat,catatan:c};
    toast('✏️ Diperbarui!');
  }else{
    tetap.items.push({id:Date.now()+'tt',nama:n,jumlah:j,kategori:selTetapCat,catatan:c});
    toast('📌 Ditambahkan!');
  }
  saveTetap();closeTetapSheet();renderTetap();
}

function bayar(id){
  const mk=monthKey(),item=tetap.items.find(x=>x.id===id);if(!item)return;
  if(!tetap.paid[mk])tetap.paid[mk]=[];
  const sudah=tetap.paid[mk].includes(id);
  if(sudah){
    tetap.paid[mk]=tetap.paid[mk].filter(x=>x!==id);
    const bln=new Date().toISOString().slice(0,7);
    txs=txs.filter(t=>!(t._tetapId===id&&t.tanggal.startsWith(bln)));
    saveTx();saveTetap();refreshHome();renderTetap();toast('↩️ '+item.nama+' dibatalkan');
  }else{
    tetap.paid[mk].push(id);
    txs.push({id:Date.now()+'',jenis:'pengeluaran',jumlah:item.jumlah,nama:item.nama,
      kategori:item.kategori,tanggal:new Date().toISOString().split('T')[0],
      catatan:item.catatan||'Pengeluaran tetap',_tetapId:id});
    saveTx();saveTetap();refreshHome();renderTetap();toast('✅ '+item.nama+' tercatat!');
  }
}

function hapusTetap(id){
  if(!confirm('Hapus pengeluaran tetap ini?'))return;
  tetap.items=tetap.items.filter(x=>x.id!==id);
  Object.keys(tetap.paid).forEach(mk=>{tetap.paid[mk]=tetap.paid[mk].filter(x=>x!==id);});
  saveTetap();renderTetap();toast('🗑️ Dihapus');
}

function monthKey(){const n=new Date();return`${n.getFullYear()}-${n.getMonth()}`;}

function renderTetap(){
  const cont=document.getElementById('tetapContainer');
  const prog=document.getElementById('progCard');
  if(!tetap.items.length){prog.style.display='none';cont.innerHTML='';return;}
  const mk=monthKey(),paid=tetap.paid[mk]||[];
  const total=tetap.items.length,done=paid.length,pct=total?(done/total*100).toFixed(0):0;
  prog.style.display='flex';
  document.getElementById('progSub').textContent=`${done} dari ${total} sudah dibayar`;
  document.getElementById('progCount').textContent=`${done}/${total}`;
  document.getElementById('progFill').style.width=pct+'%';
  const sorted=[...tetap.items].sort((a,b)=>paid.includes(a.id)-paid.includes(b.id));
  cont.innerHTML=`<div class="tetap-list">`+sorted.map(item=>{
    const c=CATS.find(x=>x.k===item.kategori)||CATS[CATS.length-1];
    const isPaid=paid.includes(item.id);
    return`<div class="tetap-item ${isPaid?'paid':''}">
      <div class="ti-icon" style="background:${c.bg}">${c.i}</div>
      <div class="ti-body"><div class="ti-name">${item.nama}</div><div class="ti-sub">${item.catatan||item.kategori}</div></div>
      <div class="ti-right">
        <div class="ti-amount">${fmt(item.jumlah)}</div>
        <button class="pay-btn" onclick="bayar('${item.id}')">${isPaid?'✓ Sudah':'Bayar'}</button>
      </div>
      <div class="ti-acts">
        <button class="ti-act ed" onclick="openTetapSheet('${item.id}')">✏️</button>
        <button class="ti-act"    onclick="hapusTetap('${item.id}')">×</button>
      </div>
    </div>`;
  }).join('')+`</div>`;
}

/* ═══════════════════════════════════
   TX CRUD
═══════════════════════════════════ */
function hapusTx(id){
  if(!confirm('Hapus transaksi ini?'))return;
  txs=txs.filter(t=>t.id!==id);saveTx();refreshHome();renderTxScreen();toast('🗑️ Dihapus');
}
function saveTx(){localStorage.setItem(K_TX,JSON.stringify(txs));}
function saveTetap(){localStorage.setItem(K_TETAP,JSON.stringify(tetap));}

/* ═══════════════════════════════════
   EXPORT / IMPORT
═══════════════════════════════════ */
function exportData(){
  const blob=new Blob([JSON.stringify({transaksi:txs,tetap},null,2)],{type:'application/json'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);
  a.download=`dompet-${new Date().toISOString().slice(0,10)}.json`;a.click();
  toast('📤 File berhasil diunduh!');
}
function importData(){document.getElementById('fileImport').click();}
function handleImport(e){
  const file=e.target.files[0];if(!file)return;
  const r=new FileReader();
  r.onload=ev=>{
    try{
      const d=JSON.parse(ev.target.result);
      if(!confirm('Import data? Data lama akan digabung.'))return;
      if(Array.isArray(d)){const ids=new Set(txs.map(t=>t.id));txs=[...txs,...d.filter(t=>!ids.has(t.id))];}
      else{
        if(d.transaksi){const ids=new Set(txs.map(t=>t.id));txs=[...txs,...d.transaksi.filter(t=>!ids.has(t.id))];}
        if(d.tetap){tetap=d.tetap;localStorage.setItem(K_TETAP,JSON.stringify(tetap));}
      }
      saveTx();refreshHome();renderTetap();toast('✅ Import berhasil!');
    }catch{toast('❌ File tidak valid');}
    e.target.value='';
  };
  r.readAsText(file);
}
function hapusSemua(){
  if(!confirm('Yakin hapus SEMUA data?'))return;
  if(!confirm('Sekali lagi?'))return;
  txs=[];saveTx();refreshHome();toast('🗑️ Semua data dihapus');
}

/* ═══════════════════════════════════
   PERIOD HELPERS
═══════════════════════════════════ */
function filterByPeriod(arr, period, offset) {
  const now  = new Date();
  let start, end;
  if (period==='hari') {
    const d = new Date(now); d.setDate(d.getDate()+offset);
    start = new Date(d.getFullYear(),d.getMonth(),d.getDate());
    end   = new Date(d.getFullYear(),d.getMonth(),d.getDate()+1);
  } else if (period==='minggu') {
    const d  = new Date(now);
    const day= d.getDay()||7;
    d.setDate(d.getDate()-day+1+offset*7);
    start = new Date(d.getFullYear(),d.getMonth(),d.getDate());
    end   = new Date(d.getFullYear(),d.getMonth(),d.getDate()+7);
  } else if (period==='bulan') {
    const m = now.getMonth()+offset;
    const y = now.getFullYear()+Math.floor(m/12);
    const mo= ((m%12)+12)%12;
    start = new Date(y,mo,1); end=new Date(y,mo+1,1);
  } else if (period==='tahun') {
    const y = now.getFullYear()+offset;
    start=new Date(y,0,1); end=new Date(y+1,0,1);
  }
  return arr.filter(t=>{
    const d=new Date(t.tanggal);
    return d>=start && d<end;
  });
}

function getPeriodLabel(period, offset) {
  const now=new Date();
  const months=['Januari','Februari','Maret','April','Mei','Juni','Juli','Agustus','September','Oktober','November','Desember'];
  const days  =['Minggu','Senin','Selasa','Rabu','Kamis','Jumat','Sabtu'];
  if (period==='hari'){
    const d=new Date(now); d.setDate(d.getDate()+offset);
    if (offset===0) return 'Hari Ini, '+d.getDate()+' '+months[d.getMonth()];
    return days[d.getDay()]+', '+d.getDate()+' '+months[d.getMonth()];
  } else if (period==='minggu'){
    const d=new Date(now);const day=d.getDay()||7;
    d.setDate(d.getDate()-day+1+offset*7);
    const e=new Date(d);e.setDate(e.getDate()+6);
    return d.getDate()+' '+months[d.getMonth()].slice(0,3)+' - '+e.getDate()+' '+months[e.getMonth()].slice(0,3);
  } else if (period==='bulan'){
    const m=now.getMonth()+offset;
    const y=now.getFullYear()+Math.floor(m/12);
    const mo=((m%12)+12)%12;
    return months[mo]+' '+y;
  } else if (period==='tahun'){
    return String(now.getFullYear()+offset);
  }
  return '';
}

/* ═══════════════════════════════════
   UTILS
═══════════════════════════════════ */
function fmt(n){return 'Rp '+Math.abs(n).toLocaleString('id-ID');}
function fmtDateLong(s){
  const d=new Date(s);
  const months=['Januari','Februari','Maret','April','Mei','Juni','Juli','Agustus','September','Oktober','November','Desember'];
  return d.getDate()+' '+months[d.getMonth()]+' '+d.getFullYear();
}
function toast(msg){
  const el=document.getElementById('toast');
  el.textContent=msg;el.classList.add('show');
  setTimeout(()=>el.classList.remove('show'),2600);
}
</script>
</body>
</html>
