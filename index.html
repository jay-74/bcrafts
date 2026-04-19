import { useState, useRef } from "react";

const INITIAL_PARTNERS = [
  "Bible Wonder Land",
  "Book Nook",
  "MBN Ikoyi",
  "MBN Lekki",
  "Deeper Life Bookshop Owerri",
  "Roving Heights",
  "Glendora",
];

function formatCurrency(val) {
  if (!val && val !== 0) return "—";
  return "₦" + Number(val).toLocaleString("en-NG", { minimumFractionDigits: 2, maximumFractionDigits: 2 });
}

function formatDate(dateStr) {
  if (!dateStr) return "—";
  const d = new Date(dateStr);
  return d.toLocaleDateString("en-NG", { day: "2-digit", month: "short", year: "numeric" });
}

function StatusBadge({ pct }) {
  if (pct >= 100) return <span style={{ background: "#d1fae5", color: "#065f46", padding: "2px 10px", borderRadius: 99, fontSize: 12, fontWeight: 700, letterSpacing: 0.5 }}>CLEARED</span>;
  if (pct >= 70) return <span style={{ background: "#fef3c7", color: "#92400e", padding: "2px 10px", borderRadius: 99, fontSize: 12, fontWeight: 700, letterSpacing: 0.5 }}>ALMOST DONE</span>;
  return <span style={{ background: "#fee2e2", color: "#991b1b", padding: "2px 10px", borderRadius: 99, fontSize: 12, fontWeight: 700, letterSpacing: 0.5 }}>OUTSTANDING</span>;
}

export default function App() {
  const [partners, setPartners] = useState(INITIAL_PARTNERS);
  const [invoices, setInvoices] = useState([]);
  const [view, setView] = useState("dashboard"); // dashboard | partner | invoice
  const [selectedPartner, setSelectedPartner] = useState(null);
  const [selectedInvoice, setSelectedInvoice] = useState(null);
  const [showAddPartner, setShowAddPartner] = useState(false);
  const [showAddInvoice, setShowAddInvoice] = useState(false);
  const [showAddPayment, setShowAddPayment] = useState(false);
  const [newPartnerName, setNewPartnerName] = useState("");
  const [invoiceForm, setInvoiceForm] = useState({ date: "", quantity: "", description: "", amount: "" });
  const [paymentForm, setPaymentForm] = useState({ date: "", amount: "", note: "" });
  const downloadRef = useRef();

  const getInvoicesForPartner = (partner) => invoices.filter(i => i.partner === partner);

  const getTotalPaid = (inv) => (inv.payments || []).reduce((s, p) => s + Number(p.amount), 0);

  const getBalance = (inv) => Number(inv.amount) - getTotalPaid(inv);

  const getPct = (inv) => Math.min(100, (getTotalPaid(inv) / Number(inv.amount)) * 100);

  const addPartner = () => {
    const name = newPartnerName.trim();
    if (!name || partners.includes(name)) return;
    setPartners(prev => [...prev, name]);
    setNewPartnerName("");
    setShowAddPartner(false);
  };

  const addInvoice = () => {
    if (!invoiceForm.amount || !invoiceForm.date) return;
    const inv = {
      id: Date.now(),
      partner: selectedPartner,
      date: invoiceForm.date,
      quantity: invoiceForm.quantity,
      description: invoiceForm.description,
      amount: Number(invoiceForm.amount),
      payments: [],
    };
    setInvoices(prev => [...prev, inv]);
    setInvoiceForm({ date: "", quantity: "", description: "", amount: "" });
    setShowAddInvoice(false);
  };

  const addPayment = () => {
    if (!paymentForm.amount || !paymentForm.date) return;
    setInvoices(prev => prev.map(i =>
      i.id === selectedInvoice.id
        ? { ...i, payments: [...i.payments, { id: Date.now(), date: paymentForm.date, amount: Number(paymentForm.amount), note: paymentForm.note }] }
        : i
    ));
    setSelectedInvoice(prev => ({
      ...prev,
      payments: [...prev.payments, { id: Date.now(), date: paymentForm.date, amount: Number(paymentForm.amount), note: paymentForm.note }]
    }));
    setPaymentForm({ date: "", amount: "", note: "" });
    setShowAddPayment(false);
  };

  const deletePayment = (paymentId) => {
    setInvoices(prev => prev.map(i =>
      i.id === selectedInvoice.id
        ? { ...i, payments: i.payments.filter(p => p.id !== paymentId) }
        : i
    ));
    setSelectedInvoice(prev => ({
      ...prev,
      payments: prev.payments.filter(p => p.id !== paymentId)
    }));
  };

  const deleteInvoice = (invId) => {
    setInvoices(prev => prev.filter(i => i.id !== invId));
    setView("partner");
    setSelectedInvoice(null);
  };

  const getPartnerSummary = (partner) => {
    const invs = getInvoicesForPartner(partner);
    const totalBilled = invs.reduce((s, i) => s + i.amount, 0);
    const totalPaid = invs.reduce((s, i) => s + getTotalPaid(i), 0);
    const outstanding = invs.filter(i => getPct(i) < 100);
    return { totalBilled, totalPaid, balance: totalBilled - totalPaid, invoiceCount: invs.length, outstanding: outstanding.length };
  };

  const generateWordDoc = (scope) => {
    const lines = [];
    const header = `BOLUSCRAFTS — Outstanding Invoice Report\nGenerated: ${new Date().toLocaleDateString("en-NG", { day: "2-digit", month: "long", year: "numeric" })}\n${"=".repeat(60)}\n\n`;
    lines.push(header);

    const targetPartners = scope === "single" ? [selectedPartner] : partners;

    targetPartners.forEach(partner => {
      const invs = getInvoicesForPartner(partner);
      const summary = getPartnerSummary(partner);
      lines.push(`PARTNER: ${partner.toUpperCase()}`);
      lines.push(`${"—".repeat(40)}`);
      lines.push(`Total Invoiced:  ${formatCurrency(summary.totalBilled)}`);
      lines.push(`Total Paid:      ${formatCurrency(summary.totalPaid)}`);
      lines.push(`Balance Due:     ${formatCurrency(summary.balance)}`);
      lines.push(`Invoices:        ${summary.invoiceCount} total, ${summary.outstanding} outstanding\n`);

      if (invs.length === 0) {
        lines.push("  No invoices recorded.\n");
      } else {
        invs.forEach((inv, idx) => {
          const paid = getTotalPaid(inv);
          const bal = getBalance(inv);
          const pct = getPct(inv);
          lines.push(`  Invoice #${idx + 1}   |   Date: ${formatDate(inv.date)}   |   ${pct >= 100 ? "CLEARED" : "OUTSTANDING"}`);
          if (inv.description) lines.push(`  Description: ${inv.description}`);
          if (inv.quantity) lines.push(`  Qty Supplied: ${inv.quantity}`);
          lines.push(`  Invoice Value: ${formatCurrency(inv.amount)}`);
          lines.push(`  Total Paid:    ${formatCurrency(paid)}`);
          lines.push(`  Balance Left:  ${formatCurrency(bal)}`);
          if (inv.payments.length > 0) {
            lines.push(`  Payment History:`);
            inv.payments.forEach((p, pi) => {
              lines.push(`    ${pi + 1}. ${formatDate(p.date)} — ${formatCurrency(p.amount)}${p.note ? ` (${p.note})` : ""}`);
            });
          }
          lines.push("");
        });
      }
      lines.push("\n");
    });

    const content = lines.join("\n");
    const blob = new Blob([content], { type: "text/plain" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = scope === "single" ? `${selectedPartner}_Invoice_Report.txt` : "Boluscrafts_All_Partners_Report.txt";
    a.click();
    URL.revokeObjectURL(url);
  };

  const inp = {
    width: "100%", padding: "10px 14px", borderRadius: 8, border: "1.5px solid #e2e8f0",
    fontSize: 14, fontFamily: "inherit", background: "#fff", outline: "none", boxSizing: "border-box",
    color: "#1e293b",
  };

  const btn = (bg = "#1e293b", color = "#fff") => ({
    background: bg, color, border: "none", borderRadius: 8, padding: "10px 20px",
    fontFamily: "inherit", fontSize: 14, fontWeight: 600, cursor: "pointer", transition: "opacity .15s",
  });

  const modal = {
    position: "fixed", inset: 0, background: "rgba(15,23,42,.45)", zIndex: 100,
    display: "flex", alignItems: "center", justifyContent: "center", padding: 20,
  };

  const card = {
    background: "#fff", borderRadius: 16, padding: 28, boxShadow: "0 8px 32px rgba(0,0,0,.12)", width: "100%", maxWidth: 440,
  };

  // ── DASHBOARD ──
  if (view === "dashboard") {
    const allInvoices = invoices;
    const totalOutstanding = allInvoices.filter(i => getPct(i) < 100).reduce((s, i) => s + getBalance(i), 0);
    const totalCleared = allInvoices.filter(i => getPct(i) >= 100).length;

    return (
      <div style={{ minHeight: "100vh", background: "linear-gradient(135deg,#f8fafc 0%,#f1f5f9 100%)", fontFamily: "'DM Sans', system-ui, sans-serif" }}>
        <style>{`@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono&display=swap'); * { box-sizing: border-box; }`}</style>

        {/* Header */}
        <div style={{ background: "#0f172a", padding: "20px 24px", display: "flex", alignItems: "center", justifyContent: "space-between" }}>
          <div>
            <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 600, letterSpacing: 2, textTransform: "uppercase" }}>Boluscrafts</div>
            <div style={{ color: "#fff", fontSize: 20, fontWeight: 700, marginTop: 2 }}>Invoice Tracker</div>
          </div>
          <button onClick={() => generateWordDoc("all")} style={{ ...btn("#334155", "#e2e8f0"), fontSize: 12, padding: "8px 14px" }}>
            ↓ Export All
          </button>
        </div>

        <div style={{ padding: "24px 20px", maxWidth: 640, margin: "0 auto" }}>
          {/* Summary cards */}
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 12, marginBottom: 24 }}>
            {[
              { label: "Partners", value: partners.length },
              { label: "Outstanding", value: formatCurrency(totalOutstanding), highlight: true },
              { label: "Cleared Invoices", value: totalCleared },
            ].map((s, i) => (
              <div key={i} style={{ background: s.highlight ? "#0f172a" : "#fff", borderRadius: 14, padding: "16px 14px", boxShadow: "0 2px 8px rgba(0,0,0,.06)" }}>
                <div style={{ fontSize: 11, fontWeight: 600, color: s.highlight ? "#94a3b8" : "#64748b", letterSpacing: 1, textTransform: "uppercase", marginBottom: 6 }}>{s.label}</div>
                <div style={{ fontSize: s.highlight ? 16 : 22, fontWeight: 700, color: s.highlight ? "#f8fafc" : "#0f172a", fontFamily: "'DM Mono', monospace" }}>{s.value}</div>
              </div>
            ))}
          </div>

          {/* Partners list */}
          <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: 14 }}>
            <div style={{ fontSize: 15, fontWeight: 700, color: "#0f172a" }}>Partner Stores</div>
            <button onClick={() => setShowAddPartner(true)} style={{ ...btn("#e2e8f0", "#0f172a"), padding: "7px 14px", fontSize: 13 }}>+ Add Partner</button>
          </div>

          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            {partners.map(partner => {
              const s = getPartnerSummary(partner);
              const pct = s.totalBilled > 0 ? Math.min(100, (s.totalPaid / s.totalBilled) * 100) : 0;
              return (
                <div key={partner} onClick={() => { setSelectedPartner(partner); setView("partner"); }}
                  style={{ background: "#fff", borderRadius: 14, padding: "18px 20px", boxShadow: "0 2px 8px rgba(0,0,0,.06)", cursor: "pointer", transition: "transform .15s, box-shadow .15s" }}
                  onMouseEnter={e => { e.currentTarget.style.transform = "translateY(-2px)"; e.currentTarget.style.boxShadow = "0 6px 20px rgba(0,0,0,.1)"; }}
                  onMouseLeave={e => { e.currentTarget.style.transform = ""; e.currentTarget.style.boxShadow = "0 2px 8px rgba(0,0,0,.06)"; }}>
                  <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 10 }}>
                    <div>
                      <div style={{ fontWeight: 700, color: "#0f172a", fontSize: 15 }}>{partner}</div>
                      <div style={{ fontSize: 12, color: "#64748b", marginTop: 2 }}>{s.invoiceCount} invoice{s.invoiceCount !== 1 ? "s" : ""} · {s.outstanding} outstanding</div>
                    </div>
                    <div style={{ textAlign: "right" }}>
                      <div style={{ fontFamily: "'DM Mono', monospace", fontWeight: 700, color: s.balance > 0 ? "#dc2626" : "#16a34a", fontSize: 15 }}>{formatCurrency(s.balance)}</div>
                      <div style={{ fontSize: 11, color: "#94a3b8", marginTop: 1 }}>balance</div>
                    </div>
                  </div>
                  {s.totalBilled > 0 && (
                    <div style={{ height: 5, background: "#f1f5f9", borderRadius: 99, overflow: "hidden" }}>
                      <div style={{ height: "100%", width: `${pct}%`, background: pct >= 100 ? "#16a34a" : pct >= 70 ? "#f59e0b" : "#dc2626", borderRadius: 99, transition: "width .4s" }} />
                    </div>
                  )}
                </div>
              );
            })}
          </div>
        </div>

        {/* Add Partner Modal */}
        {showAddPartner && (
          <div style={modal} onClick={() => setShowAddPartner(false)}>
            <div style={card} onClick={e => e.stopPropagation()}>
              <div style={{ fontSize: 17, fontWeight: 700, color: "#0f172a", marginBottom: 18 }}>Add New Partner</div>
              <input style={inp} placeholder="Partner store name" value={newPartnerName} onChange={e => setNewPartnerName(e.target.value)} onKeyDown={e => e.key === "Enter" && addPartner()} autoFocus />
              <div style={{ display: "flex", gap: 10, marginTop: 18 }}>
                <button onClick={() => setShowAddPartner(false)} style={{ ...btn("#f1f5f9", "#64748b"), flex: 1 }}>Cancel</button>
                <button onClick={addPartner} style={{ ...btn(), flex: 1 }}>Add Partner</button>
              </div>
            </div>
          </div>
        )}
      </div>
    );
  }

  // ── PARTNER VIEW ──
  if (view === "partner") {
    const partnerInvoices = getInvoicesForPartner(selectedPartner);
    const s = getPartnerSummary(selectedPartner);

    return (
      <div style={{ minHeight: "100vh", background: "linear-gradient(135deg,#f8fafc 0%,#f1f5f9 100%)", fontFamily: "'DM Sans', system-ui, sans-serif" }}>
        <style>{`@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono&display=swap'); * { box-sizing: border-box; }`}</style>

        <div style={{ background: "#0f172a", padding: "20px 24px" }}>
          <button onClick={() => setView("dashboard")} style={{ background: "none", border: "none", color: "#94a3b8", cursor: "pointer", fontSize: 13, padding: 0, marginBottom: 8 }}>← Dashboard</button>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-end" }}>
            <div>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 600, letterSpacing: 2, textTransform: "uppercase" }}>Partner</div>
              <div style={{ color: "#fff", fontSize: 20, fontWeight: 700, marginTop: 2 }}>{selectedPartner}</div>
            </div>
            <button onClick={() => generateWordDoc("single")} style={{ ...btn("#334155", "#e2e8f0"), fontSize: 12, padding: "8px 14px" }}>↓ Export</button>
          </div>
        </div>

        <div style={{ padding: "24px 20px", maxWidth: 640, margin: "0 auto" }}>
          {/* Summary */}
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 10, marginBottom: 24 }}>
            {[
              { label: "Total Billed", value: formatCurrency(s.totalBilled) },
              { label: "Total Paid", value: formatCurrency(s.totalPaid) },
              { label: "Balance Due", value: formatCurrency(s.balance), red: s.balance > 0 },
            ].map((item, i) => (
              <div key={i} style={{ background: "#fff", borderRadius: 12, padding: "14px 12px", boxShadow: "0 2px 8px rgba(0,0,0,.06)" }}>
                <div style={{ fontSize: 10, fontWeight: 600, color: "#64748b", letterSpacing: 1, textTransform: "uppercase", marginBottom: 5 }}>{item.label}</div>
                <div style={{ fontFamily: "'DM Mono', monospace", fontWeight: 700, fontSize: 13, color: item.red ? "#dc2626" : "#0f172a" }}>{item.value}</div>
              </div>
            ))}
          </div>

          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 14 }}>
            <div style={{ fontSize: 15, fontWeight: 700, color: "#0f172a" }}>Invoices</div>
            <button onClick={() => setShowAddInvoice(true)} style={{ ...btn("#0f172a"), padding: "8px 16px", fontSize: 13 }}>+ New Invoice</button>
          </div>

          {partnerInvoices.length === 0 && (
            <div style={{ textAlign: "center", padding: "48px 0", color: "#94a3b8" }}>
              <div style={{ fontSize: 36, marginBottom: 10 }}>📋</div>
              <div style={{ fontWeight: 600 }}>No invoices yet</div>
              <div style={{ fontSize: 13, marginTop: 4 }}>Tap "+ New Invoice" to record the first supply</div>
            </div>
          )}

          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            {partnerInvoices.map((inv, idx) => {
              const paid = getTotalPaid(inv);
              const bal = getBalance(inv);
              const pct = getPct(inv);
              return (
                <div key={inv.id} onClick={() => { setSelectedInvoice(inv); setView("invoice"); }}
                  style={{ background: "#fff", borderRadius: 14, padding: "18px 20px", boxShadow: "0 2px 8px rgba(0,0,0,.06)", cursor: "pointer" }}
                  onMouseEnter={e => e.currentTarget.style.boxShadow = "0 6px 20px rgba(0,0,0,.1)"}
                  onMouseLeave={e => e.currentTarget.style.boxShadow = "0 2px 8px rgba(0,0,0,.06)"}>
                  <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
                    <div>
                      <div style={{ fontWeight: 700, color: "#0f172a", fontSize: 14 }}>Invoice #{idx + 1}</div>
                      <div style={{ fontSize: 12, color: "#64748b", marginTop: 2 }}>{formatDate(inv.date)}{inv.description ? ` · ${inv.description}` : ""}</div>
                    </div>
                    <StatusBadge pct={pct} />
                  </div>
                  <div style={{ display: "flex", justifyContent: "space-between", fontSize: 13, marginBottom: 10 }}>
                    <div><span style={{ color: "#64748b" }}>Invoiced: </span><span style={{ fontFamily: "'DM Mono'", fontWeight: 600 }}>{formatCurrency(inv.amount)}</span></div>
                    <div><span style={{ color: "#64748b" }}>Balance: </span><span style={{ fontFamily: "'DM Mono'", fontWeight: 700, color: bal > 0 ? "#dc2626" : "#16a34a" }}>{formatCurrency(bal)}</span></div>
                  </div>
                  <div style={{ height: 5, background: "#f1f5f9", borderRadius: 99, overflow: "hidden" }}>
                    <div style={{ height: "100%", width: `${pct}%`, background: pct >= 100 ? "#16a34a" : pct >= 70 ? "#f59e0b" : "#dc2626", borderRadius: 99 }} />
                  </div>
                  <div style={{ fontSize: 11, color: "#94a3b8", marginTop: 6, textAlign: "right" }}>{Math.round(pct)}% paid · {inv.payments.length} payment{inv.payments.length !== 1 ? "s" : ""}</div>
                </div>
              );
            })}
          </div>
        </div>

        {/* Add Invoice Modal */}
        {showAddInvoice && (
          <div style={modal} onClick={() => setShowAddInvoice(false)}>
            <div style={card} onClick={e => e.stopPropagation()}>
              <div style={{ fontSize: 17, fontWeight: 700, color: "#0f172a", marginBottom: 18 }}>New Invoice — {selectedPartner}</div>
              <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>SUPPLY DATE *</label>
                  <input type="date" style={inp} value={invoiceForm.date} onChange={e => setInvoiceForm(f => ({ ...f, date: e.target.value }))} />
                </div>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>INVOICE AMOUNT (₦) *</label>
                  <input type="number" style={inp} placeholder="e.g. 500000" value={invoiceForm.amount} onChange={e => setInvoiceForm(f => ({ ...f, amount: e.target.value }))} />
                </div>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>QTY SUPPLIED</label>
                  <input type="text" style={inp} placeholder="e.g. 50 journals" value={invoiceForm.quantity} onChange={e => setInvoiceForm(f => ({ ...f, quantity: e.target.value }))} />
                </div>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>DESCRIPTION / NOTES</label>
                  <input type="text" style={inp} placeholder="Optional" value={invoiceForm.description} onChange={e => setInvoiceForm(f => ({ ...f, description: e.target.value }))} />
                </div>
              </div>
              <div style={{ display: "flex", gap: 10, marginTop: 20 }}>
                <button onClick={() => setShowAddInvoice(false)} style={{ ...btn("#f1f5f9", "#64748b"), flex: 1 }}>Cancel</button>
                <button onClick={addInvoice} style={{ ...btn(), flex: 1 }}>Save Invoice</button>
              </div>
            </div>
          </div>
        )}
      </div>
    );
  }

  // ── INVOICE VIEW ──
  const inv = invoices.find(i => i.id === selectedInvoice?.id) || selectedInvoice;
  if (view === "invoice" && inv) {
    const paid = getTotalPaid(inv);
    const bal = getBalance(inv);
    const pct = getPct(inv);

    return (
      <div style={{ minHeight: "100vh", background: "linear-gradient(135deg,#f8fafc 0%,#f1f5f9 100%)", fontFamily: "'DM Sans', system-ui, sans-serif" }}>
        <style>{`@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono&display=swap'); * { box-sizing: border-box; }`}</style>

        <div style={{ background: "#0f172a", padding: "20px 24px" }}>
          <button onClick={() => setView("partner")} style={{ background: "none", border: "none", color: "#94a3b8", cursor: "pointer", fontSize: 13, padding: 0, marginBottom: 8 }}>← {selectedPartner}</button>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
            <div>
              <div style={{ color: "#94a3b8", fontSize: 11, fontWeight: 600, letterSpacing: 2, textTransform: "uppercase" }}>Invoice Detail</div>
              <div style={{ color: "#fff", fontSize: 18, fontWeight: 700, marginTop: 2 }}>{selectedPartner}</div>
            </div>
            <StatusBadge pct={pct} />
          </div>
        </div>

        <div style={{ padding: "24px 20px", maxWidth: 640, margin: "0 auto" }}>
          {/* Invoice details card */}
          <div style={{ background: "#fff", borderRadius: 16, padding: 22, boxShadow: "0 2px 12px rgba(0,0,0,.08)", marginBottom: 16 }}>
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: "12px 20px", marginBottom: 18 }}>
              {[
                { label: "Supply Date", value: formatDate(inv.date) },
                { label: "Qty Supplied", value: inv.quantity || "—" },
                { label: "Description", value: inv.description || "—" },
              ].map((r, i) => (
                <div key={i} style={i === 2 ? { gridColumn: "1/-1" } : {}}>
                  <div style={{ fontSize: 10, fontWeight: 600, color: "#94a3b8", letterSpacing: 1, textTransform: "uppercase", marginBottom: 3 }}>{r.label}</div>
                  <div style={{ fontWeight: 600, color: "#1e293b", fontSize: 14 }}>{r.value}</div>
                </div>
              ))}
            </div>

            {/* Financials */}
            <div style={{ borderTop: "1.5px solid #f1f5f9", paddingTop: 16, display: "flex", flexDirection: "column", gap: 8 }}>
              {[
                { label: "Invoice Value", value: formatCurrency(inv.amount), mono: true },
                { label: "Total Paid", value: formatCurrency(paid), mono: true, color: "#16a34a" },
                { label: "Balance Remaining", value: formatCurrency(bal), mono: true, color: bal > 0 ? "#dc2626" : "#16a34a", bold: true },
              ].map((r, i) => (
                <div key={i} style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                  <span style={{ fontSize: 13, color: "#64748b", fontWeight: r.bold ? 700 : 500 }}>{r.label}</span>
                  <span style={{ fontFamily: "'DM Mono', monospace", fontWeight: r.bold ? 800 : 600, fontSize: r.bold ? 17 : 14, color: r.color || "#0f172a" }}>{r.value}</span>
                </div>
              ))}
            </div>

            {/* Progress bar */}
            <div style={{ marginTop: 16 }}>
              <div style={{ display: "flex", justifyContent: "space-between", fontSize: 11, color: "#94a3b8", marginBottom: 6 }}>
                <span>Payment progress</span><span>{Math.round(pct)}%</span>
              </div>
              <div style={{ height: 8, background: "#f1f5f9", borderRadius: 99, overflow: "hidden" }}>
                <div style={{ height: "100%", width: `${pct}%`, background: pct >= 100 ? "#16a34a" : pct >= 70 ? "#f59e0b" : "#dc2626", borderRadius: 99, transition: "width .5s" }} />
              </div>
            </div>
          </div>

          {/* Payments */}
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 12 }}>
            <div style={{ fontSize: 15, fontWeight: 700, color: "#0f172a" }}>Payments ({inv.payments.length})</div>
            {pct < 100 && <button onClick={() => setShowAddPayment(true)} style={{ ...btn("#0f172a"), padding: "8px 16px", fontSize: 13 }}>+ Record Payment</button>}
          </div>

          {inv.payments.length === 0 && (
            <div style={{ textAlign: "center", padding: "32px 0", color: "#94a3b8" }}>
              <div style={{ fontSize: 28, marginBottom: 8 }}>💳</div>
              <div style={{ fontWeight: 600, fontSize: 14 }}>No payments recorded yet</div>
            </div>
          )}

          <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
            {[...inv.payments].sort((a, b) => new Date(a.date) - new Date(b.date)).map((p, i) => (
              <div key={p.id} style={{ background: "#fff", borderRadius: 12, padding: "14px 18px", boxShadow: "0 1px 6px rgba(0,0,0,.06)", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                <div>
                  <div style={{ fontWeight: 600, color: "#0f172a", fontSize: 14, fontFamily: "'DM Mono', monospace" }}>{formatCurrency(p.amount)}</div>
                  <div style={{ fontSize: 12, color: "#64748b", marginTop: 2 }}>{formatDate(p.date)}{p.note ? ` · ${p.note}` : ""}</div>
                </div>
                <button onClick={() => deletePayment(p.id)} style={{ background: "#fee2e2", border: "none", borderRadius: 8, padding: "5px 10px", color: "#dc2626", cursor: "pointer", fontSize: 12, fontWeight: 600 }}>Remove</button>
              </div>
            ))}
          </div>

          {/* Delete invoice */}
          <div style={{ marginTop: 32, paddingTop: 20, borderTop: "1.5px solid #f1f5f9", textAlign: "center" }}>
            <button onClick={() => { if (confirm("Delete this invoice and all its payment records?")) deleteInvoice(inv.id); }} style={{ ...btn("#fee2e2", "#dc2626"), fontSize: 13 }}>
              Delete Invoice
            </button>
          </div>
        </div>

        {/* Add Payment Modal */}
        {showAddPayment && (
          <div style={modal} onClick={() => setShowAddPayment(false)}>
            <div style={card} onClick={e => e.stopPropagation()}>
              <div style={{ fontSize: 17, fontWeight: 700, color: "#0f172a", marginBottom: 4 }}>Record Payment</div>
              <div style={{ fontSize: 13, color: "#64748b", marginBottom: 18 }}>Balance remaining: <strong style={{ color: "#dc2626", fontFamily: "'DM Mono'" }}>{formatCurrency(bal)}</strong></div>
              <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>PAYMENT DATE *</label>
                  <input type="date" style={inp} value={paymentForm.date} onChange={e => setPaymentForm(f => ({ ...f, date: e.target.value }))} />
                </div>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>AMOUNT PAID (₦) *</label>
                  <input type="number" style={inp} placeholder="e.g. 23500" value={paymentForm.amount} onChange={e => setPaymentForm(f => ({ ...f, amount: e.target.value }))} />
                </div>
                <div>
                  <label style={{ fontSize: 12, fontWeight: 600, color: "#64748b", display: "block", marginBottom: 5 }}>NOTE (Optional)</label>
                  <input type="text" style={inp} placeholder="e.g. bank transfer" value={paymentForm.note} onChange={e => setPaymentForm(f => ({ ...f, note: e.target.value }))} />
                </div>
              </div>
              <div style={{ display: "flex", gap: 10, marginTop: 20 }}>
                <button onClick={() => setShowAddPayment(false)} style={{ ...btn("#f1f5f9", "#64748b"), flex: 1 }}>Cancel</button>
                <button onClick={addPayment} style={{ ...btn(), flex: 1 }}>Save Payment</button>
              </div>
            </div>
          </div>
        )}
      </div>
    );
  }

  return null;
}
