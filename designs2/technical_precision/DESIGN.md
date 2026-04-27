---
name: Technical Precision
colors:
  surface: '#fbf8ff'
  surface-dim: '#dad9e3'
  surface-bright: '#fbf8ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f4f2fd'
  surface-container: '#eeedf7'
  surface-container-high: '#e8e7f1'
  surface-container-highest: '#e3e1ec'
  on-surface: '#1a1b22'
  on-surface-variant: '#3b4b37'
  inverse-surface: '#2f3038'
  inverse-on-surface: '#f1effa'
  outline: '#6b7c65'
  outline-variant: '#b9ccb2'
  surface-tint: '#006e16'
  primary: '#006e16'
  on-primary: '#ffffff'
  primary-container: '#00ff41'
  on-primary-container: '#007117'
  inverse-primary: '#00e639'
  secondary: '#5e5e5e'
  on-secondary: '#ffffff'
  secondary-container: '#e2e2e2'
  on-secondary-container: '#646464'
  tertiary: '#775839'
  on-tertiary: '#ffffff'
  tertiary-container: '#ffd5ae'
  on-tertiary-container: '#7a5b3c'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#72ff70'
  primary-fixed-dim: '#00e639'
  on-primary-fixed: '#002203'
  on-primary-fixed-variant: '#00530e'
  secondary-fixed: '#e2e2e2'
  secondary-fixed-dim: '#c6c6c6'
  on-secondary-fixed: '#1b1b1b'
  on-secondary-fixed-variant: '#474747'
  tertiary-fixed: '#ffdcbd'
  tertiary-fixed-dim: '#e7bf99'
  on-tertiary-fixed: '#2c1701'
  on-tertiary-fixed-variant: '#5d4124'
  background: '#fbf8ff'
  on-background: '#1a1b22'
  surface-variant: '#e3e1ec'
typography:
  headline-lg:
    fontFamily: Space Grotesk
    fontSize: 48px
    fontWeight: '700'
    lineHeight: '1.1'
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Space Grotesk
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.01em
  headline-sm:
    fontFamily: Space Grotesk
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.3'
    letterSpacing: '0'
  body-lg:
    fontFamily: Space Grotesk
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.6'
    letterSpacing: '0'
  body-md:
    fontFamily: Space Grotesk
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.5'
    letterSpacing: '0'
  label-caps:
    fontFamily: Space Grotesk
    fontSize: 12px
    fontWeight: '700'
    lineHeight: '1'
    letterSpacing: 0.1em
  mono-data:
    fontFamily: Space Grotesk
    fontSize: 14px
    fontWeight: '500'
    lineHeight: '1.4'
    letterSpacing: -0.01em
spacing:
  unit: 4px
  gutter: 24px
  margin: 48px
  container-max: 1440px
---

## Brand & Style
The brand personality is engineered, authoritative, and unapologetically technical. It is designed for high-stakes engineering environments where clarity is a prerequisite for performance. The aesthetic draws from **Swiss Minimalism** and **Technical Manuals**, prioritizing structural integrity over decorative flair. 

The emotional response should be one of absolute reliability and "no-nonsense" efficiency. By utilizing a stark white canvas and a high-visibility accent, the design system creates a focused workspace that mimics a precision instrument or a high-end CAD interface.

## Colors
The palette is hyper-limited to maximize contrast and functional signaling. 
- **Base:** Pure White (#FFFFFF) serves as the universal background to eliminate visual noise.
- **Ink:** Pure Black (#000000) for all typography and structural borders, ensuring maximum legibility.
- **Accent:** Neon Green (#00FF41) is used exclusively for interactive states, progress indicators, and critical data points. 
- **Muted:** A technical Mid-Gray (#71717A) is reserved for non-essential metadata and disabled states to prevent them from competing with the core layout.

## Typography
Space Grotesk is the sole typeface, utilized for its geometric rigor and technical "quirks" that evoke engineering terminals. 
- **Headlines:** Set with tight tracking and heavy weights to create "blocks" of text.
- **Body:** Generous line-height is maintained to ensure readability against the high-contrast background.
- **Labels:** Small-scale uppercase labels are used for technical metadata, providing a distinct visual contrast to narrative text.
- **Emphasis:** Only weight changes (Medium/Bold) are used for emphasis; italics are avoided to maintain a rigid, upright architectural feel.

## Layout & Spacing
The layout follows a **Fixed 12-Column Grid** system with a focus on mathematical alignment. 
- **Rhythm:** All margins and paddings must be multiples of 4px.
- **Borders:** A 1px solid black border is the primary tool for containment and separation.
- **Whitespace:** Large, purposeful gaps of white space are used to group information, rather than using background color shifts. 
- **Density:** High Information Density is encouraged. Elements should feel tightly packed within their respective modules, separated by clear, rigid gutters.

## Elevation & Depth
Elevation is expressed through **structural layering and borders** rather than shadows. 
- **Flat Depth:** No ambient shadows or blurs are permitted.
- **Stacking:** Depth is communicated by 1px borders. If a modal or dropdown appears, it is given a 1px black border and a high-contrast offset (a "hard shadow" look created by a 2px black solid stroke offset to the bottom right).
- **Active State:** When an element is focused or active, the border weight may increase to 2px or change color to the accent Neon Green, but it never "lifts" off the page using traditional Z-axis metaphors.

## Shapes
This design system utilizes a **0px radius (Sharp)** for all elements. There are no rounded corners. Buttons, input fields, cards, and containers are all strictly rectangular. This reinforces the architectural and "blueprinted" nature of the interface. Circles are reserved exclusively for status indicators (e.g., "online" pips) to make them immediately distinct from structural UI elements.

## Components
- **Buttons:** Sharp 1px black borders. Primary buttons use a black background with white text. On hover, the background flips to the Neon Green accent with black text.
- **Input Fields:** 1px black bottom border only (minimalist "underline" style). On focus, the border becomes 2px Neon Green. Labels are always positioned above in `label-caps`.
- **Chips/Tags:** Rectangular boxes with 1px black borders. Active tags use the Neon Green background to draw immediate attention.
- **Cards:** Simple containers defined by a 1px black border. No padding on the container itself if it houses a sub-grid of data.
- **Lists:** Rows separated by 1px black horizontal rules. Hovering over a list item triggers a 4px Neon Green vertical "indicator" on the far left of the row.
- **Checkboxes:** Square, 0px radius. Checked state is a solid Neon Green fill with a black "X" or checkmark.
- **Data Tables:** High-density grids with 1px borders between all cells, resembling a technical ledger or spreadsheet.