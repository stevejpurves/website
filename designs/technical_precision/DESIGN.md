---
name: Technical Precision
colors:
  surface: '#f9f9f9'
  surface-dim: '#dadada'
  surface-bright: '#f9f9f9'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f3f3f3'
  surface-container: '#eeeeee'
  surface-container-high: '#e8e8e8'
  surface-container-highest: '#e2e2e2'
  on-surface: '#1a1c1c'
  on-surface-variant: '#434657'
  inverse-surface: '#2f3131'
  inverse-on-surface: '#f1f1f1'
  outline: '#747689'
  outline-variant: '#c4c5da'
  surface-tint: '#0743ff'
  primary: '#0030c4'
  on-primary: '#ffffff'
  primary-container: '#0041ff'
  on-primary-container: '#cfd4ff'
  inverse-primary: '#bac3ff'
  secondary: '#5f5e5e'
  on-secondary: '#ffffff'
  secondary-container: '#e5e2e1'
  on-secondary-container: '#656464'
  tertiary: '#8a1800'
  on-tertiary: '#ffffff'
  tertiary-container: '#b52200'
  on-tertiary-container: '#ffcbbf'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#dee0ff'
  primary-fixed-dim: '#bac3ff'
  on-primary-fixed: '#00115a'
  on-primary-fixed-variant: '#0031c6'
  secondary-fixed: '#e5e2e1'
  secondary-fixed-dim: '#c8c6c5'
  on-secondary-fixed: '#1c1b1b'
  on-secondary-fixed-variant: '#474646'
  tertiary-fixed: '#ffdad3'
  tertiary-fixed-dim: '#ffb4a4'
  on-tertiary-fixed: '#3d0600'
  on-tertiary-fixed-variant: '#8c1800'
  background: '#f9f9f9'
  on-background: '#1a1c1c'
  surface-variant: '#e2e2e2'
typography:
  h1:
    fontFamily: Space Grotesk
    fontSize: 72px
    fontWeight: '700'
    lineHeight: '1.1'
    letterSpacing: -0.04em
  h2:
    fontFamily: Space Grotesk
    fontSize: 48px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  h3:
    fontFamily: Space Grotesk
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.01em
  body-lg:
    fontFamily: Space Grotesk
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.6'
    letterSpacing: 0em
  body-md:
    fontFamily: Space Grotesk
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.6'
    letterSpacing: 0em
  label-caps:
    fontFamily: Space Grotesk
    fontSize: 12px
    fontWeight: '700'
    lineHeight: '1.2'
    letterSpacing: 0.1em
  mono-data:
    fontFamily: Space Grotesk
    fontSize: 14px
    fontWeight: '500'
    lineHeight: '1.4'
    letterSpacing: 0em
spacing:
  unit: 4px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 32px
  xl: 64px
  container-max: 1440px
  gutter: 24px
---

## Brand & Style

This design system is engineered for a technical consultancy where precision, clarity, and authority are paramount. The brand personality is clinical, high-performance, and uncompromisingly professional. 

The aesthetic leverages **Minimalism** with a **Brutalist** edge—relying on stark white space, rigid structural alignment, and intentional lack of decoration to convey expertise. It avoids unnecessary flourishes, focusing instead on information density and typographic hierarchy to evoke an emotional response of absolute reliability and forward-thinking engineering.

## Colors

The palette is restricted to three core pillars to ensure maximum visual impact and clarity:
- **Base:** Absolute white (#FFFFFF) provides a clean, clinical laboratory feel.
- **Typography:** Stark blacks and dark charcoals ensure high legibility and a sense of permanence.
- **Accent:** Electric Blue (#0041FF) is used surgically to denote interaction, progress, and technical sophistication.

Use the primary accent sparingly; it should act as a high-frequency signal against a quiet, monochrome background.

## Typography

This design system exclusively uses **Space Grotesk** to maintain a cohesive, technical character. The typeface's geometric quirks reflect engineering precision. 

- **Headlines:** Set with tight letter-spacing and heavy weights to create "blocks" of text.
- **Data Display:** Use the medium weight for tabular data and technical specifications.
- **Labels:** Small-caps are used for metadata, category labels, and overlines to provide contrast without increasing font size.
- **Hierarchy:** Rely on scale and weight rather than color shifts to distinguish information levels.

## Layout & Spacing

The layout follows a **Fixed Grid** philosophy based on a 12-column system. 
- **Rhythm:** A 4px baseline grid governs all vertical movement. 
- **Margins:** Generous outer margins (64px+) are encouraged to frame content and emphasize the "white space as a luxury" concept.
- **Density:** While the outer layout is spacious, internal component spacing (padding) should be tight and efficient, reflecting the density of technical documentation.

## Elevation & Depth

To maintain a stark and professional aesthetic, this design system rejects traditional shadows. Depth is communicated through **Bold Borders** and **Tonal Layers**.

- **Surfaces:** Use 1px solid borders (#000000 or #E5E5E5) to define containers.
- **Interaction:** State changes (hover/active) are indicated by filling a bordered shape with a solid color (Electric Blue or Black), rather than lifting it with a shadow.
- **Layering:** Use a light grey (#F5F5F5) background to distinguish "well" areas or secondary sidebar regions from the primary white canvas.

## Shapes

The shape language is strictly **Sharp (0px)**. 

Every element—buttons, input fields, cards, and images—must have 90-degree corners. This reinforces the "engineered" and "structural" narrative of the consultancy. Circles are permitted only for specific functional icons or status indicators, but all containing boxes must remain rectangular.

## Components

- **Buttons:** Sharp corners, 1px black border, 16px horizontal padding. Primary buttons use a solid Electric Blue fill with white text. Secondary buttons use white fill with black text and a black border.
- **Inputs:** 1px solid borders. On focus, the border weight increases to 2px or changes to Electric Blue. No rounded corners. Labels are placed above the input in `label-caps`.
- **Cards:** Defined by a 1px #E5E5E5 border. No shadows. Header sections within cards should be separated by a 1px horizontal rule.
- **Chips/Tags:** Rectangular boxes with `label-caps` typography. Use a light grey background or a thin border.
- **Data Grids:** High-density tables with 1px horizontal dividers. No vertical dividers. Header rows should be set in bold with a subtle grey background.
- **Technical Diagrams:** Use Electric Blue for the "active path" or key data points within charts and schematics, keeping all other lines in shades of grey.