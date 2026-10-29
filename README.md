# Uttam-Deb
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>U-Y Booking Request</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,600;12..96,800&family=DM+Sans:wght@400;500;700&display=swap">
<style>
/* Layout: slim brand bar, a short headline, then one booking card with service tabs; request goes to WhatsApp. */
:root {
  --bg: #f3f6f5;
  --surface: #ffffff;
  --fg: #12262b;
  --muted: #5a6e72;
  --line: #d5e0de;
  --brand: #0b5c63;
  --brand-fg: #ffffff;
  --accent: #e8590c;
  --accent-fg: #ffffff;
  --wa: #128c4a;
  --wa-fg: #ffffff;
  --err: #b42318;
  --font-display: "Bricolage Grotesque", "Segoe UI", system-ui, sans-serif;
  --font-body: "DM Sans", "Segoe UI", system-ui, sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #0d1a1d; --surface: #14262a; --fg: #e6f0ee; --muted: #93a9ac; --line: #27413f;
    --brand: #4fb3ba; --brand-fg: #0d1a1d; --accent: #ff8a4c; --accent-fg: #1a0e06;
    --wa: #2bbf6e; --wa-fg: #06210f; --err: #ff8f84; color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --bg: #0d1a1d; --surface: #14262a; --fg: #e6f0ee; --muted: #93a9ac; --line: #27413f;
  --brand: #4fb3ba; --brand-fg: #0d1a1d; --accent: #ff8a4c; --accent-fg: #1a0e06;
  --wa: #2bbf6e; --wa-fg: #06210f; --err: #ff8f84; color-scheme: dark;
}
* { box-sizing: border-box; }
body {
  background: var(--bg); color: var(--fg); font-family: var(--font-body); font-size: 16px; line-height: 1.5;
  padding-block: 0 48px;
  padding-left: max(16px, env(safe-area-inset-left, 0px));
  padding-right: max(16px, env(safe-area-inset-right, 0px));
}
.wrap { max-width: 880px; margin: 0 auto; }
header { display: flex; align-items: center; justify-content: space-between; gap: 12px; padding-block: 20px; flex-wrap: wrap; }
.logo { font-family: var(--font-display); font-weight: 800; font-size: 28px; letter-spacing: -0.02em; display: flex; align-items: center; gap: 10px; }
.logo i { width: 34px; height: 34px; background: var(--brand); border-radius: 9px 9px 9px 2px; display: inline-block; position: relative; }
.logo i::after { content: ""; position: absolute; left: 8px; top: 15px; width: 18px; height: 3px; background: var(--brand-fg); transform: rotate(-28deg); border-radius: 2px; box-shadow: 0 0 0 0 transparent; }
.logo b { color: var(--accent); font-weight: 800; }
.reach { color: var(--muted); font-size: 14px; }
.reach strong { color: var(--fg); font-variant-numeric: tabular-nums; }
h1 { font-family: var(--font-display); font-weight: 800; font-size: clamp(30px, 6vw, 48px); line-height: 1.05; letter-spacing: -0.025em; margin: 18px 0 10px; text-wrap: balance; }
.lead { color: var(--muted); max-width: 56ch; margin: 0 0 24px; }
.card { background: var(--surface); border: 1px solid var(--line); border-radius: 16px; padding: 20px; }
.tabs { display: flex; gap: 6px; flex-wrap: wrap; margin-bottom: 18px; }
.tab { font: inherit; font-weight: 700; font-size: 15px; padding: 9px 18px; border-radius: 999px; border: 1px solid var(--line); background: transparent; color: var(--fg); cursor: pointer; }
.tab[aria-selected="true"] { background: var(--brand); color: var(--brand-fg); border-color: var(--brand); }
.trip { display: flex; gap: 18px; margin-bottom: 14px; }
.trip label { display: flex; align-items: center; gap: 6px; font-weight: 500; cursor: pointer; }
.grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 14px; }
.f { display: flex; flex-direction: column; gap: 5px; min-width: 0; }
.f.span2 { grid-column: span 2; }
.f.span4 { grid-column: span 4; }
.f > span { font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted); font-weight: 700; }
input, select, textarea {
  font: inherit; color: var(--fg); background: var(--bg); border: 1px solid var(--line); border-radius: 10px;
  padding: 11px 12px; width: 100%; min-width: 0;
}
textarea { resize: vertical; min-height: 64px; }
input:focus-visible, select:focus-visible, textarea:focus-visible, .tab:focus-visible, .send:focus-visible, .copy:focus-visible {
  outline: 3px solid var(--accent); outline-offset: 2px;
}
.bad { border-color: var(--err); }
.hr { border: 0; border-top: 1px dashed var(--line); margin: 22px 0 18px; }
.actions { display: flex; align-items: center; gap: 14px; flex-wrap: wrap; margin-top: 20px; }
.send {
  display: inline-flex; align-items: center; gap: 10px; background: var(--wa); color: var(--wa-fg); text-decoration: none;
  font-weight: 700; font-size: 17px; padding: 14px 26px; border-radius: 12px;
}
.send svg { width: 22px; height: 22px; fill: currentColor; }
.copy { font: inherit; font-weight: 700; background: transparent; color: var(--brand); border: 1px solid var(--line); border-radius: 10px; padding: 12px 16px; cursor: pointer; }
.msg { font-size: 14px; color: var(--muted); }
.msg.err { color: var(--err); font-weight: 500; }
.preview { margin-top: 20px; }
.preview h2 { font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted); margin: 0 0 8px; }
.preview pre { margin: 0; white-space: pre-wrap; overflow-wrap: anywhere; font-family: var(--font-body); font-size: 14px; background: var(--bg); border: 1px solid var(--line); border-radius: 10px; padding: 12px 14px; }
.steps { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 14px; margin-top: 26px; color: var(--muted); font-size: 14px; }
.steps b { color: var(--fg); display: block; }
footer { margin-top: 28px; color: var(--muted); font-size: 13px; }
[data-svc] { display: none; }
[data-svc].on { display: flex; }
@media (max-width: 680px) {
  .grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .f.span4 { grid-column: span 2; }
  .steps { grid-template-columns: 1fr; }
  .send { width: 100%; justify-content: center; }
}
@media (prefers-reduced-motion: no-preference) {
  .tab, .send { transition: background-color .15s, color .15s; }
}
body{margin:0}
[hidden]{display:none!important}
</style>
</head>
<body>

<div class="wrap">
  <header>
    <div class="logo"><i aria-hidden="true"></i><span>U<b>-</b>Y</span></div>
    <div class="reach">Replies on WhatsApp: <strong>+91 98629 60064</strong></div>
  </header>

  <h1>Tell us where you want to go.</h1>
  <p class="lead">Fill in your trip, tap the WhatsApp button, and your request reaches us in one message. We reply with the best fare and book it for you.</p>

  <form class="card" id="form" novalidate>
    <div class="tabs" role="tablist" aria-label="Service">
      <button type="button" class="tab" role="tab" data-tab="flight" aria-selected="true">Flights</button>
      <button type="button" class="tab" role="tab" data-tab="train" aria-selected="false">Trains</button>
    </div>

    <!-- Flight -->
    <div data-svc="flight" class="on" style="flex-direction:column">
      <div class="trip" role="radiogroup" aria-label="Trip type">
        <label><input type="radio" name="trip" id="trip-one" value="One way" checked style="width:auto"> One way</label>
        <label><input type="radio" name="trip" id="trip-round" value="Round trip" style="width:auto"> Round trip</label>
      </div>
      <div class="grid">
        <label class="f span2"><span>From</span><input id="f-from" data-req placeholder="City or airport, e.g. Patna"></label>
        <label class="f span2"><span>To</span><input id="f-to" data-req placeholder="City or airport, e.g. Delhi"></label>
        <label class="f"><span>Departure</span><input type="date" id="f-dep" data-req></label>
        <label class="f" id="f-ret-wrap"><span>Return</span><input type="date" id="f-ret"></label>
        <label class="f"><span>Adults (12+)</span><select id="f-ad"><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6</option><option>7</option><option>8</option><option>9</option></select></label>
        <label class="f"><span>Children (2-11)</span><select id="f-ch"><option>0</option><option>1</option><option>2</option><option>3</option><option>4</option></select></label>
        <label class="f"><span>Infants (0-2)</span><select id="f-in"><option>0</option><option>1</option><option>2</option><option>3</option><option>4</option></select></label>
        <label class="f"><span>Class</span><select id="f-cl"><option>Economy</option><option>Premium Economy</option><option>Business</option><option>First</option></select></label>
      </div>
    </div>

    <!-- Train -->
    <div data-svc="train" style="flex-direction:column">
      <div class="grid">
        <label class="f span2"><span>From station</span><input id="t-from" data-req placeholder="e.g. Patna Junction (PNBE)"></label>
        <label class="f span2"><span>To station</span><input id="t-to" data-req placeholder="e.g. New Delhi (NDLS)"></label>
        <label class="f"><span>Travel date</span><input type="date" id="t-dt" data-req></label>
        <label class="f"><span>Passengers</span><select id="t-px"><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6</option></select></label>
        <label class="f"><span>Class</span><select id="t-cl"><option>Any</option><option>Sleeper (SL)</option><option>3rd AC (3A)</option><option>2nd AC (2A)</option><option>1st AC (1A)</option><option>Chair Car (CC)</option><option>Second Sitting (2S)</option></select></label>
        <label class="f"><span>Quota</span><select id="t-qt"><option>General</option><option>Tatkal</option><option>Ladies</option><option>Senior Citizen</option></select></label>
        <label class="f span4"><span>Train name or number (optional)</span><input id="t-tr" placeholder="e.g. 12394 Sampoorna Kranti Express"></label>
      </div>
    </div>

    <hr class="hr">

    <div class="grid">
      <label class="f span2"><span>Your name</span><input id="name" data-req autocomplete="name" placeholder="Full name"></label>
      <label class="f span2"><span>Your phone number</span><input id="phone" data-req type="tel" inputmode="tel" autocomplete="tel" placeholder="10-digit mobile number"></label>
      <label class="f span4"><span>Anything else? (optional)</span><textarea id="note" placeholder="Preferred time, meal, extra baggage, special request"></textarea></label>
    </div>

    <div class="actions">
      <a class="send" id="send" href="#" target="_blank" rel="noopener">
        <svg viewBox="0 0 32 32" aria-hidden="true"><path d="M16 3C9 3 3.4 8.6 3.4 15.5c0 2.3.6 4.4 1.7 6.3L3 29l7.4-2c1.8 1 3.800 1.500 5.900 1.500 6.900 0 12.500-5.600 12.500-12.500S22.900 3 16 3zm0 22.900c-1.900 0-3.700-.5-5.300-1.500l-.4-.2-4.400 1.200 1.200-4.300-.3-.4a10.300 10.300 0 0 1-1.600-5.500C5.200 9.700 10 5.100 16 5.100s10.800 4.700 10.800 10.400S21.900 25.900 16 25.900zm5.800-7.700c-.3-.2-1.900-.9-2.200-1s-.5-.2-.7.200-.8 1-1 1.200-.4.200-.7.100a8.600 8.600 0 0 1-4.300-3.700c-.3-.6.300-.6.900-1.800.1-.2 0-.4 0-.5l-1-2.300c-.2-.6-.5-.5-.7-.5h-.6c-.2 0-.6.100-.9.400s-1.200 1.200-1.200 2.800 1.200 3.300 1.400 3.500 2.400 3.700 5.800 5.100c2.100.9 2.900.9 4 .8.600-.1 1.900-.8 2.200-1.500s.3-1.400.2-1.500-.3-.2-.6-.4z"/></svg>
        <span>Send request on WhatsApp</span>
      </a>
      <button type="button" class="copy" id="copy">Copy message</button>
      <span class="msg" id="status" role="status">Opens WhatsApp with your request already written.</span>
    </div>

    <div class="preview">
      <h2>Message that will be sent</h2>
      <pre id="preview"></pre>
    </div>
  </form>

  <div class="steps">
    <div><b>1. Fill the form</b>Choose flight or train and enter your trip.</div>
    <div><b>2. Send on WhatsApp</b>Tap the green button. Your message is written for you.</div>
    <div><b>3. We confirm</b>We reply with price and options, then book after you agree.</div>
  </div>

  <footer>U-Y takes booking requests only. Nothing is booked and no payment is taken until we confirm with you on WhatsApp.</footer>
</div>

<script>
(function () {
  var NUMBER = "919862960064";
  var $ = function (id) { return document.getElementById(id); };
  var tab = "flight";
  var titles = { flight: "Flight", train: "Train" };

  function iso(d) { return d.getFullYear() + "-" + String(d.getMonth() + 1).padStart(2, "0") + "-" + String(d.getDate()).padStart(2, "0"); }
  var today = iso(new Date());
  document.querySelectorAll('input[type="date"]').forEach(function (el) { el.min = today; });

  function fmt(v) {
    if (!v) return "-";
    var p = v.split("-");
    var m = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];
    var d = new Date(+p[0], +p[1] - 1, +p[2]);
    var w = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"][d.getDay()];
    return w + ", " + p[2] + " " + m[+p[1] - 1] + " " + p[0];
  }
  function val(id) { return ($(id).value || "").trim(); }

  function build() {
    var L = [];
    L.push("*New booking request - U-Y*");
    L.push("Service: " + titles[tab]);
    if (tab === "flight") {
      var round = $("trip-round").checked;
      L.push("Trip: " + (round ? "Round trip" : "One way"));
      L.push("From: " + (val("f-from") || "-"));
      L.push("To: " + (val("f-to") || "-"));
      L.push("Departure: " + fmt($("f-dep").value));
      if (round) L.push("Return: " + fmt($("f-ret").value));
      L.push("Travellers: " + $("f-ad").value + " adult, " + $("f-ch").value + " child, " + $("f-in").value + " infant");
      L.push("Class: " + $("f-cl").value);
    } else {
      L.push("From: " + (val("t-from") || "-"));
      L.push("To: " + (val("t-to") || "-"));
      L.push("Date: " + fmt($("t-dt").value));
      L.push("Passengers: " + $("t-px").value);
      L.push("Class: " + $("t-cl").value);
      L.push("Quota: " + $("t-qt").value);
      if (val("t-tr")) L.push("Train: " + val("t-tr"));
    }
    L.push("");
    L.push("Name: " + (val("name") || "-"));
    L.push("Phone: " + (val("phone") || "-"));
    if (val("note")) L.push("Note: " + val("note"));
    return L.join("\n");
  }

  function refresh() {
    var text = build();
    $("preview").textContent = text;
    $("send").href = "https://wa.me/" + NUMBER + "?text=" + encodeURIComponent(text);
  }

  function activeFields() {
    var out = [];
    document.querySelectorAll('[data-svc="' + tab + '"] [data-req]').forEach(function (e) { out.push(e); });
    out.push($("name"), $("phone"));
    return out;
  }

  function validate() {
    var first = null, msg = "";
    document.querySelectorAll(".bad").forEach(function (e) { e.classList.remove("bad"); });
    activeFields().forEach(function (e) {
      var v = e.value.trim(), bad = !v;
      if (e.id === "phone" && v && v.replace(/\D/g, "").length < 10) bad = true;
      if (bad) { e.classList.add("bad"); if (!first) first = e; }
    });
    if (tab === "flight" && $("trip-round").checked) {
      if (!$("f-ret").value) { $("f-ret").classList.add("bad"); if (!first) first = $("f-ret"); }
    }
    if (first) msg = first.id === "phone" ? "Enter a valid 10-digit phone number." : "Please fill the highlighted fields.";
    return { first: first, msg: msg };
  }

  function setStatus(t, err) { var s = $("status"); s.textContent = t; s.className = "msg" + (err ? " err" : ""); }

  function setTab(t) {
    tab = t;
    document.querySelectorAll(".tab").forEach(function (b) { b.setAttribute("aria-selected", b.dataset.tab === t ? "true" : "false"); });
    document.querySelectorAll("[data-svc]").forEach(function (d) { d.classList.toggle("on", d.dataset.svc === t); });
    setStatus("Opens WhatsApp with your request already written.");
    refresh();
  }

  document.querySelectorAll(".tab").forEach(function (b) { b.addEventListener("click", function () { setTab(b.dataset.tab); }); });

  function syncTrip() {
    var round = $("trip-round").checked;
    $("f-ret-wrap").style.display = round ? "" : "none";
    refresh();
  }
  $("trip-one").addEventListener("change", syncTrip);
  $("trip-round").addEventListener("change", syncTrip);

  $("form").addEventListener("input", refresh);
  $("form").addEventListener("change", refresh);
  $("form").addEventListener("submit", function (e) { e.preventDefault(); });

  $("send").addEventListener("click", function (e) {
    var r = validate();
    if (r.first) {
      e.preventDefault();
      setStatus(r.msg, true);
      r.first.focus();
    } else {
      refresh();
      setStatus("WhatsApp opened in a new tab. Press Send there to deliver your request.");
    }
  });

  $("copy").addEventListener("click", function () {
    var text = build();
    function fallback() {
      var range = document.createRange(); range.selectNodeContents($("preview"));
      var sel = window.getSelection(); sel.removeAllRanges(); sel.addRange(range);
      setStatus("Message selected. Copy it and paste it into WhatsApp.");
    }
    try {
      navigator.clipboard.writeText(text).then(function () { setStatus("Message copied."); }, fallback);
    } catch (err) { fallback(); }
  });

  syncTrip();
})();
</script>

</body>
</html>


