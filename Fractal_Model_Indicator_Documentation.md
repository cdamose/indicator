# Fractal Model Indicator Documentation

## 📊 Overview

The **Fractal Model Indicator** is a comprehensive institutional trading tool that combines Higher Time Frame (HTF) candle analysis with advanced fractal pattern detection, sweep logic, and market structure labeling. This indicator provides traders with a complete view of institutional market behavior across multiple timeframes.

**Author**: © mindyourbuisness  
**Based on**: HTF Candles by Fadi  
**Version**: Pine Script v6  

## 🎯 Core Components

### 1. HTF (Higher Time Frame) Candles
**Purpose**: Display higher timeframe candle structure on lower timeframe charts for institutional context

**Key Features**:
- **Auto HTF Detection**: Automatically selects appropriate HTF based on chart timeframe
- **Custom HTF Option**: Manual timeframe selection
- **Real-time Timer**: Countdown to next HTF candle close
- **HTF Labels**: Clear timeframe identification
- **Multiple Display**: Up to 6 different HTF candles simultaneously

**Auto HTF Logic**:
- **5m and below** → **1H HTF**
- **1H and below** → **4H HTF**  
- **4H and below** → **Daily HTF**
- **Daily and below** → **Weekly HTF**
- **Above Daily** → **Monthly HTF**

### 2. Fractal Pattern Detection
**Purpose**: Identify institutional accumulation/distribution patterns and market structure changes

**Fractal Types**:
- **Bullish Fractal**: Higher lows formation indicating institutional buying
- **Bearish Fractal**: Lower highs formation indicating institutional selling
- **Neutral Fractal**: Consolidation patterns

**Pattern Recognition**:
- **3-point fractals**: Basic pattern detection
- **5-point fractals**: Advanced pattern confirmation
- **Sweep confirmation**: Validates fractal patterns with liquidity sweeps

### 3. Sweep Logic System
**Purpose**: Detect liquidity sweeps that confirm institutional positioning

**Sweep Types**:
- **High Sweeps**: Price breaks above previous high but closes below
- **Low Sweeps**: Price breaks below previous low but closes above
- **Chart Sweeps**: Sweeps on current timeframe
- **Fractal Sweeps**: Sweeps of fractal pattern levels

**Sweep Confirmation**:
- **Body Confirmation**: Uses candle body for sweep validation
- **Wick Confirmation**: Uses candle wicks for sweep detection
- **Visual Indicators**: Lines and labels marking sweep points

### 4. Market Structure Labeling
**Purpose**: Automatically label market structure changes and key levels

**Structure Labels**:
- **Higher High (HH)**: Bullish structure continuation
- **Higher Low (HL)**: Bullish structure support
- **Lower High (LH)**: Bearish structure resistance  
- **Lower Low (LL)**: Bearish structure continuation
- **Break of Structure (BOS)**: Trend change confirmation

### 5. Fair Value Gap (FVG) Detection
**Purpose**: Identify institutional imbalances for potential reversal zones

**FVG Types**:
- **Standard FVG**: Regular fair value gaps
- **First Presented FVG (PFVG)**: Initial FVG in HTF candle
- **Volume Imbalance**: Price gaps with volume confirmation

**FVG Features**:
- **Auto-detection**: Identifies gaps automatically
- **Visual highlighting**: Colored boxes marking FVG zones
- **Mitigation tracking**: Monitors when FVGs are filled

### 6. CISD (Change in State of Delivery)
**Purpose**: Track institutional order flow changes and delivery state modifications

**CISD Detection**:
- **Bullish CISD**: Institutional shift to buying delivery
- **Bearish CISD**: Institutional shift to selling delivery
- **Level Creation**: Automatic CISD level marking
- **Projection Lines**: Future price level projections

### 7. Position Sizing Calculator
**Purpose**: Calculate appropriate position sizes based on risk management

**Features**:
- **Account Balance**: Input total account size
- **Risk Percentage**: Set risk per trade (1-5% recommended)
- **Prop Firm Mode**: Specialized calculations for prop trading
- **Multi-Asset Support**: Forex, futures, stocks, crypto
- **Auto-Detection**: Identifies instrument type automatically

## ⚙️ Configuration Settings

### HTF Candle Settings

**Display Options**:
- **Show HTF**: Enable/disable HTF candles
- **Max Display**: Number of HTF candles (1-6)
- **HTF Mode**: Auto or Custom timeframe selection
- **Custom Timeframe**: Manual HTF selection

**Visual Styling**:
- **Bull/Bear Colors**: Customizable candle colors
- **Candle Width**: Adjustable width (1-4)
- **Spacing**: Gap between candles
- **Offset**: Distance from main chart

**Labels and Timer**:
- **HTF Label**: Show timeframe identifier
- **Timer Display**: Real-time countdown
- **Label Colors**: Customizable appearance
- **Text Sizes**: Tiny to Huge options

### Fractal Pattern Settings

**Pattern Detection**:
- **Show Fractal Patterns**: Enable/disable detection
- **Fractal Bias**: None, Bullish, or Bearish filter
- **Latest Only**: Show only most recent pattern
- **Extend to Current**: Extend pattern to current bar

**Visual Elements**:
- **Pattern Lines**: Customizable line styles
- **Transparency**: Adjustable opacity (0-100%)
- **Colors**: Bull/bear pattern colors
- **Labels**: Pattern identification text

### Sweep Detection Settings

**Sweep Types**:
- **Chart Sweeps**: Current timeframe sweeps
- **Fractal Sweeps**: Pattern-based sweeps
- **Latest Only**: Show only recent sweeps
- **Confirmation Lines**: Visual sweep confirmation

**Validation Options**:
- **Body Confirmation**: Use candle bodies
- **Wick Confirmation**: Use candle wicks
- **Confirmation Labels**: Text indicators
- **Line Styles**: Solid, dashed, dotted

### FVG and Imbalance Settings

**Fair Value Gaps**:
- **Show FVG**: Enable standard FVG detection
- **FVG Color**: Gap highlighting color
- **PFVG Detection**: First presented FVGs
- **Show All PFVGs**: Display multiple PFVGs

**Volume Imbalances**:
- **Show VI**: Enable volume imbalance detection
- **VI Color**: Imbalance zone color
- **Max Display**: Number of imbalances shown

### CISD and Projection Settings

**CISD Lines**:
- **Show CISD**: Enable CISD detection
- **CISD Color**: Line color customization
- **Line Width**: Thickness adjustment (1-5)
- **Show All**: Display all CISD levels

**Projections**:
- **Show Projections**: Enable projection lines
- **Projection Levels**: Custom level ratios
- **Extend Latest**: Extend to current bar
- **Label Size**: Projection text size

## 🔧 Advanced Features

### Auto HTF Detection Algorithm
```pine
htf_timeframe = current_tf <= 5m ? "1H" :
                current_tf <= 1H ? "4H" :
                current_tf <= 4H ? "1D" :
                current_tf <= 1D ? "1W" : "1M"
```

### Real-Time Timer Calculation
```pine
timeRemaining = (time_close(HTF) - timenow) / 1000
hours = floor(timeRemaining / 3600)
minutes = floor((timeRemaining % 3600) / 60)
seconds = floor(timeRemaining % 60)
```

### Fractal Pattern Recognition
**3-Point Fractal**:
- **Bullish**: Low[1] < Low[0] and Low[1] < Low[2]
- **Bearish**: High[1] > High[0] and High[1] > High[2]

**5-Point Fractal**:
- **Enhanced confirmation** with additional pivot points
- **Stronger signal reliability**
- **Reduced false positives**

### Sweep Detection Logic
**High Sweep**:
```pine
sweep_detected = high > previous_high and close < previous_high
```

**Low Sweep**:
```pine
sweep_detected = low < previous_low and close > previous_low
```

## 📈 Trading Applications

### 1. Multi-Timeframe Analysis
- **HTF Context**: Use HTF candles for directional bias
- **LTF Execution**: Enter trades on lower timeframes
- **Structure Alignment**: Ensure HTF and LTF structure agree

### 2. Institutional Flow Detection
- **Fractal Patterns**: Identify accumulation/distribution
- **Sweep Confirmation**: Validate institutional positioning
- **CISD Levels**: Track order flow changes

### 3. High-Probability Setups
- **Fractal + Sweep**: Pattern confirmed by liquidity sweep
- **FVG + Structure**: Imbalance at key structure level
- **CISD + HTF**: State change aligned with HTF bias

### 4. Risk Management
- **Position Sizing**: Automated calculation based on account
- **Structure Stops**: Place stops beyond key structure
- **FVG Targets**: Target unfilled fair value gaps

## 🎨 Visual Elements

### HTF Candles
- **Green Candles**: Bullish HTF candles (soft green #8ABF91)
- **Red Candles**: Bearish HTF candles (soft red #E08C89)
- **Timer Label**: Real-time countdown display
- **HTF Label**: Timeframe identifier

### Fractal Patterns
- **Pattern Boxes**: Colored rectangles marking patterns
- **Trend Lines**: Connecting fractal pivot points
- **Labels**: HH, HL, LH, LL structure markers
- **Sweep Lines**: Horizontal lines at sweep levels

### Fair Value Gaps
- **FVG Boxes**: Semi-transparent gap highlighting
- **PFVG Boxes**: Special color for first presented gaps
- **VI Zones**: Volume imbalance areas
- **Mitigation Tracking**: Visual confirmation when filled

### CISD and Projections
- **CISD Lines**: Horizontal levels at state change points
- **Projection Lines**: Future price level extensions
- **Level Labels**: Price and ratio information
- **Color Coding**: Bull/bear differentiation

## 💡 Best Practices

### Setup Recommendations
1. **Start with Auto HTF**: Let the indicator choose appropriate timeframes
2. **Enable Key Features**: HTF candles, fractals, sweeps, and CISD
3. **Customize Colors**: Adjust to match your chart theme
4. **Set Position Sizing**: Configure account balance and risk percentage

### Trading Workflow
1. **Analyze HTF Structure**: Check HTF candle direction and patterns
2. **Identify Fractals**: Look for institutional accumulation/distribution
3. **Confirm with Sweeps**: Validate patterns with liquidity sweeps
4. **Monitor CISD**: Watch for order flow state changes
5. **Execute on LTF**: Enter trades with precise timing

### Risk Management
1. **Use Position Calculator**: Size trades appropriately
2. **Respect Structure**: Don't trade against clear structure
3. **Target FVGs**: Aim for unfilled fair value gaps
4. **Monitor Timer**: Be aware of HTF candle close timing

## 🔍 Troubleshooting

### Common Issues

**HTF Candles Not Showing**:
- Check "Show HTF" setting is enabled
- Verify timeframe compatibility
- Ensure sufficient chart history

**Timer Not Updating**:
- Timer only works on real-time charts
- Historical charts show "(n/a)"
- Refresh chart if timer appears stuck

**Fractal Patterns Missing**:
- Enable "Show Fractal Patterns"
- Check fractal bias setting
- Ensure sufficient price history

**Position Size Incorrect**:
- Verify account balance setting
- Check risk percentage (1-5% recommended)
- Confirm instrument type detection

### Performance Optimization
- **Limit Max Display**: Reduce number of elements shown
- **Disable Unused Features**: Turn off unnecessary components
- **Optimize Timeframes**: Use appropriate HTF selection
- **Clear Old Elements**: Indicator auto-manages old objects

## 📊 Technical Specifications

**Pine Script Version**: v6  
**Max Bars Back**: 5000  
**Max Boxes**: 500  
**Max Lines**: 500  
**Max Labels**: 500  

**Supported Instruments**:
- Forex pairs
- Stock indices
- Individual stocks
- Cryptocurrency
- Futures contracts
- CFDs

**Timeframe Compatibility**:
- **Minimum**: 1 second
- **Maximum**: Monthly
- **Recommended**: 1m to Daily for optimal performance

## 🚀 Advanced Usage

### Custom Alert Integration
The indicator includes CustomAlertLib integration for automated notifications:
- **Fractal Pattern Alerts**: Notify on new pattern formation
- **Sweep Confirmation Alerts**: Alert on liquidity sweeps
- **CISD Change Alerts**: Notify on order flow state changes
- **Structure Break Alerts**: Alert on key level breaks

### Multi-Asset Analysis
Use the indicator across different asset classes:
- **Forex**: Currency pair correlation analysis
- **Indices**: Stock market structure tracking
- **Commodities**: Gold, oil, and agricultural products
- **Crypto**: Bitcoin and altcoin structure analysis

### Institutional Trading Integration
Combine with other institutional concepts:
- **Order Blocks**: Identify institutional order zones
- **Breaker Blocks**: Failed order block analysis
- **Mitigation Blocks**: Retest zone identification
- **Liquidity Pools**: High-probability reversal areas

This indicator provides a complete institutional trading framework, combining multiple proven concepts into a single, comprehensive tool for professional market analysis.