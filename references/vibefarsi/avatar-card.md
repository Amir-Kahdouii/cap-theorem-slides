# آواتار (avatar)
تصویر دایره‌ای کاربر که اگر تصویر نباشه، حرف اول اسم را با حلقه‌ی سفید نشان میده.
npm: none beyond react / tailwind
registry: none

## Prompt

Build a React + Tailwind CSS component named "Avatar" (avatar).

This item requires:
• If src is set, a circular image only, no fill or gradient.
• If there is no image, a white first letter, a white ring, and a transparent background.
• AvatarGroup overlaps with -ms-2 and a «+۱۲ نفر دیگر» trailer.

Persian / RTL rules for all output:
• RTL layout with dir="rtl". Use logical properties (ms/me/ps/pe/start/end), never left/right.
• Font from the project (IRANSans or Vazirmatn). Never apply letter-spacing on Persian text.
• Visible numbers use Persian digits (۰–۹), thousands separator «٬» (U+066C), and the unit «تومان» after the number.
• Colors only from theme tokens: bg-background, text-foreground, bg-primary, text-muted-foreground, border-border, and similar. Do not invent colors.
• Icons from lucide-react. Directional icons (arrows, chevrons) flip in RTL: "next" points left.
• Accessibility: correct ARIA roles, a visible focus ring, and full keyboard support.
• Form controls (input, textarea, select) must compute to at least 16px on iOS, or Safari zooms the page on focus; keep text-sm on desktop and raise it under @supports (-webkit-touch-callout: none).
• Motion is short (150–300ms) and disabled under prefers-reduced-motion.
• All visible UI copy (labels, placeholders, empty states, errors) is Persian (Farsi). Code identifiers stay English.

Output: avatar.tsx in TypeScript, no extra dependencies except lucide-react, plus a short usage example.

## Files

#### components/ui/avatar.tsx

```tsx
import * as React from "react";
import { cn, fa } from "@/lib/utils";

export interface AvatarProps {
  name: string;
  src?: string;
  size?: "sm" | "md" | "lg";
  className?: string;
}

const sizes = { sm: "size-7 text-[11px]", md: "size-9 text-sm", lg: "size-12 text-base" };

/** آواتار. Photo when `src` is set; otherwise a white initial in a white ring. */
export function Avatar({ name, src, size = "md", className }: AvatarProps) {
  const initial = name.trim().charAt(0);
  return (
    <span
      title={name}
      className={cn(
        "relative inline-flex shrink-0 items-center justify-center overflow-hidden rounded-full font-semibold",
        !src && "bg-transparent text-foreground ring-2 ring-foreground",
        sizes[size],
        className,
      )}
    >
      {/* eslint-disable-next-line @next/next/no-img-element -- avatars are tiny and often external */}
      {src ? <img src={src} alt={name} className="size-full rounded-full object-cover" /> : initial}
    </span>
  );
}

/** Overlapping avatars with a «+n» tail. */
export function AvatarGroup({ people, max = 4, size = "md", className }: { people: { name: string; src?: string }[]; max?: number; size?: AvatarProps["size"]; className?: string }) {
  const shown = people.slice(0, max);
  const rest = people.length - shown.length;
  return (
    <div className={cn("flex items-center", className)}>
      {shown.map((p, i) => (
        <Avatar key={p.name} {...p} size={size} className={cn("ring-2 ring-background", i > 0 && "-ms-2")} />
      ))}
      {rest > 0 && <span className="ms-2 text-xs text-muted-foreground">+{fa(rest)} نفر دیگر</span>}
    </div>
  );
}
```

---

# کارت (card)
کادر محتوا با سربرگ، عنوان و توضیح.
npm: none beyond react / tailwind
registry: none

## Prompt

Build a React + Tailwind CSS component named "Card" (card).

This item requires:
• 1px border from the border token, card background, radius from --radius; no heavy shadow.

Persian / RTL rules for all output:
• RTL layout with dir="rtl". Use logical properties (ms/me/ps/pe/start/end), never left/right.
• Font from the project (IRANSans or Vazirmatn). Never apply letter-spacing on Persian text.
• Visible numbers use Persian digits (۰–۹), thousands separator «٬» (U+066C), and the unit «تومان» after the number.
• Colors only from theme tokens: bg-background, text-foreground, bg-primary, text-muted-foreground, border-border, and similar. Do not invent colors.
• Icons from lucide-react. Directional icons (arrows, chevrons) flip in RTL: "next" points left.
• Accessibility: correct ARIA roles, a visible focus ring, and full keyboard support.
• Form controls (input, textarea, select) must compute to at least 16px on iOS, or Safari zooms the page on focus; keep text-sm on desktop and raise it under @supports (-webkit-touch-callout: none).
• Motion is short (150–300ms) and disabled under prefers-reduced-motion.
• All visible UI copy (labels, placeholders, empty states, errors) is Persian (Farsi). Code identifiers stay English.

Output: card.tsx in TypeScript, no extra dependencies except lucide-react, plus a short usage example.

## Files

#### components/ui/card.tsx

```tsx
import * as React from "react";
import { cn } from "@/lib/utils";

export function Card({ className, ...props }: React.HTMLAttributes<HTMLDivElement>) {
  return (
    <div
      className={cn(
        "relative isolate rounded-surface border-line border-border bg-card text-card-foreground shadow-surface [--tw-border-style:var(--line-style)]",
        // Glass systems blur what sits behind the card. The filter lives on a
        // pseudo-element so the card never traps fixed-position popovers.
        "before:pointer-events-none before:absolute before:inset-0 before:-z-10 before:rounded-[inherit] before:[backdrop-filter:var(--surface-filter)] before:content-['']",
        className,
      )}
      {...props}
    />
  );
}

export function CardHeader({ className, ...props }: React.HTMLAttributes<HTMLDivElement>) {
  return <div className={cn("flex flex-col gap-1 p-5", className)} {...props} />;
}

export function CardTitle({ className, ...props }: React.HTMLAttributes<HTMLHeadingElement>) {
  return <h3 className={cn("text-base font-semibold", className)} {...props} />;
}

export function CardDescription({ className, ...props }: React.HTMLAttributes<HTMLParagraphElement>) {
  return <p className={cn("text-sm text-muted-foreground", className)} {...props} />;
}

export function CardContent({ className, ...props }: React.HTMLAttributes<HTMLDivElement>) {
  return <div className={cn("p-5 pt-0", className)} {...props} />;
}
```