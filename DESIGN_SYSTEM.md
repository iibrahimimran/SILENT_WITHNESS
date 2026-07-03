# Silent Witness Design System

This document outlines the comprehensive design system for the Silent Witness frontend, built according to the `DESIGN.md` specification (Auros — Abyssal Terminal aesthetic).

## Overview

The design system provides a complete foundation for building the Silent Witness interface with consistency, accessibility, and premium aesthetics. All components, utilities, and tokens follow the Auros design language: a dark teal abyssal terminal with bioluminescent accents.

## Architecture

### Design Tokens

All design tokens are centralized and follow the DESIGN.md specification:

- **Colors**: Liquid Teal Stack (Abyss, Deep, Kelp) + Neutrals (Platinum, Silver Mist, Ash) + Accents (Lavender Phosphor)
- **Typography**: Matter (primary display face, weights 400 & 500) + Arial (fallback)
- **Spacing**: 4px base unit with scale from 12px to 164px
- **Border Radius**: 6px (small), 16px (cards)
- **Layout**: 1440px max-width, 68px section gap, 20px element gap

### File Structure

```
client/src/
├── components/design-system/
│   ├── GradientPillButton.tsx      # Primary CTA button
│   ├── GhostNavigationLink.tsx     # Navigation links
│   ├── SurfaceCard.tsx            # Content container
│   ├── RecessedCard.tsx           # Deep panel
│   ├── FeatureCard.tsx            # Service listing
│   ├── Typography.tsx             # Heading, Paragraph, SectionLabel, StatisticCounter
│   ├── GlassPanel.tsx             # Frosted glass effect
│   ├── AnimatedContainer.tsx      # Framer Motion wrapper
│   ├── ParticleSphere.tsx         # 3D particle animation
│   ├── ArrowIcon.tsx              # Diagonal arrow icon
│   └── index.ts                   # Barrel export
├── lib/
│   ├── motion-tokens.ts           # Animation utilities
│   ├── layout-utils.ts            # Spacing & breakpoints
│   ├── color-tokens.ts            # Color palette
│   └── accessibility-utils.ts     # WCAG compliance
├── hooks/
│   └── useResponsive.ts           # Responsive design hooks
└── styles/
    └── index.css                  # Global CSS & Tailwind config
```

## Component Library

### Buttons

#### GradientPillButton
Primary CTA with aurora gradient (cyan → white → pink).

```tsx
import { GradientPillButton } from '@/components/design-system';

<GradientPillButton>Analyze Text</GradientPillButton>
```

**Props:**
- `variant`: 'default' | 'ghost' | 'outline'
- `size`: 'default' | 'sm' | 'lg'

### Cards

#### SurfaceCard
Content container with Liquid Kelp background.

```tsx
import { SurfaceCard } from '@/components/design-system';

<SurfaceCard>
  <h3>Feature Title</h3>
  <p>Feature description</p>
</SurfaceCard>
```

**Props:**
- `padding`: 'default' | 'sm' | 'lg' | 'none'

#### RecessedCard
Deep panel for footer-adjacent content.

```tsx
import { RecessedCard } from '@/components/design-system';

<RecessedCard>
  <p>Deep content</p>
</RecessedCard>
```

#### FeatureCard
Service listing with arrow icon button.

```tsx
import { FeatureCard } from '@/components/design-system';

<FeatureCard
  title="Service Name"
  description="Service description"
  onArrowClick={() => {}}
/>
```

#### GlassPanel
Frosted glass effect with backdrop blur.

```tsx
import { GlassPanel } from '@/components/design-system';

<GlassPanel variant="default">
  <p>Glass panel content</p>
</GlassPanel>
```

### Typography

#### Heading
Semantic heading component with size variants.

```tsx
import { Heading } from '@/components/design-system';

<Heading as="h1" size="h1">Large Display</Heading>
<Heading as="h2" size="h2">Section Heading</Heading>
```

**Sizes:** 'h1' | 'h1-lg' | 'h2' | 'h3'

#### Paragraph
Body text with semantic color.

```tsx
import { Paragraph } from '@/components/design-system';

<Paragraph size="body">Body text</Paragraph>
<Paragraph size="caption">Caption text</Paragraph>
```

#### SectionLabel
Uppercase eyebrow/kicker text.

```tsx
import { SectionLabel } from '@/components/design-system';

<SectionLabel size="md" color="mist">SECTION</SectionLabel>
```

#### StatisticCounter
Large number with label (for metrics display).

```tsx
import { StatisticCounter } from '@/components/design-system';

<StatisticCounter value="$18.21B" label="Total Value" />
```

### Navigation

#### GhostNavigationLink
Transparent nav link with active state.

```tsx
import { GhostNavigationLink } from '@/components/design-system';

<GhostNavigationLink href="/explore" isActive={true}>
  Explore
</GhostNavigationLink>
```

## Animation System

### Motion Tokens

All animations follow the Auros motion philosophy: subtle, purposeful, and data-driven.

```tsx
import { motionVariants, duration, easing } from '@/lib/motion-tokens';

// Available variants:
// fadeIn, scaleIn, slideUp, slideDown, slideLeft, slideRight
// staggerContainer, staggerItem, glow, rotate, buttonHover, cardHover
```

### Animated Components

#### AnimatedContainer
Flexible wrapper for any animation.

```tsx
import { AnimatedContainer, FadeIn, SlideUp } from '@/components/design-system';

<FadeIn>Content fades in</FadeIn>
<SlideUp>Content slides up</SlideUp>
```

#### StaggerContainer + StaggerItem
Cascading animations for lists.

```tsx
import { StaggerContainer, StaggerItem } from '@/components/design-system';

<StaggerContainer>
  {items.map((item) => (
    <StaggerItem key={item.id}>{item.name}</StaggerItem>
  ))}
</StaggerContainer>
```

#### ParticleSphere
3D rotating particle animation for hero section.

```tsx
import { ParticleSphere } from '@/components/design-system';

<ParticleSphere size={400} speed={0.5} />
```

## Responsive Design

### Breakpoints

- `xs`: 320px (mobile)
- `sm`: 640px (mobile landscape)
- `md`: 768px (tablet)
- `lg`: 1024px (desktop)
- `xl`: 1280px (large desktop)
- `2xl`: 1440px (max content width)

### Responsive Hooks

```tsx
import {
  useBreakpoint,
  useIsBreakpoint,
  useViewportSize,
  useIsMobile,
  useIsTablet,
  useIsDesktop,
  useResponsiveValue,
} from '@/hooks/useResponsive';

// Get current breakpoint
const breakpoint = useBreakpoint(); // 'md' | 'lg' | etc.

// Check if at least a certain breakpoint
const isDesktop = useIsBreakpoint('lg');

// Get responsive value
const padding = useResponsiveValue(
  { xs: '1rem', md: '2rem', lg: '3rem' },
  '1rem'
);
```

## Color System

### Color Tokens

```tsx
import { colors, gradients, colorRoles } from '@/lib/color-tokens';

// Direct colors
colors.liquidAbyss      // #012624
colors.liquidKelp       // #003734
colors.lavenderPhosphor // #fde9ff

// Gradients
gradients.aurora        // Cyan → White → Pink
gradients.bioluminescent // Teal → Cyan

// Semantic roles
colorRoles.background.primary    // liquidAbyss
colorRoles.text.primary          // platinum
colorRoles.emphasis.accent       // lavenderPhosphor
```

### Color Utilities

```tsx
import { getContrastTextColor, meetsWCAGAA } from '@/lib/color-tokens';

// Get accessible text color
const textColor = getContrastTextColor('#012624'); // Returns white

// Check WCAG compliance
const isAccessible = meetsWCAGAA('#ffffff', '#012624', false); // true
```

## Accessibility

### Keyboard Navigation

All interactive components support keyboard navigation:
- `Tab` / `Shift+Tab`: Navigate between focusable elements
- `Enter` / `Space`: Activate buttons
- `Escape`: Close modals/popovers
- `Arrow Keys`: Navigate lists/menus

### Screen Reader Support

```tsx
import { announce, createLiveRegion } from '@/lib/accessibility-utils';

// Announce to screen readers
announce('Analysis complete', 'polite');

// Create live region for dynamic updates
createLiveRegion('New message received', 'assertive');
```

### Motion Preferences

```tsx
import { usePrefersReducedMotion } from '@/hooks/useResponsive';

const prefersReduced = usePrefersReducedMotion();

// Animations automatically respect prefers-reduced-motion
```

## Layout Utilities

### Spacing Scale

```tsx
import { spacing, sectionGap, elementGap, gaps } from '@/lib/layout-utils';

// Use in className
className="p-spacing-16 gap-element-gap"

// Or reference directly
const padding = spacing['36']; // '36px'
```

### Grid Patterns

```tsx
import { gridColumns } from '@/lib/layout-utils';

// Two-column asymmetric layout
className={`grid gap-section-gap`}
style={{ gridTemplateColumns: gridColumns.twoAsymmetric }}
```

## Tailwind Integration

### Custom Utilities

All design tokens are available as Tailwind utilities:

```tsx
// Colors
className="bg-liquidAbyss text-platinum border-slateDeep"

// Typography
className="font-matter text-heading leading-heading tracking-heading-lg"

// Spacing
className="p-spacing-36 gap-element-gap"

// Border Radius
className="rounded-radius-2xl"

// Gradients
className="bg-gradient-aurora"
```

## Best Practices

### Component Usage

1. **Always use design system components** instead of creating custom ones
2. **Respect the color palette** — never introduce colors outside DESIGN.md
3. **Use semantic typography** — Heading, Paragraph, SectionLabel for correct styling
4. **Leverage motion tokens** — Use predefined animations for consistency

### Responsive Design

1. **Mobile-first approach** — Start with mobile styles, enhance for larger screens
2. **Use responsive hooks** — Avoid hardcoding breakpoints
3. **Test on real devices** — Use useViewportSize to verify layouts

### Accessibility

1. **Always include alt text** for images
2. **Use semantic HTML** — Use proper heading hierarchy
3. **Ensure color contrast** — Use meetsWCAGAA to verify
4. **Support keyboard navigation** — Test with Tab key

### Performance

1. **Lazy load animations** — Use AnimatedContainer only when needed
2. **Optimize images** — Use Next.js Image component
3. **Code split components** — Import only what you need

## Future Extensions

- Support for light mode variant
- Additional animation presets
- Theme customization API
- Component composition patterns
- Design tokens export for external tools

## References

- **DESIGN.md**: Authoritative visual design specification
- **Tailwind CSS**: Utility-first CSS framework
- **Framer Motion**: Animation library
- **React Three Fiber**: 3D graphics (for ParticleSphere)
- **WCAG 2.1**: Web Content Accessibility Guidelines
