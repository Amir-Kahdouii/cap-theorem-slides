# کاغذ (paper)
کاغذ روشن و مرکب تیره با تیترهای نسخ، خط‌های نازک و فیلدهای زیرخط‌دار. هیچ سایه‌ای نداره و برای خواندن طولانی ساخته شده.
npm: none beyond react / tailwind
registry: none

## Prompt

Apply the "Paper" (paper) design system to my project.

Rules:
• Language: editorial / print. Typography does the work; boxes are barely there.
• Light theme: warm paper background, ink-dark text and primary button, vermilion brand accent, color-scheme: light. Cards share the page color and are separated by hairline rules (ink 14%).
• Headings in Noto Naskh Arabic 700; body stays sans. 2px radius on controls and cards.
• Text fields have only a bottom border (border-width 0 0 1px) on a transparent background.
• No drop shadows at all, except a faint one under floating overlays. Press = translateY(1px). Motion 160ms.
• A design system is a design language, not a palette. Components read color AND shape (--shape-control/field/surface/overlay), border width (--line, --line-field), shadows (--depth-*), press transform (--press), motion (--motion, --motion-ease), fonts (--type-display, --type-body) and density (--spacing) from these tokens.
• No hardcoded hex, radius, shadow, border width or duration inside components. Use the mapped utilities: rounded-control, rounded-field, rounded-surface, border-line, shadow-control, shadow-surface, active:shadow-press, active:[transform:var(--press)], duration-(--motion) ease-motion, font-display.

## Files

#### app/globals.css

```css
/* کاغذ، مجله‌ای. تیترها با Noto Naskh Arabic هستن. */
[data-theme="paper"] {
  color-scheme: light;

  /* رنگ */
  --background: oklch(0.985 0.004 85);
  --foreground: oklch(0.2 0.01 60);
  --card: oklch(0.985 0.004 85);
  --card-foreground: oklch(0.2 0.01 60);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.2 0.01 60);
  --primary: oklch(0.2 0.01 60);
  --primary-foreground: oklch(0.985 0.004 85);
  --secondary: oklch(0.94 0.008 85);
  --secondary-foreground: oklch(0.2 0.01 60);
  --muted: oklch(0.955 0.006 85);
  --muted-foreground: oklch(0.47 0.015 60);
  --accent: oklch(0.94 0.008 85);
  --accent-foreground: oklch(0.2 0.01 60);
  --destructive: oklch(0.55 0.2 25);
  --success: oklch(0.52 0.13 160);
  --warning: oklch(0.62 0.14 70);
  --border: oklch(0.2 0.01 60 / 14%);
  --input: oklch(0.2 0.01 60 / 30%);
  --ring: oklch(0.5 0.02 60);
  --brand: oklch(0.55 0.19 30);
  --brand-foreground: oklch(0.985 0 0);

  /* زبان طراحی: فونت، فرم، خط، عمق، حرکت و تراکم */
  --radius: 0.25rem;
  --type-display: "Noto Naskh Arabic", "IRANSans", "Vazirmatn", serif;
  --type-display-weight: 700;
  --shape-control: 0.125rem;
  --shape-field: 0rem;
  --shape-surface: 0.125rem;
  --shape-overlay: 0.25rem;
  --line: 1px;
  --line-field: 0 0 1px 0;
  --line-style: solid;
  --field: transparent;
  --depth-control: 0 0 #0000;
  --depth-press: 0 0 #0000;
  --depth-field: 0 0 #0000;
  --depth-surface: 0 0 #0000;
  --depth-overlay: 0 12px 32px -16px oklch(0.2 0.01 60 / 25%);
  --surface-filter: none;
  --press: translateY(1px);
  --motion: 160ms;
  --motion-ease: cubic-bezier(0.25, 0.1, 0.25, 1);
  --backdrop: none;
  --spacing: 0.26rem;
}
```

## Other themes

- گرافیت / Graphite (`graphite`) — سیاه خنثی با خط‌های مویی، دکمه‌ی سفید و یک رنگ تأکیدی کهربایی. آرام و دقیقه و تم پیش‌فرض سایته.
- فیروزه / Turquoise (`turquoise`) — سطح‌های نیمه‌شفاف و مات روی یک پس‌زمینه‌ی نورانی فیروزه‌ای. کارت‌ها پشتشون را محو نشون میدن و لبه‌هاشون برق می‌زنه.
- زعفران / Saffron (`saffron`) — زمینه‌ی کرم و دکمه‌ی زعفرانی با خط‌های مشکی ضخیم، گوشه‌های تیز و سایه‌ی سخت. دکمه‌ها موقع کلیک واقعاً پایین می‌رن.
- انار / Pomegranate (`pomegranate`) — صورتی ملایم با دکمه‌های کپسولی و سایه‌های پف‌دار چندلایه. حرکت‌ها فنری هستن و کمی از جاشون رد میشن.
- لاجورد / Lapis (`lapis`) — نیلی تیره با خط‌چین، گوشه‌های تقریباً تیز و فاصله‌های فشرده. حرکت‌ها پله‌ای و فوری هستن و رنگ تأکیدش سبز فسفریه.
- کاغذ / Paper (`paper`) — کاغذ روشن و مرکب تیره با تیترهای نسخ، خط‌های نازک و فیلدهای زیرخط‌دار. هیچ سایه‌ای نداره و برای خواندن طولانی ساخته شده.

Paste the CSS into :root (or replace the current block). Map tokens in @theme inline as on https://vibefarsi.ir/docs.