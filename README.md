<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>coretable</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400&family=Inter:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
/* ============================================================
   CSS VARIABLES
   ============================================================ */
:root {
  --bg:           #F7F7F5;
  --surface:      #FFFFFF;
  --surface2:     #F1F1EF;
  --surface3:     #E8E8E5;
  --border:       #E2E2DE;
  --border2:      #C9C9C4;
  --tx:           #1A1A19;
  --tx2:          #6B6B68;
  --tx3:          #A8A8A3;
  --accent:       #2F6EEB;
  --accent-h:     #1A5BD8;
  --accent-bg:    rgba(47,110,235,.07);
  --red:          #D04545;
  --red-bg:       rgba(208,69,69,.06);

  --g-hd:  #EEF0F0;
  --g-nd:  #F9F9F9;
  --g-div: #BCC1C2;

  --p-hd:  #F9E3E4;
  --p-nd:  #FEFAFB;
  --p-div: #DA7B7B;

  --r: 5px;
  --r2: 9px;
}

/* ============================================================ RESET */
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Inter',sans-serif;background:var(--bg);color:var(--tx);height:100vh;display:flex;flex-direction:column;overflow:hidden;font-size:13px}

/* ============================================================ HEADER */
header{
  background:var(--surface);border-bottom:1px solid var(--border);
  padding:0 16px;height:48px;
  display:flex;align-items:center;justify-content:space-between;
  flex-shrink:0;z-index:50;
}
.logo{font-family:'DM Mono',monospace;font-size:13px;font-weight:500;display:flex;align-items:center;gap:8px}
.logo em{color:var(--accent);font-style:normal}
.badge{display:inline-flex;align-items:center;background:var(--accent-bg);color:var(--accent);border-radius:100px;padding:1px 8px;font-size:11px;font-weight:500}
.hdr-r{display:flex;align-items:center;gap:6px}

/* ============================================================ BUTTONS */
.btn{
  display:inline-flex;align-items:center;gap:5px;
  padding:5px 11px;border-radius:var(--r);
  font-family:'Inter',sans-serif;font-size:12px;font-weight:500;
  cursor:pointer;border:none;transition:all .13s;white-space:nowrap;line-height:1.4;
}
.btn-p{background:var(--accent);color:#fff}
.btn-p:hover{background:var(--accent-h)}
.btn-g{background:transparent;color:var(--tx2);border:1px solid var(--border)}
.btn-g:hover{background:var(--surface2);color:var(--tx)}
.btn-d{background:transparent;color:var(--red);border:1px solid rgba(208,69,69,.25)}
.btn-d:hover{background:var(--red-bg)}
.btn:disabled{opacity:.38;cursor:not-allowed}

/* ============================================================ LAYOUT */
.body{display:flex;flex:1;overflow:hidden;min-height:0}

/* ---- Sidebar ---- */
.sb{width:218px;min-width:218px;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden}
.sb-top{padding:11px;border-bottom:1px solid var(--border);display:flex;flex-direction:column;gap:8px}
.sb-lbl{font-size:10px;font-weight:600;letter-spacing:.07em;text-transform:uppercase;color:var(--tx3)}
.tbl-list{flex:1;overflow-y:auto;padding:5px}
.tbl-item{padding:7px 9px;border-radius:var(--r);cursor:pointer;display:flex;align-items:center;justify-content:space-between;gap:6px;border:1px solid transparent;transition:all .1s;user-select:none}
.tbl-item:hover{background:var(--surface2)}
.tbl-item.active{background:var(--accent-bg);border-color:rgba(47,110,235,.18)}
.tbl-item-n{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:12px;color:var(--tx2)}
.tbl-item.active .tbl-item-n{color:var(--accent);font-weight:500}
.tbl-item-b{font-size:10px;background:var(--surface3);padding:2px 5px;border-radius:3px;color:var(--tx3);flex-shrink:0;display:flex;align-items:center;gap:0}

/* ---- Right Panel ---- */
.panel{width:248px;min-width:248px;background:var(--surface);border-left:1px solid var(--border);overflow-y:auto;display:flex;flex-direction:column;z-index:100}
.ps{padding:12px 13px;border-bottom:1px solid var(--border)}
.pt{font-size:10px;font-weight:600;letter-spacing:.07em;text-transform:uppercase;color:var(--tx3);margin-bottom:9px}
.fld{display:flex;flex-direction:column;gap:3px;margin-bottom:9px}
.fld:last-child{margin-bottom:0}
.fl{font-size:11px;color:var(--tx2);font-weight:500}
.fr{display:flex;gap:5px;align-items:center}
input[type=range]{-webkit-appearance:none;width:100%;height:3px;background:var(--surface3);border-radius:2px;outline:none;cursor:pointer;flex:1}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:12px;height:12px;border-radius:50%;background:var(--accent);cursor:pointer}
.ni{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);color:var(--tx);font-family:'DM Mono',monospace;font-size:11px;padding:3px 5px;width:54px;text-align:center;outline:none}
.ni:focus{border-color:var(--accent)}
.cr{display:flex;align-items:center;gap:7px}
.csw{width:22px;height:22px;border-radius:3px;border:1px solid var(--border);cursor:pointer;overflow:hidden;position:relative;flex-shrink:0}
.csw input[type=color]{position:absolute;inset:-5px;opacity:0;cursor:pointer;width:150%;height:150%}
.hxi{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);color:var(--tx);font-family:'DM Mono',monospace;font-size:11px;padding:3px 6px;flex:1;outline:none}
.hxi:focus{border-color:var(--accent)}

/* ---- Main area ---- */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0}
.nav-bar{padding:6px 13px;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:7px;flex-shrink:0}
.nav-c{font-size:12px;color:var(--tx2);font-family:'DM Mono',monospace;min-width:44px;text-align:center}
.toolbar{padding:6px 13px;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:4px;flex-wrap:wrap;flex-shrink:0}
.tsep{width:1px;height:18px;background:var(--border);margin:0 3px;flex-shrink:0}

/* ============================================================ ALIGN BUTTONS (InDesign-style) */
.ag{display:flex;gap:1px;background:var(--surface3);border-radius:var(--r);padding:2px}
.ab{
  width:26px;height:24px;border-radius:3px;
  font-size:13px;cursor:pointer;border:none;
  background:transparent;color:var(--tx2);
  display:flex;align-items:center;justify-content:center;
  transition:all .1s;
}
.ab:hover{background:var(--surface);color:var(--tx)}
.ab.on{background:var(--surface);color:var(--accent);box-shadow:0 1px 2px rgba(0,0,0,.08)}
.ab svg{width:14px;height:14px;fill:currentColor}

/* ============================================================ CANVAS */
.cvp{flex:1;overflow:hidden;position:relative;background:var(--bg);cursor:default}
.cvp.pan-mode{cursor:grab}
.cvp.panning{cursor:grabbing !important}
.clayer{position:absolute;top:0;left:0;transform-origin:0 0;display:inline-block}
.zoom-box{position:absolute;bottom:14px;right:14px;display:flex;flex-direction:column;align-items:center;gap:3px;z-index:20}
.zb{width:26px;height:26px;border-radius:var(--r);background:var(--surface);border:1px solid var(--border);color:var(--tx2);font-size:15px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .12s}
.zb:hover{background:var(--surface2);color:var(--tx)}
.zlbl{font-size:10px;color:var(--tx3);font-family:'DM Mono',monospace}

/* ============================================================ UPLOAD */
.upzone{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:var(--bg)}
.upcard{background:var(--surface);border:2px dashed var(--border);border-radius:var(--r2);padding:52px 68px;display:flex;flex-direction:column;align-items:center;gap:13px;cursor:pointer;transition:all .18s;max-width:400px;width:90%;text-align:center}
.upcard:hover,.upcard.dov{border-color:var(--accent);background:var(--accent-bg)}
.up-ico{width:46px;height:46px;background:var(--surface2);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:20px}
.up-t{font-size:15px;font-weight:600}
.up-s{font-size:12px;color:var(--tx2);line-height:1.5}

/* ============================================================ MODE TOGGLE */
.mt{display:flex;background:var(--surface2);border-radius:var(--r);padding:2px;gap:2px}
.mb{padding:4px 10px;border-radius:3px;font-size:12px;font-weight:500;cursor:pointer;border:none;background:transparent;color:var(--tx2);transition:all .13s;display:flex;align-items:center;gap:5px;flex:1;justify-content:center}
.mb.on{background:var(--surface);color:var(--tx);box-shadow:0 1px 3px rgba(0,0,0,.08)}
.msw{width:9px;height:9px;border-radius:50%;border:1px solid rgba(0,0,0,.1)}
.mg{background:#D5D9D9}
.mp{background:#F0C8CA}

/* ============================================================
   EDIT TABLE — border-collapse:separate for zero double-border issues
   border-top + border-left on every cell.
   JS adds .no-left-border to first visible cell per row (no outer-left edge).
   JS adds .bottom-edge to last visible row cells (outer-bottom edge).
   Deleted cells → .deleted-cell (white, no border, no pointer-events, still occupy space).
   ============================================================ */
.tbl-wrap{
  position:relative;
  display:inline-block;
  background:#fff;
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}

.edit-tbl{
  border-collapse: separate !important;
  border-spacing: 0 !important;
  font-family:'Roboto',sans-serif;
  font-size:8pt;
  width:590px; /* <-- Geändert von 780px für exakt 156mm */
  table-layout:fixed;
  background:#fff;
  line-height:1.35;
  border: none !important;
}

/* Every cell: top + left border only */
.edit-tbl td, .edit-tbl th {
  padding:4px 6px;
  vertical-align:middle;
  text-align:left;
  position:relative;
  cursor:default;
  word-break:break-word;
  line-height:inherit;
  color:#1a1a1a;
  outline:none;
  min-width:24px;
  border: none !important;
  border-top: 0.6px solid var(--g-div) !important;
  border-left: 0.6px solid var(--g-div) !important;
}

/* Outer edge corrections (set via JS) */
.edit-tbl .no-left-border { border-left: none !important; }
.edit-tbl .bottom-edge { border-bottom: 0.6px solid var(--g-div) !important; }

/* Theming (overridden dynamically by injectColorStyle) */
.edit-tbl.mg td.ch, .edit-tbl.mg th { background:var(--g-hd) !important; font-weight:700; }
.edit-tbl.mg td.cn { background:var(--g-nd) !important; }
.edit-tbl.mp td.ch, .edit-tbl.mp th { background:var(--p-hd) !important; font-weight:700; }
.edit-tbl.mp td.cn { background:var(--p-nd) !important; }

/* Deleted cells — white, invisible, no pointer events — still occupy space */
#the-tbl td.deleted-cell, #the-tbl th.deleted-cell {
  background-color: #ffffff !important;
  color: transparent !important;
  border: none !important;
  box-shadow: none !important;
  pointer-events: none !important;
}

/* Alignment */
.edit-tbl .va-t { vertical-align:top !important; }
.edit-tbl .va-m { vertical-align:middle !important; }
.edit-tbl .va-b { vertical-align:bottom !important; }
.edit-tbl .ta-l { text-align:left !important; }
.edit-tbl .ta-c { text-align:center !important; }
.edit-tbl .ta-r { text-align:right !important; }

/* Bullet point fix */
.edit-tbl ul { margin: 0 !important; padding: 0 !important; list-style-type: none !important; }
.edit-tbl ul li { margin: 0 !important; padding: 0 0 0 8px !important; position: relative !important; }
.edit-tbl ul li::before { content: "•" !important; position: absolute !important; left: 0px !important; top: 0 !important; font-family: Arial, sans-serif !important; }
.edit-tbl ol { margin: 0 0 0 16px !important; padding: 0 !important; }
.edit-tbl ol li { margin: 0 !important; padding: 0 0 0 4px !important; list-style-position: outside !important; }

/* Selection / editing */
.edit-tbl td.sel,.edit-tbl th.sel { box-shadow:inset 0 0 0 2px var(--accent);z-index:2; }
.edit-tbl td.edt,.edit-tbl th.edt { box-shadow:inset 0 0 0 2px #E8A000;z-index:3;cursor:text; }

/* Resize handle */
.rhdl{position:absolute;right:-3px;top:0;bottom:0;width:6px;cursor:col-resize;z-index:10;background:transparent;pointer-events:auto;}
.rhdl:hover,.rhdl.on{background:rgba(47,110,235,.4)}

/* ============================================================ MODAL */
.mov{position:fixed;inset:0;background:rgba(0,0,0,.32);backdrop-filter:blur(3px);display:flex;align-items:center;justify-content:center;z-index:9999;opacity:0;pointer-events:none;transition:opacity .18s}
.mov.open{opacity:1;pointer-events:all}
.modal{background:var(--surface);border:1px solid var(--border);border-radius:var(--r2);padding:22px;max-width:380px;width:90%;display:flex;flex-direction:column;gap:12px;box-shadow:0 8px 30px rgba(0,0,0,.1);transform:translateY(6px);transition:transform .18s}
.mov.open .modal{transform:translateY(0)}
.modal-t{font-size:15px;font-weight:600}
.modal-s{font-size:13px;color:var(--tx2);line-height:1.5}
.modal-a{display:flex;gap:7px;justify-content:flex-end}
.pw{background:var(--surface3);border-radius:100px;height:4px;overflow:hidden}
.pf{height:100%;background:var(--accent);border-radius:100px;transition:width .22s}

/* ============================================================ TOAST */
.toast{position:fixed;bottom:16px;right:16px;background:var(--tx);color:var(--surface);border-radius:var(--r2);padding:8px 14px;font-size:12px;z-index:9999;opacity:0;transform:translateY(5px);transition:all .2s;pointer-events:none;max-width:300px}
.toast.show{opacity:1;transform:translateY(0)}

/* misc */
.sp{flex:1}
.em{font-size:12px;color:var(--tx3);line-height:1.6}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border);border-radius:3px}
::-webkit-scrollbar-thumb:hover{background:var(--border2)}
.hint{font-size:11px;color:var(--tx3);margin-left:4px}
</style>
</head>
<body>

<header>
  <div class="logo">coretable
    <span class="badge" id="tbl-count" style="display:none">0 tables</span>
  </div>
  <div class="hdr-r">
    <button class="btn btn-g" id="btn-new">⊕ New File</button>
    <button class="btn btn-g" id="btn-exp-all">↓ Export All</button>
    <button class="btn btn-p" id="btn-exp-cur">↓ Export This</button>
  </div>
</header>

<div class="body">

<div class="sb">
  <div class="sb-top">
    <div class="sb-lbl">Tables</div>
    <div class="mt" id="mode-toggle">
      <button class="mb on" id="mb-g" onclick="setMode('gray')"><span class="msw mg"></span>Gray</button>
      <button class="mb"    id="mb-p" onclick="setMode('pink')"><span class="msw mp"></span>Pink</button>
    </div>
  </div>
  <div class="tbl-list" id="tbl-list">
    <div class="em" id="sb-empty" style="padding:12px 10px">Upload an HTML file to begin.</div>
  </div>
</div>

<div class="main">

  <div class="nav-bar" id="nav-bar" style="display:none">
    <button class="btn btn-g" id="btn-prev">← Prev</button>
    <span class="nav-c" id="nav-c">1 / 1</span>
    <button class="btn btn-g" id="btn-next">Next →</button>
    <span class="sp"></span>
    <span style="font-size:11px;color:var(--tx3);max-width:180px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap" id="tbl-lbl"></span>
    <button class="btn btn-d" id="btn-reset">↺ Reset</button>
  </div>

  <div class="toolbar" id="toolbar" style="display:none">

    <button class="btn btn-g" id="btn-head">☰ Header</button>
    <button class="btn btn-g" id="btn-norm">☰ Normal</button>
    <div class="tsep"></div>

    <div class="ag" title="Vertical alignment">
      <button class="ab" id="va-t" onclick="setVA('t')" title="Align top">
        <svg viewBox="0 0 14 14"><rect x="1" y="1" width="12" height="1.5" rx=".75"/><rect x="3" y="4" width="8" height="1.5" rx=".75"/><rect x="3" y="7" width="8" height="1.5" rx=".75"/></svg>
      </button>
      <button class="ab on" id="va-m" onclick="setVA('m')" title="Align middle">
        <svg viewBox="0 0 14 14"><rect x="3" y="2" width="8" height="1.5" rx=".75"/><rect x="1" y="6.25" width="12" height="1.5" rx=".75"/><rect x="3" y="10.5" width="8" height="1.5" rx=".75"/></svg>
      </button>
      <button class="ab" id="va-b" onclick="setVA('b')" title="Align bottom">
        <svg viewBox="0 0 14 14"><rect x="3" y="5" width="8" height="1.5" rx=".75"/><rect x="3" y="8" width="8" height="1.5" rx=".75"/><rect x="1" y="11.5" width="12" height="1.5" rx=".75"/></svg>
      </button>
    </div>

    <div class="ag" title="Text alignment">
      <button class="ab on" id="ta-l" onclick="setTA('l')" title="Align left">
        <svg viewBox="0 0 14 14"><rect x="1" y="2" width="12" height="1.5" rx=".75"/><rect x="1" y="5.5" width="9" height="1.5" rx=".75"/><rect x="1" y="9" width="12" height="1.5" rx=".75"/><rect x="1" y="12" width="7" height="1.5" rx=".75"/></svg>
      </button>
      <button class="ab" id="ta-c" onclick="setTA('c')" title="Align center">
        <svg viewBox="0 0 14 14"><rect x="1" y="2" width="12" height="1.5" rx=".75"/><rect x="2.5" y="5.5" width="9" height="1.5" rx=".75"/><rect x="1" y="9" width="12" height="1.5" rx=".75"/><rect x="3.5" y="12" width="7" height="1.5" rx=".75"/></svg>
      </button>
      <button class="ab" id="ta-r" onclick="setTA('r')" title="Align right">
        <svg viewBox="0 0 14 14"><rect x="1" y="2" width="12" height="1.5" rx=".75"/><rect x="4" y="5.5" width="9" height="1.5" rx=".75"/><rect x="1" y="9" width="12" height="1.5" rx=".75"/><rect x="6" y="12" width="7" height="1.5" rx=".75"/></svg>
      </button>
    </div>

    <div class="tsep"></div>
    <button class="btn btn-g" id="btn-del" title="Hide selected cell(s) — maintains table structure">✕ Delete Cell</button>
    <button class="btn btn-g" id="btn-merge">⊞ Merge</button>
    <button class="btn btn-g" id="btn-unmerge">⊡ Unmerge</button>
    <div class="tsep"></div>
    <button class="btn btn-g" id="btn-clean" title="Remove empty leading cells">⊘ Clean Empty</button>
    <span class="hint">Dbl-click to edit text</span>
  </div>

  <div class="cvp" id="cvp">
    <div class="upzone" id="upzone">
      <div class="upcard" id="upcard">
        <div class="up-ico">📄</div>
        <div class="up-t">Drop HTML file here</div>
        <div class="up-s">or click to browse — tables extracted automatically</div>
        <button class="btn btn-p" style="margin-top:4px">Choose File</button>
      </div>
    </div>

    <div class="clayer" id="clayer" style="display:none">
      <div class="tbl-wrap" id="tbl-wrap"></div>
    </div>

    <div class="zoom-box" id="zoom-box" style="display:none">
      <button class="zb" onclick="doZoom(1.2)">+</button>
      <div class="zlbl" id="zlbl">100%</div>
      <button class="zb" onclick="doZoom(1/1.2)">−</button>
      <button class="zb" title="Fit to screen" onclick="zoomFit()">⊡</button>
    </div>
  </div>

</div><div class="panel">

  <div class="ps">
    <div class="pt">Spacing</div>
    <div class="fld">
      <div class="fl">Cell padding vertical (px)</div>
      <div class="fr"><input type="range" min="0" max="20" value="4" id="pv-r" oninput="onPad()"><input type="number" class="ni" value="4" id="pv-n" min="0" max="20" oninput="onPad()"></div>
    </div>
    <div class="fld">
      <div class="fl">Cell padding horizontal (px)</div>
      <div class="fr"><input type="range" min="0" max="30" value="6" id="ph-r" oninput="onPad()"><input type="number" class="ni" value="6" id="ph-n" min="0" max="30" oninput="onPad()"></div>
    </div>
    <div class="fld">
      <div class="fl">Font size (pt)</div>
      <div class="fr"><input type="range" min="5" max="16" value="8" step="0.5" id="fs-r" oninput="onFS()"><input type="number" class="ni" value="8" id="fs-n" min="5" max="16" step="0.5" oninput="onFS()"></div>
    </div>
    <div class="fld">
      <div class="fl">Line height</div>
      <div class="fr"><input type="range" min="1" max="2.5" value="1.35" step="0.05" id="lh-r" oninput="onLH()"><input type="number" class="ni" value="1.35" id="lh-n" min="1" max="2.5" step="0.05" oninput="onLH()"></div>
    </div>
  </div>

  <div class="ps">
    <div class="pt">Column Width</div>
    <div class="fld">
      <div class="fl">Selected column (px)</div>
      <div class="fr">
        <input type="number" class="ni" id="col-w" placeholder="auto" style="width:68px" oninput="applyColW()">
        <button class="btn btn-g" style="font-size:11px;padding:3px 8px" onclick="resetColW()">Auto</button>
      </div>
    </div>
  </div>

  <div class="ps">
    <div class="pt">Colour Overrides</div>
    <div class="fld">
      <div class="fl">Header cell</div>
      <div class="cr"><div class="csw" id="sw-dark"><input type="color" id="ci-dark" oninput="onCI('dark',this.value)"></div><input class="hxi" id="hx-dark" maxlength="7" oninput="onHX('dark',this.value)"></div>
    </div>
    <div class="fld">
      <div class="fl">Normal cell</div>
      <div class="cr"><div class="csw" id="sw-light"><input type="color" id="ci-light" oninput="onCI('light',this.value)"></div><input class="hxi" id="hx-light" maxlength="7" oninput="onHX('light',this.value)"></div>
    </div>
    <div class="fld">
      <div class="fl">Divider lines</div>
      <div class="cr"><div class="csw" id="sw-div"><input type="color" id="ci-div" oninput="onCI('div',this.value)"></div><input class="hxi" id="hx-div" maxlength="7" oninput="onHX('div',this.value)"></div>
    </div>
    <button class="btn btn-g" style="width:100%;font-size:11px;margin-top:3px" onclick="resetColors()">↺ Reset to mode defaults</button>
  </div>

  <div class="ps">
    <div class="pt">Selection</div>
    <div id="sel-info" class="em">Click a cell to select.<br>Shift+click for multi-select.</div>
  </div>

</div>
</div><div class="mov" id="exp-modal">
  <div class="modal">
    <div class="modal-t">Export as PNG</div>
    <div class="modal-s">
      Output: <strong>156 mm × 300 DPI</strong> = 1843 px wide. Roboto font, zero margin.<br>
      Multiple tables are bundled into a <strong>.zip</strong> file.
    </div>
    <div class="pw" id="exp-pw" style="display:none"><div class="pf" id="exp-pf" style="width:0"></div></div>
    <div id="exp-st" style="font-size:12px;color:var(--tx2);min-height:16px"></div>
    <div class="modal-a">
      <button class="btn btn-g" onclick="closeModal()">Cancel</button>
      <button class="btn btn-p" id="exp-go">Choose Save Location & Export</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
'use strict';

/* ============================================================
   CONSTANTS
   ============================================================ */
const EXPORT_PX = Math.round(156 * 300 / 25.4); // 1843px @ 300 DPI / 156mm

const CDEF = {
  gray: { dark:'#EEF0F0', light:'#F9F9F9', div:'#BCC1C2' },
  pink: { dark:'#F9E3E4', light:'#FEFAFB', div:'#DA7B7B' }
};

/* ============================================================
   STATE
   ============================================================ */
let tables    = [];   // { id, title, originalRows, rows, mode }
let tblStates = [];   // { padV, padH, fontSize, lh, colWidths, colorOv }
let curIdx    = 0;
let selCells  = new Set();
let editTd    = null;
let expMode   = 'current';

let scale = 1, panX = 60, panY = 60;
let isPanning = false, panSX = 0, panSY = 0, spaceDown = false;

function mkState(){
  return { padV:4, padH:6, fontSize:8, lh:1.35, colWidths:{}, colorOv:null };
}

/* ============================================================
   UPLOAD
   ============================================================ */
const fileIn = Object.assign(document.createElement('input'), {type:'file', accept:'.html,.htm'});
fileIn.style.display='none';
document.body.appendChild(fileIn);

['upcard','btn-new'].forEach(id =>
  document.getElementById(id).addEventListener('click', ()=>fileIn.click())
);
fileIn.addEventListener('change', e=>{
  if(e.target.files[0]) readFile(e.target.files[0]);
  fileIn.value='';
});
const uCard = document.getElementById('upcard');
uCard.addEventListener('dragover',  e=>{ e.preventDefault(); uCard.classList.add('dov'); });
uCard.addEventListener('dragleave', ()=>uCard.classList.remove('dov'));
uCard.addEventListener('drop', e=>{
  e.preventDefault(); uCard.classList.remove('dov');
  if(e.dataTransfer.files[0]) readFile(e.dataTransfer.files[0]);
});

function readFile(f){ const r=new FileReader(); r.onload=e=>parseHTML(e.target.result); r.readAsText(f); }

/* ============================================================
   PARSE — with bold-class detection from source CSS
   ============================================================ */
function parseHTML(html){
  const doc = new DOMParser().parseFromString(html, 'text/html');

  // Detect bold classes from source CSS
  let boldClasses = new Set();
  doc.querySelectorAll('style').forEach(styleTag => {
    const blocks = styleTag.textContent.split('}');
    blocks.forEach(block => {
      if(block.match(/font-weight\s*:\s*(bold|700|800|900)/i)){
        const selectors = block.split('{')[0];
        const classMatches = selectors.match(/\.([a-zA-Z0-9_-]+)/g);
        if(classMatches) classMatches.forEach(cls => boldClasses.add(cls.substring(1)));
      }
    });
  });

  // Wrap bold elements in <strong>
  doc.querySelectorAll('*').forEach(el => {
    if(['STRONG','B','TH','H1','H2','H3','H4','H5','H6'].includes(el.tagName)) return;
    let isBold = false;
    if(el.style && (el.style.fontWeight === 'bold' || parseInt(el.style.fontWeight) >= 700)){
      isBold = true;
    } else {
      for(const cls of el.classList){
        if(boldClasses.has(cls)){ isBold = true; break; }
      }
    }
    if(isBold && !el.querySelector('td,th,tr,tbody,table')){
      const str = doc.createElement('strong');
      str.innerHTML = el.innerHTML;
      el.innerHTML = '';
      el.appendChild(str);
    }
  });

  const rawTables = doc.querySelectorAll('table');
  if(!rawTables.length){ showToast('No tables found.'); return; }

  tables=[]; tblStates=[];

  rawTables.forEach((t,i)=>{
    const rows = extractRows(t);
    if(rows.length > 0){
      ensureHeaderRow(rows);
      tables.push({
        id:i,
        title: guessTitle(t,i),
        originalRows: deepClone(rows),
        rows,
        mode: 'gray'
      });
      tblStates.push(mkState());
    }
  });

  if(!tables.length){ showToast('All tables empty.'); return; }
  curIdx=0;
  showEditor();
  renderTable();
  renderSidebar();
  zoomFit();
  showToast(`${tables.length} table${tables.length>1?'s':''} extracted.`);
}

function guessTitle(tbl,i){
  const cap = tbl.querySelector('caption');
  if(cap && cap.textContent.trim()) return cap.textContent.trim().slice(0,55);
  let el = tbl.previousElementSibling;
  while(el){
    const txt = el.textContent.trim();
    if(/^H[1-6]$/.test(el.tagName) && txt) return txt.slice(0,55);
    if(txt) break;
    el = el.previousElementSibling;
  }
  const th = tbl.querySelector('th');
  if(th && th.textContent.trim()) return `Table ${i+1}: ${th.textContent.trim().slice(0,35)}`;
  return `Table ${i+1}`;
}

function extractRows(tbl){
  const grid=[], occ=new Set();
  tbl.querySelectorAll('tr').forEach((tr,ri)=>{
    if(!grid[ri]) grid[ri]=[];
    let ci=0;
    tr.querySelectorAll('td,th').forEach(cell=>{
      while(occ.has(`${ri},${ci}`)) ci++;
      const cs=Math.max(1,parseInt(cell.getAttribute('colspan')||'1'));
      const rs=Math.max(1,parseInt(cell.getAttribute('rowspan')||'1'));
      grid[ri][ci]={
        content: cleanHTML(cell.innerHTML),
        isHead:  cell.tagName==='TH',
        colspan:cs, rowspan:rs,
        deleted:false, width:null,
        va:null, ta:null
      };
      occ.add(`${ri},${ci}`);
      for(let r=0;r<rs;r++) for(let c=0;c<cs;c++){
        if(r===0&&c===0) continue;
        if(!grid[ri+r]) grid[ri+r]=[];
        grid[ri+r][ci+c]=null;
        occ.add(`${ri+r},${ci+c}`);
      }
      ci+=cs;
    });
  });
  while(grid.length && (!grid[grid.length-1]||grid[grid.length-1].every(c=>!c))) grid.pop();
  return grid;
}

function cleanHTML(html){
  const tmp = document.createElement('div');
  tmp.innerHTML = html;

  tmp.querySelectorAll('*').forEach(el => {
    el.removeAttribute('style'); el.removeAttribute('class'); el.removeAttribute('id');
    el.removeAttribute('width'); el.removeAttribute('height'); el.removeAttribute('border');
    el.removeAttribute('cellpadding'); el.removeAttribute('cellspacing');
  });

  const KEEP = new Set(['strong','b','em','i','u','br','sup','sub','ul','ol','li','span']);
  const elements = Array.from(tmp.querySelectorAll('*')).reverse();
  for(const el of elements){
    if(!el.parentNode) continue;
    const tag = el.tagName.toLowerCase();
    if(!KEEP.has(tag)){
      while(el.firstChild) el.parentNode.insertBefore(el.firstChild, el);
      el.remove();
    }
  }
  return tmp.innerHTML.trim();
}

function ensureHeaderRow(rows){ if(rows[0]) rows[0].forEach(c=>{ if(c) c.isHead=true; }); }
function deepClone(rows){ return rows.map(row=>row ? row.map(c=>c ? {...c} : null) : null); }

/* ============================================================
   SIDEBAR — with per-table color-theme dot
   ============================================================ */
function renderSidebar(){
  try {
    const list = document.getElementById('tbl-list');
    if(!list) return;
    list.innerHTML = '';
    const emptyMsg = document.getElementById('sb-empty');
    if(emptyMsg) emptyMsg.style.display = 'none';

    tables.forEach((t,i)=>{
      const vr = t.rows.filter(r=>r&&r.some(c=>c&&!c.deleted));
      const vc = vr[0] ? vr[0].filter(c=>c&&!c.deleted).length : 0;
      const el = document.createElement('div');
      el.className = 'tbl-item'+(i===curIdx?' active':'');

      // Color dot reflects current theme
      const dotColor = t.mode==='pink' ? '#DA7B7B' : '#BCC1C2';
      const dot = `<span style="display:inline-block;width:7px;height:7px;border-radius:50%;background:${dotColor};margin-right:3px;flex-shrink:0;border:1px solid rgba(0,0,0,.08)"></span>`;

      el.innerHTML = `<span class="tbl-item-n">${esc(String(t.title||`Table ${i+1}`))}</span>
                      <span class="tbl-item-b">${dot}${vr.length}×${vc}</span>`;
      el.addEventListener('click', ()=>switchTable(i));
      list.appendChild(el);
    });

    const badge = document.getElementById('tbl-count');
    if(badge){
      badge.textContent = `${tables.length} table${tables.length!==1?'s':''}`;
      badge.style.display = tables.length ? '' : 'none';
    }
  } catch(err){ console.error('Sidebar error:', err); }
}

function refreshSidebarActive(){
  document.querySelectorAll('.tbl-item').forEach((el,i)=>el.classList.toggle('active',i===curIdx));
}

/* ============================================================
   SHOW EDITOR
   ============================================================ */
function showEditor(){
  document.getElementById('upzone').style.display    = 'none';
  document.getElementById('clayer').style.display    = '';
  document.getElementById('nav-bar').style.display   = tables.length>1?'flex':'none';
  document.getElementById('toolbar').style.display   = 'flex';
  document.getElementById('zoom-box').style.display  = 'flex';
}

/* ============================================================
   RENDER TABLE — smart border logic via getMasterCell
   ============================================================ */

// Returns the master cell that controls a given [r,c] slot
// (handles null slots from rowspan/colspan)
function getMasterCell(t, r, c){
  if(!t.rows[r] || t.rows[r][c] === undefined) return null;
  if(t.rows[r][c] !== null) return t.rows[r][c];
  for(let ir=r; ir>=0; ir--){
    for(let ic=c; ic>=0; ic--){
      const cell = t.rows[ir] && t.rows[ir][ic];
      if(cell && cell !== null){
        if(ir + (cell.rowspan||1) > r && ic + (cell.colspan||1) > c) return cell;
      }
    }
  }
  return null;
}

function renderTable(){
  selCells.clear();
  updateSelInfo();

  const t=tables[curIdx], s=tblStates[curIdx];
  if(!t||!s) return;

  document.getElementById('nav-c').textContent   = `${curIdx+1} / ${tables.length}`;
  document.getElementById('tbl-lbl').textContent = t.title;
  document.getElementById('mb-g').classList.toggle('on', t.mode==='gray');
  document.getElementById('mb-p').classList.toggle('on', t.mode==='pink');

  const wrap=document.getElementById('tbl-wrap');
  wrap.innerHTML='';

  const tbl=document.createElement('table');
  tbl.className=`edit-tbl m${t.mode==='pink'?'p':'g'}`;
  tbl.id='the-tbl';
  tbl.style.fontSize  = s.fontSize+'pt';
  tbl.style.lineHeight= s.lh;

  injectColorStyle(s, t.mode);

  t.rows.forEach((row,ri)=>{
    if(!row) return;
    const tr=document.createElement('tr');

    row.forEach((cell,ci)=>{
      if(cell===null||cell===undefined) return; // spanned slot, skip

      const td=document.createElement(cell.isHead?'th':'td');
      let cls = cell.isHead?'ch':'cn';

      if(cell.deleted){
        cls += ' deleted-cell';
      } else {
        // No left border for leftmost visible cell in this row
        let leftEmpty = true;
        for(let c=0; c<ci; c++){
          const m = getMasterCell(t, ri, c);
          if(m && !m.deleted){ leftEmpty = false; break; }
        }
        if(leftEmpty) cls += ' no-left-border';

        // Bottom border for bottommost visible cells in this column
        let bottomEmpty = true;
        for(let r = ri + (cell.rowspan||1); r < t.rows.length; r++){
          const m = getMasterCell(t, r, ci);
          if(m && !m.deleted){ bottomEmpty = false; break; }
        }
        if(bottomEmpty) cls += ' bottom-edge';

        if(cell.va) cls += ' va-'+cell.va;
        if(cell.ta) cls += ' ta-'+cell.ta;
      }

      td.className  = cls;
      td.dataset.r  = ri;
      td.dataset.c  = ci;
      td.innerHTML  = cell.content;
      td.style.padding = `${s.padV}px ${s.padH}px`;
      if(cell.width) td.style.width = cell.width+'px';
      if(cell.colspan>1) td.setAttribute('colspan', cell.colspan);
      if(cell.rowspan>1) td.setAttribute('rowspan', cell.rowspan);

      const hdl=document.createElement('div');
      hdl.className='rhdl';
      hdl.addEventListener('mousedown', e=>startResize(e,ri,ci));
      td.appendChild(hdl);

      td.addEventListener('click',    onCellClick);
      td.addEventListener('dblclick', onCellDblClick);
      tr.appendChild(td);
    });

    if(tr.childElementCount>0) tbl.appendChild(tr);
  });

  wrap.appendChild(tbl);
  updatePanelInputs(s);
}

/* ---- Dynamic colour injection ---- */
function injectColorStyle(s, mode){
  let el=document.getElementById('_tcs');
  if(!el){ el=document.createElement('style'); el.id='_tcs'; document.head.appendChild(el); }

  const d=CDEF[mode||'gray'];
  const ov=s.colorOv||{};
  const drk=ov.dark||d.dark, lgt=ov.light||d.light, div=ov.div||d.div;

  el.textContent=`
    #the-tbl td, #the-tbl th {
      border-top-color: ${div} !important;
      border-left-color: ${div} !important;
    }
    #the-tbl .bottom-edge {
      border-bottom-color: ${div} !important;
    }
    #the-tbl td.ch, #the-tbl th { background-color: ${drk} !important; }
    #the-tbl td.cn { background-color: ${lgt} !important; }
    table.edit-tbl td.deleted-cell, table.edit-tbl th.deleted-cell,
    #the-tbl td.deleted-cell, #the-tbl th.deleted-cell {
      background-color: #ffffff !important;
      color: transparent !important;
      border: none !important;
      box-shadow: none !important;
      pointer-events: none !important;
    }
  `;

  syncCUI('dark',drk); syncCUI('light',lgt); syncCUI('div',div);
}

function syncCUI(key,hex){
  const ci=document.getElementById(`ci-${key}`);
  const sw=document.getElementById(`sw-${key}`);
  const hx=document.getElementById(`hx-${key}`);
  if(ci) ci.value=hex; if(sw) sw.style.background=hex; if(hx) hx.value=hex;
}

function updatePanelInputs(s){
  sRN('pv',s.padV); sRN('ph',s.padH); sRN('fs',s.fontSize); sRN('lh',s.lh);
}
function sRN(id,val){
  const r=document.getElementById(id+'-r'), n=document.getElementById(id+'-n');
  if(r) r.value=val; if(n) n.value=val;
}

/* ============================================================
   CELL EVENTS
   ============================================================ */
function onCellClick(e){
  if(e.target.classList.contains('rhdl')) return;
  if(e.currentTarget.classList.contains('deleted-cell')){ selCells.clear(); reRender(); return; }
  e.stopPropagation();
  const key=`${e.currentTarget.dataset.r},${e.currentTarget.dataset.c}`;
  if(e.shiftKey||e.ctrlKey||e.metaKey){
    selCells.has(key)?selCells.delete(key):selCells.add(key);
  } else {
    selCells.clear(); selCells.add(key);
    document.getElementById('col-w').value=Math.round(e.currentTarget.offsetWidth)||'';
  }
  refreshHL(); updateSelInfo();
}

function onCellDblClick(e){
  if(e.target.classList.contains('rhdl')) return;
  if(e.currentTarget.classList.contains('deleted-cell')) return;
  const td=e.currentTarget;
  if(editTd&&editTd!==td) commitEdit(editTd);
  td.contentEditable='true'; td.classList.add('edt'); td.focus();
  try{
    const rng=document.createRange(); rng.selectNodeContents(td); rng.collapse(false);
    const sel=window.getSelection(); sel.removeAllRanges(); sel.addRange(rng);
  }catch(_){}
  editTd=td;
}

function commitEdit(td){
  if(!td) return;
  td.contentEditable='false'; td.classList.remove('edt');
  const c=tables[curIdx]?.rows?.[td.dataset.r]?.[td.dataset.c];
  if(c){ const cl=td.cloneNode(true); cl.querySelectorAll('.rhdl').forEach(h=>h.remove()); c.content=cl.innerHTML.trim(); }
  if(editTd===td) editTd=null;
}

// Click outside table → deselect
document.body.addEventListener('click', e=>{
  if(!tables.length) return;
  if(!e.target.closest('#the-tbl') && !e.target.closest('.toolbar') && !e.target.closest('.panel')){
    if(selCells.size > 0){ selCells.clear(); reRender(); }
  }
});

function refreshHL(){
  document.getElementById('the-tbl')?.querySelectorAll('td,th').forEach(td=>{
    td.classList.toggle('sel', selCells.has(`${td.dataset.r},${td.dataset.c}`));
  });
}

function updateSelInfo(){
  const el=document.getElementById('sel-info');
  if(!selCells.size){ el.innerHTML='Click a cell to select.<br>Shift+click for multi-select.'; return; }
  const cells=selData();
  const hn=cells.filter(c=>c.isHead).length;
  el.innerHTML=`<strong style="color:var(--tx)">${selCells.size}</strong> cell${selCells.size>1?'s':''} — ${hn} header, ${cells.length-hn} normal`;
}

function selData(){
  return [...selCells].map(k=>{
    const [r,c]=k.split(',').map(Number);
    return tables[curIdx]?.rows?.[r]?.[c];
  }).filter(Boolean);
}

/* ============================================================
   KEYBOARD
   ============================================================ */
document.addEventListener('keydown', e=>{
  if(e.key===' '&&!editTd){ spaceDown=true; document.getElementById('cvp').classList.add('pan-mode'); e.preventDefault(); }
  if(editTd){ if(e.key==='Escape') commitEdit(editTd); return; }
  if(!tables.length) return;
  if(e.key==='ArrowLeft'&&curIdx>0){ curIdx--; switchTable(curIdx); }
  if(e.key==='ArrowRight'&&curIdx<tables.length-1){ curIdx++; switchTable(curIdx); }
  if((e.key==='Delete'||e.key==='Backspace')&&selCells.size){ e.preventDefault(); doDelete(); }
});
document.addEventListener('keyup', e=>{
  if(e.key===' '){ spaceDown=false; document.getElementById('cvp').classList.remove('pan-mode'); }
});

/* ============================================================
   TOOLBAR ACTIONS
   ============================================================ */
document.getElementById('btn-head').addEventListener('click', ()=>{ applyToSel(c=>c.isHead=true); reRender(); });
document.getElementById('btn-norm').addEventListener('click', ()=>{ applyToSel(c=>c.isHead=false); reRender(); });
document.getElementById('btn-del').addEventListener('click',  doDelete);
document.getElementById('btn-clean').addEventListener('click', doClean);
document.getElementById('btn-merge').addEventListener('click', doMerge);
document.getElementById('btn-unmerge').addEventListener('click', doUnmerge);

document.getElementById('btn-reset').addEventListener('click', ()=>{
  const t=tables[curIdx]; if(!t) return;
  if(!confirm(`Reset "${t.title}" to original? All edits will be lost.`)) return;
  if(editTd) commitEdit(editTd);
  t.rows=deepClone(t.originalRows);
  tblStates[curIdx]=mkState();
  selCells.clear(); editTd=null;
  document.getElementById('col-w').value='';
  renderTable(); renderSidebar(); zoomFit();
  showToast('Table reset to original.');
});

function setVA(va){
  applyToSel(c=>c.va=va);
  ['t','m','b'].forEach(v=>document.getElementById('va-'+v).classList.toggle('on',v===va));
  reRender();
}
function setTA(ta){
  applyToSel(c=>c.ta=ta);
  ['l','c','r'].forEach(v=>document.getElementById('ta-'+v).classList.toggle('on',v===ta));
  reRender();
}

function applyToSel(fn){
  selCells.forEach(k=>{
    const [r,c]=k.split(',').map(Number);
    const cell=tables[curIdx]?.rows?.[r]?.[c];
    if(cell) fn(cell);
  });
}

function doDelete(){
  applyToSel(c=>c.deleted=true);
  selCells.clear(); reRender();
}

function doClean(){
  const t=tables[curIdx]; if(!t) return;
  let n=0;
  t.rows.forEach(row=>{
    if(!row) return;
    for(let ci=0;ci<row.length;ci++){
      const c=row[ci];
      if(c===null||c===undefined||c.deleted) continue;
      if(stripTags(c.content||'').trim()===''){ c.deleted=true; n++; }
      break;
    }
  });
  selCells.clear(); reRender();
  showToast(n?`${n} empty cell${n>1?'s':''} removed.`:'No empty leading cells found.');
}

function doMerge(){
  if(selCells.size<2){ showToast('Select 2+ cells to merge.'); return; }
  const keys=[...selCells].map(k=>k.split(',').map(Number));
  const minR=Math.min(...keys.map(k=>k[0])), maxR=Math.max(...keys.map(k=>k[0]));
  const minC=Math.min(...keys.map(k=>k[1])), maxC=Math.max(...keys.map(k=>k[1]));
  const t=tables[curIdx];
  let content='';
  for(let r=minR;r<=maxR;r++) for(let c=minC;c<=maxC;c++){
    const cell=t?.rows?.[r]?.[c];
    if(!cell||cell.deleted) continue;
    if(r===minR&&c===minC){ content=cell.content; }
    else if(cell.content.trim()){ content+=' '+cell.content; }
  }
  const anchor=t.rows[minR]?.[minC]; if(!anchor) return;
  anchor.content=content.trim(); anchor.colspan=maxC-minC+1; anchor.rowspan=maxR-minR+1; anchor.deleted=false;
  for(let r=minR;r<=maxR;r++){
    if(!t.rows[r]) t.rows[r]=[];
    for(let c=minC;c<=maxC;c++){
      if(r===minR&&c===minC) continue;
      t.rows[r][c]=null;
    }
  }
  selCells.clear(); reRender();
}

function doUnmerge(){
  if(selCells.size!==1){ showToast('Select exactly one merged cell.'); return; }
  const [k]=[...selCells];
  const [r,c]=k.split(',').map(Number);
  const cell=tables[curIdx]?.rows?.[r]?.[c];
  if(!cell||(cell.colspan<=1&&cell.rowspan<=1)){ showToast('Cell is not merged.'); return; }
  const cs=cell.colspan, rs=cell.rowspan;
  cell.colspan=1; cell.rowspan=1;
  for(let rr=r;rr<r+rs;rr++){
    if(!tables[curIdx].rows[rr]) tables[curIdx].rows[rr]=[];
    for(let cc=c;cc<c+cs;cc++){
      if(rr===r&&cc===c) continue;
      tables[curIdx].rows[rr][cc]={content:'',isHead:false,colspan:1,rowspan:1,deleted:false,width:null,va:null,ta:null};
    }
  }
  selCells.clear(); reRender();
}

function reRender(){
  const sv=new Set(selCells);
  renderTable();
  sv.forEach(k=>selCells.add(k));
  refreshHL(); updateSelInfo();
}

/* ============================================================
   COLOR MODE — per table
   ============================================================ */
function setMode(m){
  const t=tables[curIdx]; if(!t) return;
  t.mode=m;
  document.getElementById('mb-g').classList.toggle('on',m==='gray');
  document.getElementById('mb-p').classList.toggle('on',m==='pink');
  renderTable();
  renderSidebar(); // update dot in sidebar
}

/* ============================================================
   NAV
   ============================================================ */
document.getElementById('btn-prev').addEventListener('click', ()=>{ if(curIdx>0) switchTable(curIdx-1); });
document.getElementById('btn-next').addEventListener('click', ()=>{ if(curIdx<tables.length-1) switchTable(curIdx+1); });

function switchTable(i){
  if(editTd) commitEdit(editTd);
  selCells.clear();
  curIdx=Math.max(0,Math.min(i,tables.length-1));
  renderTable();
  renderSidebar();
  zoomFit();
}

/* ============================================================
   PANEL CONTROLS
   ============================================================ */
function syncS(id){
  const r=document.getElementById(id+'-r'), n=document.getElementById(id+'-n');
  if(!r||!n) return;
  if(document.activeElement===r) n.value=r.value; else r.value=n.value;
}
function onPad(){
  syncS('pv'); syncS('ph');
  const s=tblStates[curIdx]; if(!s) return;
  s.padV=parseFloat(document.getElementById('pv-n').value)||0;
  s.padH=parseFloat(document.getElementById('ph-n').value)||0;
  renderTable();
}
function onFS(){
  syncS('fs');
  const s=tblStates[curIdx]; if(!s) return;
  s.fontSize=parseFloat(document.getElementById('fs-n').value)||8;
  const tbl=document.getElementById('the-tbl');
  if(tbl) tbl.style.fontSize=s.fontSize+'pt';
}
function onLH(){
  syncS('lh');
  const s=tblStates[curIdx]; if(!s) return;
  s.lh=parseFloat(document.getElementById('lh-n').value)||1.35;
  const tbl=document.getElementById('the-tbl');
  if(tbl) tbl.style.lineHeight=s.lh;
}

/* ============================================================
   COLUMN RESIZE — scale-aware
   ============================================================ */
let rsState=null;
function startResize(e,ri,ci){
  e.preventDefault(); e.stopPropagation();
  const td=e.currentTarget.parentElement;
  rsState={ci, sx:e.clientX, sw:td.offsetWidth};
  e.currentTarget.classList.add('on');
  const onMove=ev=>{
    if(!rsState) return;
    const w=Math.max(24, rsState.sw + (ev.clientX-rsState.sx)/scale);
    applyColWpx(rsState.ci, w);
    document.getElementById('col-w').value=Math.round(w);
  };
  const onUp=()=>{
    document.querySelectorAll('.rhdl.on').forEach(h=>h.classList.remove('on'));
    rsState=null;
    document.removeEventListener('mousemove',onMove);
    document.removeEventListener('mouseup',onUp);
  };
  document.addEventListener('mousemove',onMove);
  document.addEventListener('mouseup',onUp);
}
function applyColWpx(ci,w){
  tblStates[curIdx].colWidths[ci]=w;
  tables[curIdx]?.rows.forEach(r=>{ if(r&&r[ci]) r[ci].width=w; });
  document.getElementById('the-tbl')?.querySelectorAll(`[data-c="${ci}"]`).forEach(td=>td.style.width=w+'px');
  document.getElementById('col-w').value=Math.round(w);
}
function applyColW(){
  if(!selCells.size) return;
  const v=parseInt(document.getElementById('col-w').value);
  if(!v||isNaN(v)) return;
  applyColWpx(parseInt([...selCells][0].split(',')[1]),v);
}
function resetColW(){
  if(!selCells.size) return;
  const ci=parseInt([...selCells][0].split(',')[1]);
  tblStates[curIdx].colWidths[ci]=null;
  tables[curIdx]?.rows.forEach(r=>{ if(r&&r[ci]) r[ci].width=null; });
  document.getElementById('the-tbl')?.querySelectorAll(`[data-c="${ci}"]`).forEach(td=>td.style.width='');
  document.getElementById('col-w').value='';
}

/* ============================================================
   COLOUR OVERRIDES
   ============================================================ */
function onCI(key,val){
  document.getElementById(`hx-${key}`).value=val;
  document.getElementById(`sw-${key}`).style.background=val;
  saveOv(key,val);
}
function onHX(key,val){
  if(!/^#[0-9A-Fa-f]{6}$/.test(val)) return;
  document.getElementById(`ci-${key}`).value=val;
  document.getElementById(`sw-${key}`).style.background=val;
  saveOv(key,val);
}
function saveOv(key,val){
  const s=tblStates[curIdx]; if(!s) return;
  if(!s.colorOv) s.colorOv={};
  s.colorOv[key]=val;
  injectColorStyle(s, tables[curIdx]?.mode);
}
function resetColors(){
  const s=tblStates[curIdx]; if(!s) return;
  s.colorOv=null;
  injectColorStyle(s, tables[curIdx]?.mode);
}

/* ============================================================
   PAN & ZOOM
   ============================================================ */
const CVP   = document.getElementById('cvp');
const LAYER = document.getElementById('clayer');

function applyTF(){
  LAYER.style.transform=`translate(${panX}px,${panY}px) scale(${scale})`;
  document.getElementById('zlbl').textContent=Math.round(scale*100)+'%';
}
function doZoom(f,cx,cy){
  const r=CVP.getBoundingClientRect();
  const ox=cx!=null?cx-r.left:r.width/2, oy=cy!=null?cy-r.top:r.height/2;
  const ns=Math.max(.05,Math.min(6,scale*f));
  panX=ox-(ox-panX)*(ns/scale); panY=oy-(oy-panY)*(ns/scale); scale=ns; applyTF();
}
function zoomFit(){
  const wrap=document.getElementById('tbl-wrap');
  if(!wrap) return;
  const r=CVP.getBoundingClientRect();
  const tw=wrap.offsetWidth||780, th=wrap.offsetHeight||200;
  scale=Math.min(1,(r.width-80)/tw,(r.height-80)/th);
  panX=(r.width-tw*scale)/2; panY=(r.height-th*scale)/2; applyTF();
}

CVP.addEventListener('wheel', e=>{ e.preventDefault(); doZoom(e.deltaY<0?1.1:1/1.1,e.clientX,e.clientY); },{passive:false});
CVP.addEventListener('mousedown', e=>{
  if(e.button!==1&&!spaceDown&&e.target!==CVP&&e.target!==LAYER) return;
  isPanning=true; panSX=e.clientX-panX; panSY=e.clientY-panY;
  CVP.classList.add('panning'); e.preventDefault();
});
document.addEventListener('mousemove', e=>{ if(!isPanning) return; panX=e.clientX-panSX; panY=e.clientY-panSY; applyTF(); });
document.addEventListener('mouseup',   ()=>{ isPanning=false; CVP.classList.remove('panning'); });

/* ============================================================
   EXPORT
   ============================================================ */
function getTimestampPrefix() {
  const now = new Date();
  const yy = String(now.getFullYear()).slice(-2);
  const mm = String(now.getMonth() + 1).padStart(2, '0');
  const dd = String(now.getDate()).padStart(2, '0');
  const hh = String(now.getHours()).padStart(2, '0');
  const min = String(now.getMinutes()).padStart(2, '0');
  return `${yy}${mm}${dd}-${hh}-${min}-`;
}

document.getElementById('btn-exp-cur').addEventListener('click', ()=>{
  if(!tables.length){ showToast('No tables loaded.'); return; }
  expMode='current';
  document.getElementById('exp-st').textContent=`Export: "${tables[curIdx]?.title}"`;
  document.getElementById('exp-pw').style.display='none';
  document.getElementById('exp-modal').classList.add('open');
});
document.getElementById('btn-exp-all').addEventListener('click', ()=>{
  if(!tables.length){ showToast('No tables loaded.'); return; }
  expMode='all';
  document.getElementById('exp-st').textContent=`Will export all ${tables.length} tables as a .zip`;
  document.getElementById('exp-pw').style.display='none';
  document.getElementById('exp-modal').classList.add('open');
});
document.getElementById('exp-modal').addEventListener('click', e=>{ if(e.target===e.currentTarget) closeModal(); });
document.getElementById('exp-go').addEventListener('click', runExport);
function closeModal(){ document.getElementById('exp-modal').classList.remove('open'); }

/* Native File System Access API with fallback */
async function saveFileCustom(blob, defaultName){
  if(window.showSaveFilePicker){
    try{
      const handle=await window.showSaveFilePicker({
        suggestedName: defaultName,
        types:[{
          description: defaultName.endsWith('.zip')?'ZIP Archive':'PNG Image',
          accept: defaultName.endsWith('.zip')?{'application/zip':['.zip']}:{'image/png':['.png']},
        }],
      });
      const writable=await handle.createWritable();
      await writable.write(blob); await writable.close();
      return;
    }catch(err){
      if(err.name!=='AbortError') console.error('Save failed',err);
      return;
    }
  }
  // Fallback
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a'); a.href=url; a.download=defaultName;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  setTimeout(()=>URL.revokeObjectURL(url),1000);
}

async function runExport(){
  const btn=document.getElementById('exp-go');
  btn.disabled=true; btn.textContent='Rendering…';
  const idxs=expMode==='all'?tables.map((_,i)=>i):[curIdx];
  const pw=document.getElementById('exp-pw');
  const pf=document.getElementById('exp-pf');
  const st=document.getElementById('exp-st');
  pw.style.display='';

  if(idxs.length===1){
    st.textContent=`Rendering: ${tables[idxs[0]].title}`;
    pf.style.width='0%';
    try{
      const blob=await renderTableToPNG(idxs[0]);
      if(blob){
        pf.style.width='100%';
        st.textContent='Please pick save location…';
        await saveFileCustom(blob, getTimestampPrefix() + safeName(tables[idxs[0]].title, idxs[0]) + '.png');
        st.textContent='Done!';
      }
    }catch(err){ console.error(err); st.textContent='Error — see console.'; }
  } else {
    const zip=new JSZip();
    for(let i=0;i<idxs.length;i++){
      const idx=idxs[i];
      st.textContent=`Rendering ${i+1}/${idxs.length}: ${tables[idx].title}`;
      pf.style.width=`${Math.round(i/idxs.length*100)}%`;
      try{
        const blob=await renderTableToPNG(idx);
        if(blob) zip.file(getTimestampPrefix() + safeName(tables[idx].title,idx) + '.png', blob);
      }catch(err){ console.error('Error on table',idx,err); }
      await sleep(40);
    }
    pf.style.width='90%';
    st.textContent='Zipping…';
    const zipBlob=await zip.generateAsync({type:'blob',compression:'DEFLATE'});
    pf.style.width='100%';
    st.textContent='Please pick save location…';
    await saveFileCustom(zipBlob, getTimestampPrefix() + 'coretable-export.zip');
    st.textContent=`Done — ${idxs.length} tables exported.`;
  }

  btn.disabled=false; btn.textContent='Choose Save Location & Export';
  setTimeout(closeModal,2200);
}

/* ============================================================
   RENDER TABLE TO PNG — export uses same border logic as editor
   ============================================================ */
async function renderTableToPNG(idx){
  const t=tables[idx], s=tblStates[idx];
  const d=CDEF[t.mode||'gray'], ov=s.colorOv||{};
  const drk=ov.dark||d.dark, lgt=ov.light||d.light, div=ov.div||d.div;

  const host=document.createElement('div');
  host.className='xt-temp';
  host.style.cssText='position:fixed;left:-9999px;top:0;background:#ffffff;font-family:Roboto,sans-serif';

  const wrap=document.createElement('div');
  wrap.style.cssText='display:inline-block;background:#ffffff;';

  const tbl=document.createElement('table');
  tbl.style.fontSize=s.fontSize+'pt';
  tbl.style.lineHeight=s.lh;

  const disp=document.getElementById('the-tbl');
  const targetWidth=(idx===curIdx&&disp)?disp.offsetWidth:590; /* <-- 780 durch 590 ersetzt */
  tbl.style.width=targetWidth+'px';

  t.rows.forEach((row,ri)=>{
    if(!row) return;
    const tr=document.createElement('tr');
    row.forEach((cell,ci)=>{
      if(cell===null||cell===undefined) return;
      const td=document.createElement(cell.isHead?'th':'td');
      let cls=cell.isHead?'ch':'cn';

      if(cell.deleted){
        cls+=' deleted-cell';
      } else {
        let leftEmpty=true;
        for(let c=0;c<ci;c++){
          const m=getMasterCell(t,ri,c);
          if(m&&!m.deleted){ leftEmpty=false; break; }
        }
        if(leftEmpty) cls+=' no-left-border';

        let bottomEmpty=true;
        for(let r=ri+(cell.rowspan||1);r<t.rows.length;r++){
          const m=getMasterCell(t,r,ci);
          if(m&&!m.deleted){ bottomEmpty=false; break; }
        }
        if(bottomEmpty) cls+=' bottom-edge';

        if(cell.va) cls+=' va-'+cell.va;
        if(cell.ta) cls+=' ta-'+cell.ta;
      }

      td.className=cls;
      td.innerHTML=cell.content;
      td.style.padding=`${s.padV}px ${s.padH}px`;
      if(cell.width) td.style.width=cell.width+'px';
      if(cell.colspan>1) td.setAttribute('colspan',cell.colspan);
      if(cell.rowspan>1) td.setAttribute('rowspan',cell.rowspan);
      tr.appendChild(td);
    });
    if(tr.childElementCount>0) tbl.appendChild(tr);
  });

  wrap.appendChild(tbl);
  host.appendChild(wrap);

  // Export styles — identical border approach to editor
  const styleBlock=document.createElement('style');
  styleBlock.textContent=`
    .xt-temp table {
      border-collapse: separate !important; border-spacing: 0 !important;
      font-family:'Roboto',sans-serif; border: none !important;
      table-layout: fixed !important;
    }
    .xt-temp td, .xt-temp th {
      border: none !important;
      border-top: 0.6px solid ${div} !important;
      border-left: 0.6px solid ${div} !important;
      background-clip: padding-box;
      text-align: left;
    }
    .xt-temp .bottom-edge { border-bottom: 0.6px solid ${div} !important; }
    .xt-temp .no-left-border { border-left: none !important; }
    .xt-temp td.ch, .xt-temp th { background-color: ${drk} !important; font-weight: 700; }
    .xt-temp td.cn { background-color: ${lgt} !important; }
    .xt-temp td.deleted-cell, .xt-temp th.deleted-cell {
      background-color: #ffffff !important; color: transparent !important;
      border: none !important; box-shadow: none !important; pointer-events: none !important;
    }
    .xt-temp strong, .xt-temp b { font-weight: 700 !important; }
    .xt-temp .va-t { vertical-align:top !important; }
    .xt-temp .va-m { vertical-align:middle !important; }
    .xt-temp .va-b { vertical-align:bottom !important; }
    .xt-temp .ta-l { text-align:left !important; }
    .xt-temp .ta-c { text-align:center !important; }
    .xt-temp .ta-r { text-align:right !important; }
    .xt-temp ul { margin:0 !important; padding:0 !important; list-style-type:none !important; }
    .xt-temp ul li { margin:0 !important; padding:0 0 0 8px !important; position:relative !important; }
    .xt-temp ul li::before { content:"•" !important; position:absolute !important; left:0 !important; top:0 !important; font-family:Arial,sans-serif !important; }
    .xt-temp ol { margin:0 0 0 16px !important; padding:0 !important; }
    .xt-temp ol li { margin:0 !important; padding:0 0 0 4px !important; list-style-position:outside !important; }
  `;
  host.appendChild(styleBlock);
  document.body.appendChild(host);

  await sleep(150);
  try{ await document.fonts.ready; }catch(_){}

  const scaleFactor=EXPORT_PX/wrap.offsetWidth;
  const canvas=await html2canvas(wrap,{
    scale: scaleFactor,
    useCORS: true,
    backgroundColor: '#ffffff',
    logging: false
  });

  document.body.removeChild(host);
  return await new Promise(res=>canvas.toBlob(res,'image/png'));
}

/* ============================================================
   UTILITIES
   ============================================================ */
function safeName(title,idx){ return String(title).replace(/[^a-z0-9]/gi,'_').replace(/_+/g,'_').toLowerCase().slice(0,50)||`table_${idx+1}`; }
function stripTags(h){ const d=document.createElement('div'); d.innerHTML=h; return d.textContent||''; }
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }
function showToast(msg,dur=3200){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  clearTimeout(t._t); t._t=setTimeout(()=>t.classList.remove('show'),dur);
}

// Init
applyTF();
</script>
</body>
</html>
