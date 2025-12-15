# CRT + CISD + Displacement + SMT Indicator Documentation

## 📊 Overview

The **CRT + CISD + Displacement + SMT** indicator is a comprehensive institutional trading system that combines four powerful concepts to identify high-probability trade setups:

- **CRT (Candle Range Theory)**: Market structure and range analysis
- **CISD (Change in State of Delivery)**: Institutional order flow detection  
- **Displacement**: Momentum and directional bias confirmation
- **SMT (Smart Money Technique)**: Multi-asset divergence analysis

## 🎯 Core Components

### 1. CRT (Candle Range Theory)
**Purpose**: Identifies institutional accumulation/distribution ranges and key levels

**Logic**:
- Analyzes multiple timeframes (1H, 4H, 6H, Daily, Weekly, Monthly)
- Creates horizontal ranges showing institutional interest zones
- Provides entry/exit levels within established ranges
- Color-coded by timeframe for easy identification

**Visual Elements**:
- **Blue lines**: 1H ranges
- **Green lines**: 4H ranges  
- **Dark green lines**: 6H ranges
- **Black lines**: Daily ranges
- **Purple lines**: Weekly ranges
- **Red lines**: Monthly ranges

### 2. CISD (Change in State of Delivery)
**Purpose**: Detects when institutional players change their market delivery method

**Detection Logic**:
```pine
// Bullish CISD: After low sweep, price breaks back above CISD level
cisd_bullish := recent_low_sweep and close > cisd_level and was_below_cisd and close > open

// Bearish CISD: After high sweep, price breaks back below CISD level  
cisd_bearish := recent_high_sweep and close < cisd_level and was_above_cisd and close < open
```

**Key Features**:
- Requires recent sweep confirmation
- Validates momentum direction (close vs open)
- Confirms timing (was recently on opposite side)
- Creates purple horizontal levels on chart

### 3. Displacement Detection
**Purpose**: Identifies strong directional moves that indicate institutional participation

**Characteristics**:
- Large candle bodies relative to recent price action
- Volume confirmation (when available)
- Breaks through key levels with conviction
- Often precedes or follows CISD signals

### 4. SMT (Smart Money Technique)
**Purpose**: Analyzes divergence between correlated assets to identify institutional positioning

**🔑 KEY CONCEPT: HTF Sweeps → LTF Entries**

**Sweep Detection Logic**:
- **Sweeps are detected on HIGHER timeframes** (HTF)
- **Entries are taken on LOWER timeframes** (LTF)
- **HTF sweep provides directional bias for LTF precision entries**

**Timeframe Hierarchy**:
| Your Chart TF | HTF Sweep Detection | Purpose |
|---------------|-------------------|---------|
| **1m-15m** | **1H sweeps** | HTF bias for scalp entries |
| **30m-1H** | **4H sweeps** | HTF bias for intraday entries |
| **2H-4H** | **Daily sweeps** | HTF bias for swing entries |
| **Daily+** | **Weekly sweeps** | HTF bias for position entries |

**Sweep Types**:
| Type | Logic | Meaning |
|------|-------|---------|
| **XH Sweep** | `xh0 > xh1 and xc0 < xh1` | Main asset breaks HTF high, correlated fails |
| **XL Sweep** | `xl0 < xl1 and xc0 > xl1` | Main asset breaks HTF low, correlated fails |
| **CH Sweep** | `ch0 > ch1 and cc0 < ch1` | Correlated breaks HTF high, main fails |
| **CL Sweep** | `cl0 < cl1 and cc0 > cl1` | Correlated breaks HTF low, main fails |

**Default Correlation**: XAUUSD (Gold) ↔ XAGUSD (Silver)

## 🔥 Signal Strength Scoring System

The indicator uses a point-based system to determine trade quality:

### Point Values (Customizable)
| Signal Type | Default Points | Range | Weight |
|-------------|----------------|-------|--------|
| **SMT Confirmation** | 3.0 | 0.5-5.0 | Highest |
| **Double Sweep** | 2.5 | 0.5-5.0 | High |
| **CRT Touch/Zone** | 2.0 | 0.5-5.0 | Medium-High |
| **CISD Break** | 1.5 | 0.5-5.0 | Medium |
| **Single Sweep** | 1.0 | 0.5-5.0 | Low |

### Entry Requirements (Configurable)
- **Minimum Entry Score**: Default 4.0 (adjustable 1.0-10.0)
- **Directional bias** must be stronger than opposing direction
- **Multiple confirmations** prevent false signals
- **Real-time score breakdown** available in optional table

### High-Probability Combinations
✅ **SMT + CISD** = 3.0 + 1.5 = **4.5 points**  
✅ **SMT + Single Sweep** = 3.0 + 1.0 = **4.0 points**  
✅ **Double Sweep + CRT Touch** = 2.5 + 2.0 = **4.5 points**  
✅ **Double Sweep + CISD** = 2.5 + 1.5 = **4.0 points**  
✅ **CRT + CISD + Single Sweep** = 2.0 + 1.5 + 1.0 = **4.5 points**

## 🎯 HTF Sweep → LTF Entry Concept

### **The Core Logic**

**Higher Timeframe (HTF) Analysis**:
- Sweeps are detected on higher timeframes to identify **institutional bias**
- HTF sweeps show where **smart money** is positioning
- Provides **directional context** for lower timeframe entries

**Lower Timeframe (LTF) Execution**:
- Entries are taken on your **current chart timeframe**
- Uses HTF bias for **precision timing**
- Combines HTF sweep + LTF CISD + LTF price action

### **Example Workflow**

**Scenario**: Trading on 5-minute chart
1. **HTF Analysis**: 1H timeframe shows **XL Sweep** (bullish bias)
   - Gold breaks 1H low, Silver fails to break 1H low
   - This creates **bullish institutional bias**

2. **LTF Entry Setup**: Wait for 5-minute chart signals
   - **CISD level** created after the HTF sweep
   - **Price breaks above CISD** on 5-minute chart
   - **CRT touch** or **additional confirmations**

3. **Signal Strength Calculation**:
   - HTF XL Sweep: +1.0-2.5 points
   - LTF CISD break: +1.5 points  
   - LTF CRT touch: +2.0 points
   - **Total: 4.5+ points** → **Entry triggered**

### **Why This Works**

**Institutional Flow**:
- **HTF sweeps** = Smart money positioning
- **LTF entries** = Retail precision timing
- **Combination** = Trade with institutions, enter with precision

**Risk Management**:
- **HTF bias** reduces directional risk
- **LTF timing** improves entry precision
- **Multi-timeframe** confirmation increases probability

## 📈 Entry Model

### Trade Detection Process

1. **Timeframe Analysis**
   ```pine
   if current_tf_seconds <= timeframe.in_seconds("15")
       // Use 1H SMT signals for 1m-15m charts
   else if current_tf_seconds <= timeframe.in_seconds("60")
       // Use 4H SMT signals for 30m-1H charts  
   else if current_tf_seconds <= timeframe.in_seconds("240")
       // Use Daily SMT signals for 2H-4H charts
   else
       // Use Weekly SMT signals for Daily+ charts
   ```

2. **Signal Validation**
   - Check for recent sweeps in appropriate timeframe
   - Validate CISD level breaks with momentum
   - Confirm CRT range positioning
   - Calculate total signal strength

3. **Entry Trigger**
   ```pine
   if signal_strength >= 4.0 and signal_direction != ""
       // Create trade levels automatically
       createTradeLevels(direction, entry, sl, tp1, tp2, tp3, strength)
   ```

### Trade Level Calculation

**Within CRT Range**:
- **Entry**: 10% from CRT boundary toward center
- **Stop Loss**: Just outside CRT boundary (risk management)
- **TP1**: CRT midpoint (50% of range)
- **TP2**: Opposite CRT boundary (full range)
- **TP3**: 150% of range extension

**Outside CRT Range** (Fallback):
- **Entry**: Current price ± (ATR × 0.1)
- **Stop Loss**: ATR × 0.8 from entry
- **Targets**: Risk multiples (0.5R, 1R, 1.5R)

## 🎨 Visual Elements

### Trade Lines (Historical Display)
The indicator maintains the **last 3 trade setups** with transparency levels:

- **Most Recent**: 20% transparency (bright)
- **Second Recent**: 50% transparency (medium)
- **Oldest**: 75% transparency (faded)

### Line Colors
- **Entry Lines**: Yellow (solid)
- **Stop Loss Lines**: Red (dashed)
- **Target Lines**: Green (dotted, varying thickness)

### Debug Features
- **CISD Triangles**: Green ↑ (bullish) / Red ↓ (bearish)
- **Status Table**: Real-time signal information
- **SMT Table**: Multi-timeframe correlation analysis

## ⚙️ Configuration

### Entry Score Settings
**Customize signal strength requirements and point values:**

**Minimum Entry Score**:
- **Default**: 4.0 points
- **Range**: 1.0 - 10.0 points
- **Purpose**: Set how strict entry requirements are

**Signal Point Values** (all adjustable 0.5-5.0):
- **SMT Confirmation**: 3.0 (institutional divergence)
- **Double Sweep**: 2.5 (both assets sweep)
- **CRT Touch/Zone**: 2.0 (range boundary interaction)
- **CISD Break**: 1.5 (state change confirmation)
- **Single Sweep**: 1.0 (single asset sweep)

**Score Display Options**:
- **Show Score Breakdown**: Real-time table with active signals
- **Table Position**: Top/Bottom Left/Right placement
- **Live Updates**: See exactly which signals are contributing points

**Example Configurations**:
- **Conservative**: Min 5.0 points (fewer, higher quality trades)
- **Aggressive**: Min 3.0 points (more frequent entries)
- **Balanced**: Min 4.0 points (default institutional standard)

### CRT Settings
- **Timeframes**: Toggle H1, H4, H6, D, W, M ranges
- **Colors**: Customizable for each timeframe
- **Line Style**: Solid, dotted, or dashed
- **Thickness**: 1-4 pixel width

### SMT Settings  
- **Symbols**: Primary and correlated asset pairs
- **Timeframes**: 7 different timeframe analyses
- **Display**: Toggle SMT lines and sweep indicators
- **Alerts**: Bullish/bearish signal notifications

### CISD Settings
- **Display**: Show/hide CISD levels
- **History**: Keep all levels or latest only
- **Colors**: Bullish (green) / Bearish (red)

### Trade Settings
- **Auto Levels**: Enable/disable automatic trade level plotting
- **Labels**: Show/hide trade information labels
- **History**: Display last 3 setups with transparency

## 🚀 Usage Workflow

### 1. Setup Phase
- Configure desired timeframes for CRT analysis
- Set up SMT correlation pairs (default: Gold/Silver)
- Enable trade level automation
- Adjust visual preferences

### 2. Analysis Phase
- Wait for CRT ranges to establish
- Monitor SMT table for divergence signals
- Watch for sweep confirmations
- Look for CISD level creation

### 3. Entry Phase
- Signal strength reaches 4.0+ points
- Multiple confirmations align
- Trade levels automatically appear
- Entry, SL, and TP lines plotted

### 4. Management Phase
- Monitor price action relative to CRT ranges
- Watch for additional CISD confirmations
- Manage risk according to plotted levels
- Track institutional flow changes

## 📊 Timeframe Recommendations

| Chart TF | SMT Analysis TF | CRT Analysis TF | Best For |
|----------|----------------|-----------------|----------|
| 1m-15m | 1H | 1H-4H | Scalping |
| 30m-1H | 4H | 4H-Daily | Intraday |
| 2H-4H | Daily | Daily-Weekly | Swing |
| Daily+ | Weekly | Weekly-Monthly | Position |

## ⚠️ Important Notes

### Limitations
- Requires correlated asset data for SMT analysis
- Best performance on liquid markets (Forex, Gold, Indices)
- Signal quality depends on market conditions
- Multiple timeframe analysis needed for confirmation

### Best Practices
- Use appropriate timeframe combinations
- Wait for minimum 4.0 signal strength
- Respect CRT range boundaries
- Monitor institutional flow changes
- Combine with additional confluence factors

### Risk Management
- Always use stop losses (automatically calculated)
- Position size according to account risk
- Monitor correlation strength between assets
- Be aware of news events affecting institutional flow

## 🔧 Technical Implementation

### Key Functions
- `detectTradeSetup()`: Main signal detection logic
- `calculateTradeLevels()`: Entry/exit level calculation  
- `createTradeLevels()`: Visual trade line creation
- `manageTradeHistory()`: Historical display management
- `f_smt()`: Smart Money Technique analysis

### Performance Optimizations
- Maximum 4000 bars lookback
- Efficient array management for historical data
- Conditional calculations based on timeframe
- Optimized visual element creation

This indicator represents a comprehensive institutional trading approach, combining multiple proven concepts into a single, automated system for identifying high-probability trade opportunities.