import { useState, useMemo, useEffect, useRef } from "react";
import {
  ChevronRight, ChevronLeft, Bell, Plus, X,
  ExternalLink, ArrowLeft, BookOpen, Calendar,
  StickyNote, FileText, Link2, Wrench, Eye, Music, Trash2,
} from "lucide-react";

/* ─────────────────────────────────────────────
   FONTS & GLOBAL STYLE (injected once)
───────────────────────────────────────────── */
const GLOBAL_CSS = `
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400&family=Fira+Code:wght@400;500&family=Outfit:wght@300;400;500&display=swap');
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{-webkit-font-smoothing:antialiased}
body{background:#F6F4EE;min-height:100vh}
::-webkit-scrollbar{width:3px;height:3px}
::-webkit-scrollbar-thumb{background:#CCC9BF;border-radius:2px}
input[type=date]::-webkit-calendar-picker-indicator,
input[type=time]::-webkit-calendar-picker-indicator{opacity:.4;cursor:pointer}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.fade-up{animation:fadeUp .28s ease both}
`;

/* ─────────────────────────────────────────────
   DESIGN TOKENS
───────────────────────────────────────────── */
const T = {
  paper:  "#F6F4EE",
  surface:"#FFFFFE",
  ink:    "#1C1B17",
  mid:    "#6B6A63",
  muted:  "#A8A79F",
  line:   "#E8E5DB",
  hover:  "#F0EDE5",
  // fonts
  fd: "'Cormorant Garamond', Georgia, serif",
  fm: "'Fira Code', 'Courier New', monospace",
  fb: "'Outfit', system-ui, sans-serif",
};

/* ─────────────────────────────────────────────
   CATEGORY DEFINITIONS (monochrome steps)
───────────────────────────────────────────── */
const CATS = [
  { id:"live",      label:"本番・ライブ",  bg:"#1C1B17", fg:"#F6F4EE", dot:"#1C1B17" },
  { id:"rehearsal", label:"リハーサル",    bg:"#454540", fg:"#F6F4EE", dot:"#454540" },
  { id:"admin",     label:"事務・申請",    bg:"#7A7971", fg:"#F6F4EE", dot:"#7A7971" },
  { id:"meeting",   label:"ミーティング",  bg:"#B3B1A8", fg:"#1C1B17", dot:"#B3B1A8" },
  { id:"other",     label:"その他",        bg:"#D9D7CE", fg:"#1C1B17", dot:"#D9D7CE" },
];
const getCat = id => CATS.find(c => c.id === id) ?? CATS[4];

/* ─────────────────────────────────────────────
   DATE HELPERS
───────────────────────────────────────────── */
// Fiscal period: Sep 2025 → Nov 2026  (15 months)
const FISCAL = (() => {
  const r = []; let y = 2025, m = 8;
  while (y < 2026 || (y === 2026 && m <= 10)) {
    r.push({ year: y, month: m });
    m === 11 ? (y++, m = 0) : m++;
  }
  return r;
})();

const M_EN  = ["January","February","March","April","May","June","July","August","September","October","November","December"];
const M_JA  = ["1月","2月","3月","4月","5月","6月","7月","8月","9月","10月","11月","12月"];
const DOW   = ["日","月","火","水","木","金","土"];

const MOCK_TODAY = new Date(2026, 3, 15);
const pad    = n => String(n).padStart(2, "0");
const toKey  = (y, m, d) => `${y}-${pad(m+1)}-${pad(d)}`;
const daysIn = (y, m) => new Date(y, m+1, 0).getDate();
const wd1st  = (y, m) => new Date(y, m, 1).getDay();
const TODAY  = toKey(MOCK_TODAY.getFullYear(), MOCK_TODAY.getMonth(), MOCK_TODAY.getDate());
const away   = s => { const a=new Date(MOCK_TODAY);a.setHours(0,0,0,0);const b=new Date(s);b.setHours(0,0,0,0);return Math.round((b-a)/864e5); };

let _id = 100;
const uid = () => `e${++_id}`;

/* ─────────────────────────────────────────────
   SEED EVENTS  (2025.9 – 2026.11)
───────────────────────────────────────────── */
const SEED = [
  {id:"s1",  title:"前期合宿",               startDate:"2025-09-04", endDate:"2025-09-06", time:"",    content:"場所：軽井沢　年間方針決め・新入生歓迎",       category:"other"},
  {id:"s2",  title:"秋ライブ 出欠1次申請",   startDate:"2025-09-15", endDate:"2025-09-22", time:"",    content:"Googleフォームにて各自回答",                     category:"admin"},
  {id:"s3",  title:"セトリ案 提出締切",      startDate:"2025-10-07", endDate:"2025-10-07", time:"23:59",content:"連絡班へメール送付",                            category:"admin"},
  {id:"s4",  title:"秋ライブ リハーサル",    startDate:"2025-10-18", endDate:"2025-10-26", time:"14:00",content:"週末のみ実施 · スタジオA",                      category:"rehearsal"},
  {id:"s5",  title:"設営・音響チェック",     startDate:"2025-10-30", endDate:"2025-10-30", time:"10:00",content:"ライブハウスにて",                              category:"meeting"},
  {id:"s6",  title:"秋ライブ 本番",          startDate:"2025-11-01", endDate:"2025-11-01", time:"18:00",content:"会場：ライブハウス○○\nセトリ最終確定済み",      category:"live"},
  {id:"s7",  title:"引き継ぎMTG",           startDate:"2025-11-08", endDate:"2025-11-08", time:"16:00",content:"次期担当者へのブリーフィング",                   category:"meeting"},
  {id:"s8",  title:"年末ふりかえりMTG",     startDate:"2025-12-20", endDate:"2025-12-20", time:"14:00",content:"年間活動レビュー",                              category:"meeting"},
  {id:"s9",  title:"新歓ビラ作成・印刷",    startDate:"2026-03-15", endDate:"2026-03-25", time:"",    content:"デザイン確認→印刷所入稿",                        category:"admin"},
  {id:"s10", title:"新入生勧誘期間",        startDate:"2026-04-01", endDate:"2026-04-14", time:"",    content:"ビラ配り・体験入部受付",                         category:"admin"},
  {id:"s11", title:"会場 打ち合わせ",       startDate:"2026-04-16", endDate:"2026-04-16", time:"14:00",content:"ライブハウスにて最終確認",                       category:"meeting"},
  {id:"s12", title:"音響 打ち合わせ",       startDate:"2026-04-18", endDate:"2026-04-18", time:"13:00",content:"PA担当と事前ブリーフィング",                    category:"rehearsal"},
  {id:"s13", title:"春ライブ 出欠1次申請",  startDate:"2026-04-20", endDate:"2026-04-27", time:"",    content:"Googleフォームにて各自回答",                     category:"admin"},
  {id:"s14", title:"春ライブ リハーサル",   startDate:"2026-06-13", endDate:"2026-06-28", time:"14:00",content:"週末スタジオ練習",                              category:"rehearsal"},
  {id:"s15", title:"PA・転換リハ",          startDate:"2026-07-02", endDate:"2026-07-02", time:"13:00",content:"会場入りしてフルリハ",                          category:"rehearsal"},
  {id:"s16", title:"春ライブ 本番",         startDate:"2026-07-04", endDate:"2026-07-04", time:"17:30",content:"会場：ライブハウス△△",                         category:"live"},
  {id:"s17", title:"夏合宿",               startDate:"2026-08-20", endDate:"2026-08-23", time:"",    content:"合宿所：那須高原\n秋ライブ向け集中練習",          category:"other"},
  {id:"s18", title:"秋ライブ リハーサル",   startDate:"2026-10-10", endDate:"2026-10-25", time:"14:00",content:"週末スタジオ",                                  category:"rehearsal"},
  {id:"s19", title:"秋ライブ 本番",         startDate:"2026-11-07", endDate:"2026-11-07", time:"18:00",content:"今年度最後のライブ",                            category:"live"},
  {id:"s20", title:"年度末 引き継ぎMTG",   startDate:"2026-11-15", endDate:"2026-11-15", time:"15:00",content:"次期スタッフへ業務引き継ぎ",                    category:"meeting"},
];

const INITIAL_NOTES = `【引き継ぎ全般の注意事項】

■ コミュニケーション
・連絡は必ず LINE グループ内で行い、個人連絡は避けてください
・返信期限は原則 24 時間以内
・緊急時は電話連絡も OK

■ 備品管理
・使用した備品は必ず元の場所に返却すること
・消耗品が残り少なくなったら即時報告
・機材の破損・紛失は速やかに現場監督へ報告

■ 個人情報の取り扱い
・出演者・スタッフの個人情報は外部に漏らさないこと
・写真・動画の撮影・投稿は事前承認が必要

■ 緊急連絡先
・現場監督:         090-XXXX-XXXX
・ライブハウス担当:  03-XXXX-XXXX
・警察 / 救急:      110 / 119`;

/* ─────────────────────────────────────────────
   MULTI-DAY EVENT LAYOUT
   Returns { items: [{ev, col0, col1, row, startsHere, endsHere}], rowCount }
───────────────────────────────────────────── */
function layoutWeek(cells, events) {
  const valid   = cells.filter(Boolean);
  if (!valid.length) return { items: [], rowCount: 0 };
  const wStart  = valid[0].key;
  const wEnd    = valid[valid.length - 1].key;

  // events that overlap this week
  const overlap = events
    .filter(e => e.startDate <= wEnd && e.endDate >= wStart)
    .sort((a, b) => {
      if (a.startDate !== b.startDate) return a.startDate < b.startDate ? -1 : 1;
      const da = new Date(a.endDate) - new Date(a.startDate);
      const db = new Date(b.endDate) - new Date(b.startDate);
      return db - da; // longer first
    });

  const grid  = []; // grid[row][col] = true if occupied
  const items = [];

  for (const ev of overlap) {
    // find leftmost column in this week for this event
    let c0 = cells.findIndex(c => c && c.key >= ev.startDate);
    if (c0 < 0) c0 = cells.findIndex(Boolean);
    if (c0 < 0) continue;

    let c1 = -1;
    for (let i = 6; i >= 0; i--) {
      if (cells[i] && cells[i].key <= ev.endDate) { c1 = i; break; }
    }
    if (c1 < c0) continue;

    // find free row
    let row = 0;
    outer: while (true) {
      if (!grid[row]) grid[row] = Array(7).fill(false);
      for (let c = c0; c <= c1; c++) {
        if (grid[row][c]) { row++; continue outer; }
      }
      break;
    }
    for (let c = c0; c <= c1; c++) grid[row][c] = true;

    items.push({
      ev,
      c0, c1,
      span: c1 - c0 + 1,
      row,
      startsHere: ev.startDate >= wStart,
      endsHere:   ev.endDate   <= wEnd,
    });
  }
  return { items, rowCount: grid.length };
}

/* ─────────────────────────────────────────────
   SHARED ATOMS
───────────────────────────────────────────── */
const css = (obj) => Object.entries(obj).map(([k,v]) => `${k.replace(/([A-Z])/g,'-$1').toLowerCase()}:${v}`).join(';');

function Pill({ label }) {
  return (
    <span style={{
      fontSize: 9, fontFamily: T.fm, letterSpacing: "0.08em",
      background: T.hover, color: T.muted,
      padding: "2px 8px", borderRadius: 99,
    }}>{label}</span>
  );
}

function SectionLabel({ children }) {
  return (
    <p style={{
      fontFamily: T.fm, fontSize: 9, letterSpacing: "0.14em",
      textTransform: "uppercase", color: T.muted, marginBottom: 12,
    }}>{children}</p>
  );
}

function ImgPlaceholder({ label = "参考画像" }) {
  return (
    <div style={{
      aspectRatio: "16/9", borderRadius: 10, background: T.paper,
      border: `1.5px dashed ${T.line}`,
      display: "flex", flexDirection: "column", alignItems: "center",
      justifyContent: "center", gap: 6, margin: "14px 0",
    }}>
      <FileText size={17} style={{ color: T.line }} />
      <span style={{ fontSize: 10, color: T.muted, fontFamily: T.fm }}>{label}</span>
    </div>
  );
}

/* ─────────────────────────────────────────────
   ACCORDION
───────────────────────────────────────────── */
function Accordion({ title, icon, badge, depth = 0, children }) {
  const [open, setOpen] = useState(false);
  const pl = `${1.25 + depth * 1.25}rem`;
  return (
    <div style={{
      border: `1px solid ${T.line}`, borderRadius: 12,
      background: depth === 0 ? T.surface : T.paper,
      marginBottom: depth === 0 ? 8 : 0, marginTop: depth > 0 ? 6 : 0, overflow: "hidden",
    }}>
      <button
        onClick={() => setOpen(o => !o)}
        onMouseEnter={e => e.currentTarget.style.background = T.hover}
        onMouseLeave={e => e.currentTarget.style.background = "transparent"}
        style={{
          width: "100%", display: "flex", alignItems: "center",
          justifyContent: "space-between", paddingLeft: pl,
          paddingRight: "1.25rem", paddingTop: "0.9rem", paddingBottom: "0.9rem",
          background: "transparent", border: "none", cursor: "pointer", textAlign: "left",
          transition: "background .12s",
        }}
      >
        <div style={{ display: "flex", alignItems: "center", gap: 10, minWidth: 0 }}>
          {icon && <span style={{ color: T.muted, flexShrink: 0 }}>{icon}</span>}
          <span style={{ fontSize: 13, fontWeight: 500, color: T.ink, fontFamily: T.fb }}>{title}</span>
          {badge && <Pill label={badge} />}
        </div>
        {open
          ? <ChevronRight size={12} style={{ color: T.muted, transform: "rotate(90deg)", transition: ".15s", flexShrink: 0 }} />
          : <ChevronRight size={12} style={{ color: T.line, transition: ".15s", flexShrink: 0 }} />}
      </button>
      {open && (
        <div style={{
          borderTop: `1px solid ${T.line}`,
          padding: `1rem ${pl} 1rem 1.25rem`,
          paddingLeft: pl,
        }}>
          {children}
        </div>
      )}
    </div>
  );
}

/* ─────────────────────────────────────────────
   MANUALS PAGE
───────────────────────────────────────────── */
const TP  = { fontSize: 13, color: T.mid, lineHeight: 1.8, marginBottom: 10, fontFamily: T.fb };
const TPH = { ...TP, fontWeight: 500, color: T.ink, marginTop: 10 };
const UL  = { fontSize: 12, color: T.mid, lineHeight: 2.1, paddingLeft: 0, listStyle: "none" };

function ManualsPage() {
  return (
    <div style={{ maxWidth: 640, margin: "0 auto" }} className="fade-up">
      <Accordion title="セトリ班" icon={<FileText size={14} />} badge="外部リンク">
        <p style={TP}>セットリストの作成・管理を担当する班のマニュアルです。最新版はGoogleスプレッドシートで管理されています。更新後は連絡班に必ず通知してください。</p>
        <a href="https://docs.google.com/spreadsheets" style={{
          display: "inline-flex", alignItems: "center", gap: 7,
          background: T.ink, color: T.paper, fontSize: 12, fontWeight: 400,
          padding: "9px 18px", borderRadius: 8, textDecoration: "none",
          fontFamily: T.fb, letterSpacing: "0.02em",
        }}>
          <ExternalLink size={11} />セトリ管理シートを開く
        </a>
      </Accordion>

      <Accordion title="連絡班" icon={<Bell size={14} />}>
        <Accordion title="全体連絡用" depth={1} badge="テキスト">
          <p style={TP}>全体への連絡はLINEグループ「〇〇スタッフ全体」で行います。重要事項は必ずピン留めし、返信は24時間以内を目安にしてください。</p>
          {[["仮出欠ノート","#"],["1次申請フォーム","#"]].map(([label, href]) => (
            <a key={label} href={href} style={{
              display: "flex", alignItems: "center", gap: 8, fontSize: 13, color: T.mid,
              padding: "10px 12px", border: `1px solid ${T.line}`, borderRadius: 8,
              marginBottom: 6, textDecoration: "none", background: T.paper,
              fontFamily: T.fb, transition: "border-color .12s",
            }}>
              <Link2 size={11} style={{ color: T.line }} />{label}
            </a>
          ))}
        </Accordion>
        <Accordion title="ライブハウス連絡用" depth={1} badge="テキスト">
          <p style={TP}>ライブハウスへの連絡は担当者（連絡班長）が一本化して行います。</p>
          <ul style={UL}>
            {["問い合わせは必ずメールで行い、電話は緊急時のみ","件名に「[〇〇バンド]」を必ず記載する","連絡先: livehouse@example.com","緊急連絡先: 03-XXXX-XXXX"].map((t, i) => (
              <li key={i} style={{ display: "flex", gap: 8 }}><span style={{ color: T.line }}>—</span>{t}</li>
            ))}
          </ul>
        </Accordion>
      </Accordion>

      <Accordion title="設営・撤収" icon={<Wrench size={14} />} badge="テキスト + 画像">
        <p style={TPH}>設営手順</p>
        <ol style={{ ...UL, paddingLeft: 18, listStyle: "decimal" }}>
          {["搬入口から機材を運び込む（エレベーター使用可）","PA機材は先にステージ上に配置","照明機材の設置（高所作業は必ず2名以上）","マイクスタンド・ケーブルの配線","音響・照明チェック開始"].map((t, i) => <li key={i}>{t}</li>)}
        </ol>
        <ImgPlaceholder label="設営フロー図" />
        <p style={TPH}>撤収手順</p>
        <ol style={{ ...UL, paddingLeft: 18, listStyle: "decimal" }}>
          {["ケーブル類を丁寧に束ねて保管","機材チェックリストで全点確認","忘れ物チェック後、搬出"].map((t, i) => <li key={i}>{t}</li>)}
        </ol>
        <ImgPlaceholder label="機材配置図" />
      </Accordion>

      <Accordion title="現場監督" icon={<Eye size={14} />} badge="テキスト">
        <p style={TP}>現場監督は当日の全体進行を管理する責任者です。</p>
        <p style={TPH}>主な役割</p>
        <ul style={UL}>
          {["タイムスケジュールの管理と各班への指示","トラブル発生時の即時対応・判断","スタッフ間の連絡調整","ライブハウス担当者との折衝"].map((t, i) => (
            <li key={i} style={{ display: "flex", gap: 8 }}><span style={{ color: T.line }}>·</span>{t}</li>
          ))}
        </ul>
      </Accordion>

      <Accordion title="PA・転換について" icon={<Music size={14} />}>
        <Accordion title="PAについて" depth={1} badge="テキスト + 画像">
          <p style={TP}>PAはPublic Address（音響）の略です。</p>
          <p style={TPH}>音響チェック手順</p>
          <ol style={{ ...UL, paddingLeft: 18, listStyle: "decimal" }}>
            {["機材の電源投入順序を守る（アンプは最後）","マイクゲインの調整（ファンタム電源確認）","モニター返しの確認（各演奏者と個別確認）","本番レベルでのサウンドチェック"].map((t, i) => <li key={i}>{t}</li>)}
          </ol>
          <ImgPlaceholder label="PA機材接続図" />
          <ImgPlaceholder label="ミキサー操作パネル図" />
        </Accordion>
        <Accordion title="転換について" depth={1} badge="テキスト + 画像">
          <p style={TP}>転換とはバンド交代時の機材入れ替え作業です。目標：15分以内。</p>
          <ol style={{ ...UL, paddingLeft: 18, listStyle: "decimal" }}>
            {["前バンドのステージアウト後、速やかに撤収開始","ドラムセットは共有部分を残し最小限の変更","アンプのチャンネル切り替え・音量調整","次バンドのメンバーへマイク位置の確認"].map((t, i) => <li key={i}>{t}</li>)}
          </ol>
          <ImgPlaceholder label="転換フロー図" />
          <ImgPlaceholder label="ステージレイアウト図" />
        </Accordion>
      </Accordion>
    </div>
  );
}

/* ─────────────────────────────────────────────
   CALENDAR PAGE
───────────────────────────────────────────── */
const EV_H  = 22; // event bar height px
const EV_G  = 3;  // gap between bars px
const DAY_H = 36; // day number row height px

function CalendarPage({ events, onAdd, onDelete }) {
  // default to current fiscal month (April 2026 = index 7)
  const initIdx = FISCAL.findIndex(f => f.year === 2026 && f.month === 3);
  const [mIdx,  setMIdx]  = useState(initIdx >= 0 ? initIdx : 0);
  const [modal, setModal] = useState(false);
  const [form,  setForm]  = useState({ title:"", startDate:"", endDate:"", time:"", content:"", category:"other" });

  const { year, month } = FISCAL[mIdx];

  /* Build calendar grid */
  const { weeks, layouts } = useMemo(() => {
    const fd    = wd1st(year, month);
    const total = daysIn(year, month);
    const cells = [
      ...Array(fd).fill(null),
      ...Array.from({ length: total }, (_, i) => ({
        day: i + 1,
        key: toKey(year, month, i + 1),
      })),
    ];
    while (cells.length % 7) cells.push(null);

    const wks = [];
    for (let i = 0; i < cells.length; i += 7) wks.push(cells.slice(i, i + 7));
    return {
      weeks: wks,
      layouts: wks.map(w => layoutWeek(w, events)),
    };
  }, [year, month, events]);

  /* Events in this month */
  const mStart    = toKey(year, month, 1);
  const mEnd      = toKey(year, month, daysIn(year, month));
  const monthEvs  = events
    .filter(e => e.startDate <= mEnd && e.endDate >= mStart)
    .sort((a, b) => a.startDate < b.startDate ? -1 : 1);

  function openAdd(dateKey) {
    const d = dateKey || TODAY;
    setForm({ title: "", startDate: d, endDate: d, time: "", content: "", category: "other" });
    setModal(true);
  }
  function handleSubmit() {
    if (!form.title.trim() || !form.startDate) return;
    const endDate = (form.endDate && form.endDate >= form.startDate) ? form.endDate : form.startDate;
    onAdd({ id: uid(), ...form, endDate });
    setModal(false);
  }

  /* Month selector pills */
  const pillRows = useMemo(() => {
    const rows = [];
    let row = [], curYear = null;
    FISCAL.forEach((f, i) => {
      if (f.year !== curYear) {
        if (row.length) rows.push(row);
        row = [];
        curYear = f.year;
      }
      const ms = toKey(f.year, f.month, 1);
      const me = toKey(f.year, f.month, daysIn(f.year, f.month));
      const hasEvt = events.some(e => e.startDate <= me && e.endDate >= ms);
      row.push({ i, f, hasEvt });
    });
    if (row.length) rows.push(row);
    return rows;
  }, [events]);

  return (
    <div style={{ maxWidth: 820, margin: "0 auto" }} className="fade-up">

      {/* ── Archive header ── */}
      <div style={{
        display: "flex", alignItems: "flex-start", justifyContent: "space-between",
        flexWrap: "wrap", gap: 12, marginBottom: "1.5rem",
        paddingBottom: "1.5rem", borderBottom: `1px solid ${T.line}`,
      }}>
        <div>
          <p style={{
            fontFamily: T.fm, fontSize: 9, letterSpacing: "0.14em",
            textTransform: "uppercase", color: T.muted, marginBottom: 8,
          }}>
            2026年度 業務カレンダー · Archive  2025.09 — 2026.11
          </p>
          {/* fiscal month selector */}
          {pillRows.map((row, ri) => {
            const fy = FISCAL[row[0].i].year;
            return (
              <div key={ri} style={{ display: "flex", alignItems: "center", gap: 4, marginBottom: 4, flexWrap: "wrap" }}>
                <span style={{ fontFamily: T.fm, fontSize: 9, color: T.line, width: 30, flexShrink: 0 }}>{fy}</span>
                {row.map(({ i, f, hasEvt }) => {
                  const active = i === mIdx;
                  return (
                    <button
                      key={i}
                      onClick={() => setMIdx(i)}
                      style={{
                        padding: "4px 12px", borderRadius: 6,
                        fontSize: 11, fontFamily: T.fm,
                        border: active ? `1.5px solid ${T.ink}` : `1px solid ${T.line}`,
                        background: active ? T.ink : "transparent",
                        color: active ? T.paper : hasEvt ? T.mid : T.line,
                        cursor: "pointer", transition: "all .12s",
                        position: "relative",
                      }}
                    >
                      {M_JA[f.month]}
                      {hasEvt && !active && (
                        <span style={{
                          position: "absolute", top: 4, right: 4,
                          width: 3, height: 3, borderRadius: "50%", background: T.muted,
                        }} />
                      )}
                    </button>
                  );
                })}
              </div>
            );
          })}
        </div>
        <button onClick={() => openAdd(null)} style={{
          display: "flex", alignItems: "center", gap: 7,
          padding: "10px 18px", borderRadius: 9, border: "none",
          background: T.ink, color: T.paper,
          fontSize: 12, fontWeight: 400, cursor: "pointer",
          fontFamily: T.fb, letterSpacing: "0.02em", transition: "opacity .15s",
          alignSelf: "flex-start",
        }}>
          <Plus size={12} />予定を追加
        </button>
      </div>

      {/* ── Month title ── */}
      <div style={{
        display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: "1.25rem",
      }}>
        <h2 style={{
          fontFamily: T.fd, fontSize: 48, fontWeight: 300,
          color: T.ink, lineHeight: 1, letterSpacing: "-0.01em",
        }}>
          {M_EN[month]}{" "}
          <span style={{ fontSize: 20, color: T.muted, fontWeight: 300 }}>{year}</span>
        </h2>
        <div style={{ display: "flex", gap: 6 }}>
          {[
            [mIdx === 0, () => setMIdx(i => Math.max(0, i-1)), <ChevronLeft size={14} />],
            [mIdx === FISCAL.length-1, () => setMIdx(i => Math.min(FISCAL.length-1, i+1)), <ChevronRight size={14} />],
          ].map(([disabled, fn, icon], ki) => (
            <button key={ki} onClick={fn} disabled={disabled} style={{
              width: 34, height: 34, borderRadius: 8, border: `1px solid ${T.line}`,
              background: "transparent", cursor: disabled ? "not-allowed" : "pointer",
              opacity: disabled ? 0.25 : 1, display: "flex", alignItems: "center",
              justifyContent: "center", color: T.mid, transition: "border-color .12s",
            }}>{icon}</button>
          ))}
        </div>
      </div>

      {/* ── Calendar grid ── */}
      <div style={{
        border: `1px solid ${T.line}`, borderRadius: 14, overflow: "hidden",
        background: T.surface,
      }}>
        {/* DOW header */}
        <div style={{ display: "grid", gridTemplateColumns: "repeat(7,1fr)", background: T.paper }}>
          {DOW.map((d, i) => (
            <div key={d} style={{
              textAlign: "center", padding: "8px 0",
              fontFamily: T.fm, fontSize: 9, letterSpacing: "0.06em",
              color: i === 0 ? "#C08080" : i === 6 ? "#8090C0" : T.muted,
              borderRight: i < 6 ? `1px solid ${T.line}` : "none",
            }}>{d}</div>
          ))}
        </div>

        {/* Week rows */}
        {weeks.map((week, wi) => {
          const { items, rowCount } = layouts[wi];
          const evZoneH = rowCount > 0 ? rowCount * (EV_H + EV_G) + EV_G : 6;
          return (
            <div key={wi} style={{ borderTop: `1px solid ${T.line}` }}>
              {/* Day number row */}
              <div style={{ display: "grid", gridTemplateColumns: "repeat(7,1fr)" }}>
                {week.map((cell, ci) => {
                  const isToday   = cell?.key === TODAY;
                  const isWeekend = ci === 0 || ci === 6;
                  return (
                    <div
                      key={ci}
                      onClick={() => cell && openAdd(cell.key)}
                      onMouseEnter={e => { if (cell) e.currentTarget.style.background = T.hover; }}
                      onMouseLeave={e => { if (cell) e.currentTarget.style.background = "transparent"; }}
                      style={{
                        height: DAY_H, display: "flex", alignItems: "center", justifyContent: "center",
                        borderRight: ci < 6 ? `1px solid ${T.line}` : "none",
                        background: cell ? "transparent" : T.paper,
                        cursor: cell ? "pointer" : "default", transition: "background .1s",
                      }}
                    >
                      {cell && (
                        <span style={{
                          width: 24, height: 24, borderRadius: "50%",
                          display: "flex", alignItems: "center", justifyContent: "center",
                          fontSize: 11, fontFamily: T.fm,
                          background: isToday ? T.ink : "transparent",
                          color: isToday ? T.paper : isWeekend ? T.line : T.mid,
                        }}>{cell.day}</span>
                      )}
                    </div>
                  );
                })}
              </div>

              {/* Event bars zone */}
              <div style={{
                position: "relative", height: evZoneH,
                borderTop: rowCount > 0 ? `1px solid ${T.line}` : "none",
              }}>
                {/* Column dividers */}
                {[1,2,3,4,5,6].map(ci => (
                  <div key={ci} style={{
                    position: "absolute", top: 0, bottom: 0,
                    left: `${ci/7*100}%`, width: 1, background: T.line,
                  }} />
                ))}

                {items.map(({ ev, c0, c1, span, row, startsHere, endsHere }) => {
                  const cat    = getCat(ev.category);
                  const top    = EV_G + row * (EV_H + EV_G);
                  const lPct   = c0 / 7 * 100;
                  const wPct   = span / 7 * 100;
                  const rL     = startsHere ? 5 : 0;
                  const rR     = endsHere   ? 5 : 0;
                  const lPad   = startsHere ? 8 : 4;
                  const lOff   = startsHere ? 3 : 0;
                  const rOff   = endsHere   ? 3 : 0;
                  return (
                    <div
                      key={ev.id + "-" + wi}
                      title={`${ev.title}  ${ev.startDate}${ev.endDate !== ev.startDate ? " – " + ev.endDate : ""}`}
                      style={{
                        position: "absolute",
                        left: `calc(${lPct}% + ${lOff}px)`,
                        width: `calc(${wPct}% - ${lOff + rOff}px)`,
                        top, height: EV_H,
                        background: cat.bg, color: cat.fg,
                        borderRadius: `${rL}px ${rR}px ${rR}px ${rL}px`,
                        display: "flex", alignItems: "center",
                        paddingLeft: lPad, overflow: "hidden",
                        fontSize: 10, fontFamily: T.fb, fontWeight: 400,
                        letterSpacing: "0.01em", cursor: "default",
                        whiteSpace: "nowrap",
                      }}
                    >
                      {startsHere && (
                        <>
                          {ev.time && (
                            <span style={{ opacity: 0.5, marginRight: 4, fontFamily: T.fm, fontSize: 9 }}>{ev.time}</span>
                          )}
                          {ev.title}
                        </>
                      )}
                    </div>
                  );
                })}
              </div>
            </div>
          );
        })}
      </div>

      {/* ── Legend ── */}
      <div style={{ display: "flex", gap: 16, flexWrap: "wrap", marginTop: 12, marginBottom: 28 }}>
        {CATS.map(c => (
          <div key={c.id} style={{ display: "flex", alignItems: "center", gap: 6 }}>
            <span style={{ width: 10, height: 10, borderRadius: 3, background: c.bg, flexShrink: 0 }} />
            <span style={{ fontSize: 11, color: T.muted, fontFamily: T.fm }}>{c.label}</span>
          </div>
        ))}
      </div>

      {/* ── Event list for current month ── */}
      <SectionLabel>{M_JA[month]}の業務一覧  ·  {monthEvs.length}件</SectionLabel>
      <div style={{ display: "flex", flexDirection: "column", gap: 7 }}>
        {monthEvs.length === 0 && (
          <p style={{ fontSize: 13, color: T.muted, textAlign: "center", padding: "2rem 0", fontFamily: T.fm }}>
            この月の予定はありません
          </p>
        )}
        {monthEvs.map(ev => {
          const cat      = getCat(ev.category);
          const isSingle = ev.startDate === ev.endDate;
          const dur      = isSingle ? 0
            : Math.round((new Date(ev.endDate) - new Date(ev.startDate)) / 864e5);
          return (
            <div key={ev.id} style={{
              display: "flex", alignItems: "flex-start", gap: 12,
              padding: "14px 16px", background: T.surface,
              border: `1px solid ${T.line}`, borderRadius: 10,
            }}>
              {/* Category accent */}
              <div style={{
                width: 3, borderRadius: 2, background: cat.bg,
                alignSelf: "stretch", flexShrink: 0,
              }} />
              <div style={{ flex: 1, minWidth: 0 }}>
                <div style={{ display: "flex", alignItems: "center", gap: 8, flexWrap: "wrap", marginBottom: 3 }}>
                  <span style={{ fontSize: 13, fontWeight: 500, color: T.ink, fontFamily: T.fb }}>{ev.title}</span>
                  <span style={{
                    fontSize: 9, background: cat.bg, color: cat.fg,
                    padding: "2px 8px", borderRadius: 99, fontFamily: T.fm, letterSpacing: "0.04em",
                  }}>{cat.label}</span>
                  {!isSingle && (
                    <span style={{ fontSize: 9, color: T.muted, fontFamily: T.fm }}>{dur}日間</span>
                  )}
                </div>
                <p style={{ fontSize: 11, color: T.muted, fontFamily: T.fm, marginBottom: ev.content ? 4 : 0 }}>
                  {isSingle ? ev.startDate : `${ev.startDate}  →  ${ev.endDate}`}
                  {ev.time && `  ·  ${ev.time}`}
                </p>
                {ev.content && (
                  <p style={{ fontSize: 12, color: T.mid, lineHeight: 1.7, whiteSpace: "pre-line", fontFamily: T.fb }}>
                    {ev.content}
                  </p>
                )}
              </div>
              <button
                onClick={() => onDelete(ev.id)}
                onMouseEnter={e => e.currentTarget.style.color = T.mid}
                onMouseLeave={e => e.currentTarget.style.color = T.line}
                style={{ padding: 6, border: "none", background: "transparent", cursor: "pointer", color: T.line, flexShrink: 0, transition: "color .12s" }}
              >
                <Trash2 size={12} />
              </button>
            </div>
          );
        })}
      </div>

      {/* ── Add Event Modal ── */}
      {modal && (
        <div
          onClick={e => { if (e.target === e.currentTarget) setModal(false); }}
          style={{
            position: "fixed", inset: 0, zIndex: 50,
            background: "rgba(20,19,15,0.6)",
            display: "flex", alignItems: "center", justifyContent: "center", padding: 16,
          }}
        >
          <div style={{
            background: T.paper, borderRadius: 18, width: "100%", maxWidth: 450,
            padding: "1.75rem", boxSizing: "border-box",
          }}>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 20 }}>
              <div>
                <p style={{ fontFamily: T.fd, fontSize: 22, fontWeight: 400, color: T.ink, lineHeight: 1 }}>
                  予定を追加
                </p>
                <p style={{ fontSize: 10, color: T.muted, fontFamily: T.fm, marginTop: 3 }}>
                  2026年度 アーカイブカレンダーに記録します
                </p>
              </div>
              <button onClick={() => setModal(false)} style={{ border: "none", background: "transparent", cursor: "pointer", padding: 4 }}>
                <X size={14} style={{ color: T.muted }} />
              </button>
            </div>

            {/* Category picker */}
            <div style={{ marginBottom: 16 }}>
              <label style={{ fontSize: 9, fontFamily: T.fm, letterSpacing: "0.12em", textTransform: "uppercase", color: T.muted, display: "block", marginBottom: 8 }}>カテゴリ</label>
              <div style={{ display: "flex", gap: 5, flexWrap: "wrap" }}>
                {CATS.map(c => {
                  const active = form.category === c.id;
                  return (
                    <button key={c.id} onClick={() => setForm(f => ({ ...f, category: c.id }))} style={{
                      padding: "5px 12px", borderRadius: 6, fontSize: 11, fontFamily: T.fm,
                      border: active ? `1.5px solid ${c.bg}` : `1px solid ${T.line}`,
                      background: active ? c.bg : "transparent",
                      color: active ? c.fg : T.muted, cursor: "pointer", transition: "all .12s",
                    }}>{c.label}</button>
                  );
                })}
              </div>
            </div>

            {/* Title */}
            <ModalField label="タイトル *">
              <input type="text" value={form.title}
                onChange={e => setForm(f => ({ ...f, title: e.target.value }))}
                placeholder="例）本番当日、リハーサル期間…"
                style={inputStyle}
                onFocus={e => e.target.style.borderColor = T.mid}
                onBlur={e => e.target.style.borderColor = T.line}
              />
            </ModalField>

            {/* Date range */}
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10, marginBottom: 12 }}>
              <ModalField label="開始日">
                <input type="date" value={form.startDate}
                  onChange={e => setForm(f => {
                    const v = { ...f, startDate: e.target.value };
                    if (v.endDate && v.endDate < e.target.value) v.endDate = e.target.value;
                    return v;
                  })}
                  style={inputStyle}
                />
              </ModalField>
              <ModalField label="終了日 (期間)">
                <input type="date" value={form.endDate} min={form.startDate}
                  onChange={e => setForm(f => ({ ...f, endDate: e.target.value }))}
                  style={inputStyle}
                />
              </ModalField>
            </div>

            {/* Time + note */}
            <div style={{ display: "grid", gridTemplateColumns: "1fr 2fr", gap: 10, marginBottom: 16 }}>
              <ModalField label="時間">
                <input type="time" value={form.time}
                  onChange={e => setForm(f => ({ ...f, time: e.target.value }))}
                  style={inputStyle}
                />
              </ModalField>
              <ModalField label="メモ">
                <textarea value={form.content} rows={2}
                  onChange={e => setForm(f => ({ ...f, content: e.target.value }))}
                  placeholder="場所、持ち物など"
                  style={{ ...inputStyle, resize: "none", lineHeight: 1.65 }}
                />
              </ModalField>
            </div>

            <div style={{ display: "flex", gap: 10 }}>
              <button onClick={() => setModal(false)} style={{
                flex: 1, padding: 11, borderRadius: 10, border: `1px solid ${T.line}`,
                background: "transparent", fontSize: 13, color: T.mid,
                cursor: "pointer", fontFamily: T.fb,
              }}>キャンセル</button>
              <button onClick={handleSubmit} disabled={!form.title.trim() || !form.startDate} style={{
                flex: 2, padding: 11, borderRadius: 10, border: "none",
                background: !form.title.trim() || !form.startDate ? T.line : T.ink,
                color: T.paper, fontSize: 13, fontWeight: 500,
                cursor: !form.title.trim() || !form.startDate ? "not-allowed" : "pointer",
                fontFamily: T.fb, transition: "background .15s",
              }}>カレンダーに追加</button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

/* modal helpers */
const inputStyle = {
  width: "100%", padding: "9px 11px", border: `1px solid ${T.line}`,
  borderRadius: 8, fontSize: 12, background: T.surface, outline: "none",
  boxSizing: "border-box", fontFamily: T.fb, color: T.ink, transition: "border-color .12s",
};
function ModalField({ label, children }) {
  return (
    <div style={{ marginBottom: 0 }}>
      <label style={{ fontSize: 9, fontFamily: T.fm, letterSpacing: "0.12em", textTransform: "uppercase", color: T.muted, display: "block", marginBottom: 6 }}>{label}</label>
      {children}
    </div>
  );
}

/* ─────────────────────────────────────────────
   NOTES PAGE
───────────────────────────────────────────── */
function NotesPage() {
  const [notes,   setNotes]   = useState(INITIAL_NOTES);
  const [editing, setEditing] = useState(false);
  return (
    <div style={{ maxWidth: 640, margin: "0 auto" }} className="fade-up">
      <div style={{ display: "flex", justifyContent: "flex-end", marginBottom: 14 }}>
        <button onClick={() => setEditing(e => !e)} style={{
          fontSize: 11, border: `1px solid ${T.line}`, color: T.mid,
          padding: "6px 14px", borderRadius: 8, background: "transparent",
          cursor: "pointer", fontFamily: T.fm, transition: "border-color .12s",
        }}>
          {editing ? "保存する" : "編集する"}
        </button>
      </div>
      {editing ? (
        <textarea value={notes} onChange={e => setNotes(e.target.value)} rows={26}
          style={{
            width: "100%", border: `1px solid ${T.line}`, borderRadius: 12,
            padding: "1.5rem", fontSize: 13, color: T.ink, lineHeight: 1.9,
            background: T.surface, outline: "none", resize: "none",
            boxSizing: "border-box", fontFamily: T.fm,
          }}
        />
      ) : (
        <div style={{
          background: T.surface, border: `1px solid ${T.line}`, borderRadius: 12,
          padding: "1.75rem 2rem",
        }}>
          <pre style={{
            fontSize: 13, color: T.mid, whiteSpace: "pre-wrap", lineHeight: 1.95,
            fontFamily: T.fm, margin: 0,
          }}>{notes}</pre>
        </div>
      )}
    </div>
  );
}

/* ─────────────────────────────────────────────
   HOME PAGE
───────────────────────────────────────────── */
const REMIND_LABELS = { 1: "明日", 3: "3日前", 7: "1週間前" };

function HomePage({ setView, events }) {
  const reminders = events
    .map(e => ({ ...e, days: away(e.startDate) }))
    .filter(e => REMIND_LABELS[e.days])
    .sort((a, b) => a.days - b.days)
    .map(e => ({ ...e, label: REMIND_LABELS[e.days] }));

  const panels = [
    { id: "manuals",  icon: <BookOpen size={22} />,   title: "マニュアル一覧",    en: "Manuals",  desc: "各班の業務マニュアルを閲覧",             meta: "5カテゴリ" },
    { id: "calendar", icon: <Calendar size={22} />,   title: "業務日程カレンダー", en: "Calendar", desc: "2026年度 全業務日程アーカイブ · 15か月",  meta: `${events.length}件の予定` },
    { id: "notes",    icon: <StickyNote size={22} />, title: "その他注意事項",    en: "Notes",    desc: "連絡ルール・緊急連絡先など",             meta: "随時更新" },
  ];

  return (
    <div style={{ maxWidth: 580, margin: "0 auto" }} className="fade-up">
      {/* Hero */}
      <div style={{ marginBottom: "2.5rem" }}>
        <p style={{ fontFamily: T.fm, fontSize: 9, letterSpacing: "0.14em", textTransform: "uppercase", color: T.muted, marginBottom: 12 }}>
          2026年度 業務引き継ぎ管理システム
        </p>
        <h1 style={{ fontFamily: T.fd, fontSize: 44, fontWeight: 300, color: T.ink, lineHeight: 1.05, marginBottom: 8 }}>
          おはようございます
        </h1>
        <p style={{ fontFamily: T.fm, fontSize: 11, color: T.muted }}>2026.04.15  Wed</p>
      </div>

      {/* Reminders */}
      {reminders.length > 0 && (
        <section style={{ marginBottom: "2rem" }}>
          <SectionLabel>リマインド  ·  {reminders.length}件</SectionLabel>
          <div style={{ display: "grid", gap: 8, gridTemplateColumns: "repeat(auto-fill,minmax(190px,1fr))" }}>
            {reminders.map(r => {
              const urgent = r.days === 1;
              const cat    = getCat(r.category);
              return (
                <div key={r.id} style={{
                  padding: "14px 16px", borderRadius: 12,
                  background: urgent ? T.ink : T.surface,
                  border: `1px solid ${urgent ? T.ink : T.line}`,
                }}>
                  <span style={{
                    display: "inline-block", marginBottom: 7,
                    fontSize: 9, fontFamily: T.fm, letterSpacing: "0.06em",
                    background: urgent ? "#2E2E2A" : T.hover,
                    color: urgent ? T.muted : T.muted,
                    padding: "2px 8px", borderRadius: 99,
                  }}>{r.label}</span>
                  <p style={{ fontSize: 13, fontWeight: 500, color: urgent ? T.paper : T.ink, marginBottom: 3, fontFamily: T.fb }}>{r.title}</p>
                  <p style={{ fontSize: 10, color: urgent ? "#666660" : T.muted, fontFamily: T.fm }}>
                    {r.startDate !== r.endDate ? `${r.startDate} —` : r.startDate}
                    {r.time && `  ·  ${r.time}`}
                  </p>
                </div>
              );
            })}
          </div>
        </section>
      )}

      {/* Navigation */}
      <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
        {panels.map((p, pi) => (
          <button key={p.id} onClick={() => setView(p.id)}
            onMouseEnter={e => {
              e.currentTarget.style.borderColor = T.muted;
              e.currentTarget.style.background  = T.hover;
            }}
            onMouseLeave={e => {
              e.currentTarget.style.borderColor = T.line;
              e.currentTarget.style.background  = T.surface;
            }}
            style={{
              textAlign: "left", padding: "18px 20px",
              background: T.surface, border: `1px solid ${T.line}`,
              borderRadius: 14, cursor: "pointer",
              display: "flex", alignItems: "center", gap: 16,
              transition: "all .15s",
              animationDelay: `${pi * 60}ms`,
            }}
            className="fade-up"
          >
            <div style={{
              width: 46, height: 46, borderRadius: 12, background: T.paper,
              display: "flex", alignItems: "center", justifyContent: "center",
              flexShrink: 0, color: T.mid,
            }}>{p.icon}</div>
            <div style={{ flex: 1, minWidth: 0 }}>
              <div style={{ display: "flex", alignItems: "baseline", gap: 8, marginBottom: 4 }}>
                <span style={{ fontSize: 14, fontWeight: 500, color: T.ink, fontFamily: T.fb }}>{p.title}</span>
                <span style={{ fontSize: 9, color: T.line, fontFamily: T.fm }}>{p.en}</span>
              </div>
              <p style={{ fontSize: 12, color: T.muted, fontFamily: T.fb, marginBottom: 3 }}>{p.desc}</p>
              <span style={{ fontSize: 10, color: T.line, fontFamily: T.fm }}>{p.meta}</span>
            </div>
            <ChevronRight size={13} style={{ color: T.line, flexShrink: 0 }} />
          </button>
        ))}
      </div>
    </div>
  );
}

/* ─────────────────────────────────────────────
   INTRO ANIMATION  14 → 15
   ・hold    : "14" を静止表示
   ・scramble: 2桁目が高速でインクリメント回転
   ・settle  : "15" で着地 + マルチベース readout が色変化
   ・fadeout : スケール+フェードで消える
───────────────────────────────────────────── */

// digit sequence: cycles 5→6→…→9→0→…→4→5, ending on 5 (21 steps)
const SEQ   = [5,6,7,8,9,0,1,2,3,4,5,6,7,8,9,0,1,2,3,4,5];
// wait[i] = how long to show SEQ[i] before advancing (ms); 20 gaps for 21 items
const WAIT  = [38,38,38,38,38,38,38,38, 68,68,68,68,68, 110,110,110, 175,175, 250,300];

function IntroAnimation({ onComplete }) {
  const [digit,   setDigit]   = useState(4);   // initially shows "14"
  const [phase,   setPhase]   = useState("hold"); // hold | scramble | settle | out
  const [prog,    setProg]    = useState(0);    // 0→1 for the progress line
  const [exiting, setExiting] = useState(false);
  const timerRef = useRef(null);

  /* Phase 1 – hold "14" for 1.1 s then scramble */
  useEffect(() => {
    timerRef.current = setTimeout(() => setPhase("scramble"), 1100);
    return () => clearTimeout(timerRef.current);
  }, []);

  /* Phase 2 – scramble */
  useEffect(() => {
    if (phase !== "scramble") return;
    let step = 0;
    let alive = true;

    function advance() {
      if (!alive) return;
      setDigit(SEQ[step]);
      setProg((step + 1) / SEQ.length);

      if (step < SEQ.length - 1) {
        timerRef.current = setTimeout(() => { step++; advance(); }, WAIT[step]);
      } else {
        // last element = 5, brief pause then settle
        timerRef.current = setTimeout(() => { if (alive) setPhase("settle"); }, 420);
      }
    }

    timerRef.current = setTimeout(advance, 80);
    return () => { alive = false; clearTimeout(timerRef.current); };
  }, [phase]);

  /* Phase 3 – settle then exit */
  useEffect(() => {
    if (phase !== "settle") return;
    timerRef.current = setTimeout(() => setExiting(true), 1300);
    return () => clearTimeout(timerRef.current);
  }, [phase]);

  /* Phase 4 – after fade, unmount */
  useEffect(() => {
    if (!exiting) return;
    timerRef.current = setTimeout(onComplete, 820);
    return () => clearTimeout(timerRef.current);
  }, [exiting]);

  const settled  = phase === "settle";
  const N        = parseInt(`1${digit}`);          // full number 10–19
  const binStr   = N.toString(2).padStart(8, "0"); // 8-bit binary
  const binFmt   = binStr.slice(0, 4) + " " + binStr.slice(4);
  const hexStr   = "0x" + N.toString(16).toUpperCase().padStart(2, "0");
  const octStr   = "0o" + N.toString(8).padStart(2, "0");

  const accentColor  = settled ? T.ink  : T.mid;
  const readoutColor = settled ? T.ink  : T.mid;

  return (
    <div style={{
      position: "fixed", inset: 0, zIndex: 9999,
      background: T.paper,
      display: "flex", flexDirection: "column",
      alignItems: "center", justifyContent: "center",
      opacity:    exiting ? 0 : 1,
      transform:  exiting ? "scale(1.025)" : "scale(1)",
      transition: exiting ? "opacity 0.82s ease, transform 0.82s ease" : "none",
      // subtle horizontal ruled lines — ledger paper feel
      backgroundImage: `repeating-linear-gradient(transparent,transparent 39px,${T.line} 39px,${T.line} 40px)`,
      userSelect: "none",
    }}>
      {/* ── Large numeral ── */}
      <div style={{ display: "flex", alignItems: "baseline", marginBottom: 44 }}>
        {/* "1" — always stable */}
        <span style={{
          fontFamily: T.fd, fontWeight: 300, lineHeight: 1,
          fontSize: "clamp(96px,16vw,210px)", color: T.ink,
          letterSpacing: "-0.015em",
        }}>1</span>

        {/* cycling digit */}
        <span style={{
          fontFamily: T.fd, fontWeight: 300, lineHeight: 1,
          fontSize: "clamp(96px,16vw,210px)",
          color: accentColor,
          transition: settled ? "color 0.55s ease" : "none",
          letterSpacing: "-0.015em",
          display: "inline-block", minWidth: "0.58em", textAlign: "center",
        }}>{digit}</span>
      </div>

      {/* ── Multi-base readout (appears after scramble starts) ── */}
      <div style={{
        marginBottom: 36, opacity: phase === "hold" ? 0 : 1,
        transition: "opacity 0.35s ease",
      }}>
        {[["DEC", String(N).padStart(2, "0")], ["BIN", binFmt], ["HEX", hexStr], ["OCT", octStr]].map(([label, val], i) => (
          <div key={label} style={{ display: "flex", alignItems: "baseline", gap: 20, marginBottom: 4 }}>
            <span style={{
              fontFamily: T.fm, fontSize: 9, letterSpacing: "0.14em",
              color: T.muted, width: 28, textAlign: "right",
            }}>{label}</span>
            {/* value rendered char by char so changed bits pop */}
            <span style={{
              fontFamily: T.fm, fontSize: 14,
              color: readoutColor,
              transition: settled ? "color 0.55s ease" : "none",
              letterSpacing: "0.14em",
            }}>{val}</span>
          </div>
        ))}
      </div>

      {/* ── Progress bar ── */}
      <div style={{ width: 200, height: 1, background: T.line, marginBottom: 22 }}>
        <div style={{
          height: 1,
          background: accentColor,
          width: `${prog * 100}%`,
          transition: settled ? "background 0.55s ease" : "width 0.06s linear",
        }} />
      </div>

      {/* ── Status label ── */}
      <p style={{
        fontFamily: T.fm, fontSize: 9, letterSpacing: "0.16em",
        textTransform: "uppercase", color: T.muted,
        transition: "opacity 0.3s",
      }}>
        {phase === "hold"     ? "2026年度 業務引き継ぎ管理"    :
         phase === "scramble" ? "Resolving fiscal archive…"     :
                               "15 months  ·  2025.09 — 2026.11"}
      </p>

      {/* ── Corner marks (technical feel) ── */}
      {[["0 0","tl"],["100% 0","tr"],["0 100%","bl"],["100% 100%","br"]].map(([pos, key]) => {
        const [rx, ry] = pos.split(" ");
        const x = rx === "0" ? 20 : undefined;
        const r = rx !== "0" ? 20 : undefined;
        const t = ry === "0" ? 20 : undefined;
        const b = ry !== "0" ? 20 : undefined;
        return (
          <svg key={key} width="12" height="12" style={{
            position: "absolute",
            left: x, right: r, top: t, bottom: b,
            opacity: 0.25,
          }}>
            <line x1={rx==="0"?"0":"12"} y1="0"  x2={rx==="0"?"0":"12"} y2="12" stroke={T.ink} strokeWidth="1"/>
            <line x1="0" y1={ry==="0"?"0":"12"} x2="12" y2={ry==="0"?"0":"12"} stroke={T.ink} strokeWidth="1"/>
          </svg>
        );
      })}
    </div>
  );
}

/* ─────────────────────────────────────────────
   APP ROOT
───────────────────────────────────────────── */
const PAGE_TITLE = { manuals: "マニュアル一覧", calendar: "業務日程カレンダー", notes: "その他注意事項" };

export default function App() {
  const [intro,  setIntro]  = useState(true);   // show intro on first load
  const [view,   setView]   = useState("home");
  const [events, setEvents] = useState(SEED);

  const addEvt = e  => setEvents(p => [...p, e]);
  const delEvt = id => setEvents(p => p.filter(e => e.id !== id));

  return (
    <>
      <style dangerouslySetInnerHTML={{ __html: GLOBAL_CSS }} />
      {intro && <IntroAnimation onComplete={() => setIntro(false)} />}
      <div style={{ minHeight: "100vh", background: T.paper, fontFamily: T.fb }}>

        {/* ── Header ── */}
        <header style={{
          position: "sticky", top: 0, zIndex: 40,
          background: "rgba(246,244,238,0.85)", backdropFilter: "blur(16px)",
          borderBottom: `1px solid ${T.line}`,
        }}>
          <div style={{
            maxWidth: 900, margin: "0 auto", padding: "0 24px",
            height: 52, display: "flex", alignItems: "center",
            justifyContent: "space-between", position: "relative",
          }}>
            {view !== "home" ? (
              <button onClick={() => setView("home")}
                onMouseEnter={e => e.currentTarget.style.color = T.ink}
                onMouseLeave={e => e.currentTarget.style.color = T.mid}
                style={{
                  display: "flex", alignItems: "center", gap: 6,
                  fontSize: 12, color: T.mid, border: "none",
                  background: "transparent", cursor: "pointer",
                  fontFamily: T.fb, transition: "color .14s",
                }}>
                <ArrowLeft size={13} />ホーム
              </button>
            ) : (
              <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                {/* Logomark: 2×2 grid */}
                <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
                  <rect x="1" y="1" width="8" height="8" rx="2.5" fill={T.ink} />
                  <rect x="11" y="1" width="8" height="8" rx="2.5" fill={T.muted} />
                  <rect x="1" y="11" width="8" height="8" rx="2.5" fill={T.muted} />
                  <rect x="11" y="11" width="8" height="8" rx="2.5" fill={T.ink} />
                </svg>
                <span style={{ fontSize: 13, fontWeight: 500, color: T.ink, fontFamily: T.fb }}>引き継ぎ管理</span>
                <span style={{ fontSize: 9, color: T.muted, fontFamily: T.fm, letterSpacing: "0.06em" }}>2026年度</span>
              </div>
            )}

            {view !== "home" && (
              <span style={{
                position: "absolute", left: "50%", transform: "translateX(-50%)",
                fontSize: 13, fontWeight: 500, color: T.ink, fontFamily: T.fb,
              }}>{PAGE_TITLE[view]}</span>
            )}
            <div style={{ width: 64 }} />
          </div>
        </header>

        {/* ── Main ── */}
        <main style={{ maxWidth: 900, margin: "0 auto", padding: "2.5rem 24px 6rem" }}>
          {view === "home"     && <HomePage setView={setView} events={events} />}
          {view === "manuals"  && <ManualsPage />}
          {view === "calendar" && <CalendarPage events={events} onAdd={addEvt} onDelete={delEvt} />}
          {view === "notes"    && <NotesPage />}
        </main>
      </div>
    </>
  );
}
