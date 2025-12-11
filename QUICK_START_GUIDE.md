# Quick Start Guide - Auto Trade Plotting

## 🚀 Get Started in 3 Steps

### Step 1: Add to TradingView
1. Copy the updated `fractal_model_indicator.pine` code
2. Open TradingView Pine Editor
3. Paste the code
4. Click "Add to Chart"

### Step 2: Enable Trade Plotting
1. Click the ⚙️ settings icon on the indicator
2. Scroll to **"Auto Trade Plotting"** section
3. Check ✅ **"Show Trade Setups"**

### Step 3: Configure (Recommended Settings)
```
✅ Show Trade Setups: ON
📍 Entry Type: CISD Breakout
🛑 Stop Loss Type: Below Sweep
🎯 Target Type: Multiple
🟢 Long Color: Green
🔴 Short Color: Red
📝 Show Labels: ON
📏 Label Size: Small
```

---

## What You'll See

When a fractal pattern forms, you'll automatically see:

### Bullish Setup (Long):
```
$4,257 ········· TP3 (green dotted)
$4,245 ········· TP2 (green dotted)
$4,236 ········· TP1 (green dotted)
$4,215 ━━━━━━━━ ENTRY (green solid) ━━━━━━ R:R 6:1
$4,208 - - - - - STOP (red dashed)
```

### Bearish Setup (Short):
```
$4,250 - - - - - STOP (red dashed)
$4,257 ━━━━━━━━ ENTRY (red solid) ━━━━━━━━ R:R 6:1
$4,245 ········· TP1 (green dotted)
$4,235 ········· TP2 (green dotted)
$4,220 ········· TP3 (green dotted)
```

---

## How to Trade

### When You See a Setup:

1. **Check the R:R ratio** (shown on right side)
   - Minimum 1:2 recommended
   - 1:3 or better is ideal

2. **Wait for entry confirmation**
   - CISD Breakout: Price breaks the entry line
   - Immediate: Enter right away
   - Fractal Zone: Wait for pullback

3. **Place your orders**
   - Entry: At the solid line
   - Stop: At the dashed line
   - Targets: At the dotted lines

4. **Manage the trade**
   - Take 25% profit at TP1
   - Take 50% profit at TP2
   - Trail stop to TP3

---

## Example Trade

### Gold Bullish Setup (From Your Chart):

**What Happened:**
- 01:00 AM: Sweep low at $4,206
- 01:30 AM: CISD breakout at $4,215
- Trade plot appeared automatically

**Trade Details:**
```
Entry:  $4,215 (CISD breakout)
Stop:   $4,208 (7 points risk)
TP1:    $4,225 (10 points) ✅ Hit at 02:00
TP2:    $4,245 (30 points) ✅ Hit at 09:00
TP3:    $4,257 (42 points) ✅ Hit at 11:00
R:R:    1:6
Result: +42 points = $420 profit per contract
```

---

## Customization Options

### Conservative Trader:
```
Entry Type: Fractal Zone
Stop Loss: Below Sweep
Target Type: Fractal Midpoint
```
- Safer entries
- Wider stops
- Single target
- Lower R:R but higher win rate

### Aggressive Trader:
```
Entry Type: Immediate
Stop Loss: Below Fractal
Target Type: Multiple
```
- Faster entries
- Tighter stops
- Multiple targets
- Higher R:R but more stop-outs

### Balanced Trader (Recommended):
```
Entry Type: CISD Breakout
Stop Loss: Below Sweep
Target Type: Multiple
```
- Confirmed entries
- Safe stops
- Multiple targets
- Good R:R with decent win rate

---

## Tips

### ✅ DO:
- Wait for fractal to fully form
- Check R:R ratio before entering
- Use proper position sizing
- Take partial profits at targets
- Trail your stop loss

### ❌ DON'T:
- Enter before fractal confirms
- Ignore the stop loss
- Risk more than 1-2% per trade
- Move stop loss further away
- Chase price if you miss entry

---

## Troubleshooting

**Q: Lines not showing?**
A: Check "Show Trade Setups" is enabled in settings

**Q: Too many lines on chart?**
A: Reduce "Max Display" setting to show fewer fractals

**Q: Labels overlapping?**
A: Change "Label Size" to Tiny or disable labels

**Q: Targets too far?**
A: Change "Target Type" to "Fractal Midpoint"

**Q: Stops too wide?**
A: Change "Stop Loss Type" to "Below Fractal" (use carefully!)

---

## Next Steps

1. ✅ Test on demo account first
2. ✅ Backtest on historical data
3. ✅ Find your optimal settings
4. ✅ Set up alerts for fractals
5. ✅ Start with small position sizes
6. ✅ Keep a trade journal
7. ✅ Scale up gradually

---

## Support

For questions or issues:
1. Check the full documentation: `TRADE_PLOTTING_FEATURE.md`
2. Review your indicator settings
3. Test on different timeframes
4. Adjust settings to match your style

---

**You're all set! The indicator will now automatically plot your trades. Happy trading! 🎯**
