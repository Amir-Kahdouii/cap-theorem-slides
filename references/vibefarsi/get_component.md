# دکمه (button)
دکمه در چند واریانت و اندازه، با حالت غیرفعال و آیکونی که در جهت درست کنار متن می‌نشینه.
npm: lucide-react
registry: none

## Prompt

Build a React + Tailwind CSS component named "Button" (button).

This item requires:
• Variants default, secondary, outline, ghost, destructive and sizes sm/md/lg/icon.
• Icons sized with [&_svg]:size-4 and gap-2 from the label.
• Disabled: opacity-50 and pointer-events-none; active: scale-[0.98].

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

Output: button.tsx in TypeScript, no extra dependencies except lucide-react, plus a short usage example.

## Files

#### components/ui/button.tsx

```tsx
import * as React from "react";
import { cn } from "@/lib/utils";

type Variant = "default" | "secondary" | "outline" | "ghost" | "brand" | "destructive";
type Size = "sm" | "md" | "lg" | "icon";

const variants: Record<Variant, string> = {
  default: "bg-primary text-primary-foreground hover:bg-primary/90 shadow-control active:shadow-press",
  secondary: "bg-secondary text-secondary-foreground hover:bg-secondary/80 border-line border-border shadow-control active:shadow-press",
  outline: "border-line border-input bg-transparent hover:bg-accent hover:text-accent-foreground shadow-control active:shadow-press",
  ghost: "hover:bg-accent hover:text-accent-foreground",
  brand: "bg-brand text-brand-foreground hover:bg-brand/90 shadow-control active:shadow-press",
  destructive: "bg-destructive text-white hover:bg-destructive/90 shadow-control active:shadow-press",
};

const sizes: Record<Size, string> = {
  sm: "h-8 px-3 text-[13px] gap-1.5",
  md: "h-10 px-4 text-sm gap-2",
  lg: "h-12 px-6 text-base gap-2.5",
  icon: "size-10",
};

export interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: Variant;
  size?: Size;
  asChild?: boolean;
}

export function Button({ className, variant = "default", size = "md", type = "button", ...props }: ButtonProps) {
  return (
    <button
      type={type}
      className={cn(
        // Shape, depth, press and motion come from the design-system tokens.
        "inline-flex items-center justify-center whitespace-nowrap rounded-control font-semibold transition-all duration-(--motion) ease-motion",
        "focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 focus-visible:ring-offset-background",
        "disabled:pointer-events-none disabled:opacity-50 active:[transform:var(--press)]",
        "[&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
        variants[variant],
        sizes[size],
        className,
      )}
      {...props}
    />
  );
}
```

---

# نشان (badge)
برچسب وضعیت با متن رنگی، بدون پس‌زمینه و آیکون.
npm: none beyond react / tailwind
registry: none

## Prompt

Build a React + Tailwind CSS component named "Badge" (badge).

This item requires:
• Text only, no background and no icon; text-xs and font-medium.
• Color from the variant token: success, warning, brand, destructive.

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

Output: badge.tsx in TypeScript, no extra dependencies except lucide-react, plus a short usage example.

## Files

#### components/ui/badge.tsx

```tsx
import * as React from "react";
import { cn } from "@/lib/utils";

type Variant = "default" | "secondary" | "outline" | "success" | "warning" | "brand" | "destructive";

const variants: Record<Variant, string> = {
  default: "text-foreground",
  secondary: "text-muted-foreground",
  outline: "text-foreground/55",
  success: "text-success",
  warning: "text-warning",
  brand: "text-brand",
  destructive: "text-destructive",
};

export function Badge({
  className,
  variant = "default",
  ...props
}: React.HTMLAttributes<HTMLSpanElement> & { variant?: Variant }) {
  return (
    <span
      className={cn(
        "inline-flex items-center text-xs font-medium leading-6 whitespace-nowrap",
        variants[variant],
        className,
      )}
      {...props}
    />
  );
}
```

---

# تب‌ها (tabs)
تب‌های بخش‌بندی‌شده یا خطی که با کیبورد کار می‌کنن و جهت راست‌چین را رعایت می‌کنن. در حالت segmented یک قرص زیر تب فعال سر می‌خوره.
npm: none beyond react / tailwind
registry: none

## Prompt

Build a React + Tailwind CSS component named "Tabs" (tabs).

This item requires:
• role="tablist"/"tab"/"tabpanel" with aria-controls; only the active tab is tabIndex=0.
• In RTL ArrowLeft moves to the next tab (to the left).
• segmented: measure the active tab's offsetLeft/offsetWidth and slide an absolute bg-background pill with translateX; re-measure on ResizeObserver.

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

Output: tabs.tsx in TypeScript, no extra dependencies except lucide-react, plus a short usage example.

## Files

#### components/ui/tabs.tsx

```tsx
"use client";

import * as React from "react";
import { cn } from "@/lib/utils";

type Ctx = {
  value: string;
  setValue: (v: string) => void;
  variant: "segmented" | "underline";
  id: string;
};
const TabsCtx = React.createContext<Ctx | null>(null);

export interface TabsProps {
  value?: string;
  defaultValue: string;
  onValueChange?: (value: string) => void;
  variant?: "segmented" | "underline";
  className?: string;
  children: React.ReactNode;
}

/** تب‌ها. In RTL the first tab is on the right; ArrowLeft moves to the next tab. */
export function Tabs({ value, defaultValue, onValueChange, variant = "segmented", className, children }: TabsProps) {
  const [internal, setInternal] = React.useState(defaultValue);
  const id = React.useId();
  const v = value ?? internal;
  const setValue = (next: string) => {
    if (value === undefined) setInternal(next);
    onValueChange?.(next);
  };
  return (
    <TabsCtx.Provider value={{ value: v, setValue, variant, id }}>
      <div className={className}>{children}</div>
    </TabsCtx.Provider>
  );
}

export function TabsList({
  className,
  children,
  "aria-label": label,
}: {
  className?: string;
  children: React.ReactNode;
  "aria-label"?: string;
}) {
  const ctx = React.useContext(TabsCtx)!;
  const list = React.useRef<HTMLDivElement>(null);
  const [pill, setPill] = React.useState<{ x: number; w: number } | null>(null);

  const measure = React.useCallback(() => {
    if (ctx.variant !== "segmented") {
      setPill(null);
      return;
    }
    const root = list.current;
    const el = root?.querySelector<HTMLElement>('[aria-selected="true"]');
    if (!root || !el) return setPill(null);
    setPill({ x: el.offsetLeft, w: el.offsetWidth });
  }, [ctx.variant, ctx.value]);

  React.useLayoutEffect(measure, [measure, children]);
  React.useEffect(() => {
    const root = list.current;
    if (!root || typeof ResizeObserver === "undefined") return;
    const ro = new ResizeObserver(measure);
    ro.observe(root);
    return () => ro.disconnect();
  }, [measure]);

  return (
    <div
      ref={list}
      role="tablist"
      aria-label={label}
      onKeyDown={(e) => {
        const tabs = Array.from(e.currentTarget.querySelectorAll<HTMLElement>("[role=tab]"));
        const i = tabs.indexOf(document.activeElement as HTMLElement);
        const dir = e.key === "ArrowLeft" ? 1 : e.key === "ArrowRight" ? -1 : 0;
        if (!dir || i < 0) return;
        e.preventDefault();
        const next = tabs[(i + dir + tabs.length) % tabs.length];
        next.focus();
        next.click();
      }}
      className={cn(
        "relative isolate",
        ctx.variant === "segmented"
          ? "inline-flex rounded-[calc(var(--shape-control)+2px)] border-line border-border bg-muted p-0.5"
          : "flex gap-1 border-b border-border",
        className,
      )}
    >
      {ctx.variant === "segmented" && pill ? (
        <span
          aria-hidden
          className="absolute inset-y-0.5 -z-10 rounded-control bg-background shadow-sm ring-1 ring-border transition-[transform,width] duration-(--motion) ease-motion"
          style={{ width: pill.w, left: 0, transform: `translateX(${pill.x}px)` }}
        />
      ) : null}
      {children}
    </div>
  );
}

export function TabsTrigger({
  value,
  className,
  children,
}: {
  value: string;
  className?: string;
  children: React.ReactNode;
}) {
  const ctx = React.useContext(TabsCtx)!;
  const active = ctx.value === value;
  return (
    <button
      type="button"
      role="tab"
      id={`${ctx.id}-tab-${value}`}
      aria-selected={active}
      aria-controls={`${ctx.id}-panel-${value}`}
      tabIndex={active ? 0 : -1}
      onClick={() => ctx.setValue(value)}
      className={cn(
        "relative z-10 cursor-pointer text-sm transition-colors duration-(--motion) ease-motion focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring/60",
        ctx.variant === "segmented"
          ? cn(
              "rounded-control px-3 py-1.5",
              active ? "font-semibold text-foreground" : "text-muted-foreground hover:text-foreground",
            )
          : cn(
              "-mb-px border-b-2 px-3 py-2",
              active
                ? "border-foreground font-semibold text-foreground"
                : "border-transparent text-muted-foreground hover:text-foreground",
            ),
        className,
      )}
    >
      {children}
    </button>
  );
}

export function TabsContent({
  value,
  className,
  children,
}: {
  value: string;
  className?: string;
  children: React.ReactNode;
}) {
  const ctx = React.useContext(TabsCtx)!;
  if (ctx.value !== value) return null;
  return (
    <div
      role="tabpanel"
      id={`${ctx.id}-panel-${value}`}
      aria-labelledby={`${ctx.id}-tab-${value}`}
      className={cn("mt-3", className)}
    >
      {children}
    </div>
  );
}
```

---

# متن رابط کاربری (persian-ui-copy)
دکمه، لیبل، پیام خطا، حالت خالی و توست به فارسی درست. با واژه‌نامه‌ی رابط کاربری تا Login بشه «ورود» و Submit بشه «ثبت»، نه «ارسال نمایید».
npm: none beyond react / tailwind
registry: none

## Files

#### .claude/skills/persian-ui-copy/SKILL.md

```md
---
name: persian-ui-copy
description: >
  Write Persian (Farsi) UI microcopy: button labels, field labels and
  placeholders, validation and error messages, empty states, loading and
  success toasts, confirmations, notifications. Use whenever generating or
  translating any user-facing string for an Iranian product (متن دکمه، پیام
  خطا، لیبل فرم، ترجمه‌ی رابط کاربری، فارسی‌سازی). Includes an English→Persian
  UI glossary so «Login» becomes «ورود» and «Submit» becomes «ثبت», never a
  literal translation.
---

# Persian UI copy (متن رابط کاربری)

Interface strings are short, so every wrong word is loud. Models produce two
failure types: literal translations («ارسال نمایید» for Submit) and mismatched
register (a bureaucratic error under a friendly form). This skill fixes both.

## 1. Choose the product register once

| Register | Use for | Verb style |
|---|---|---|
| Formal-but-human (default) | Banking, B2B, admin panels, government, health | می‌شود، کنید، است |
| Light conversational | Consumer apps, shops, social, onboarding | میشه، می‌تونید، کنید |

Hold it across the whole product. «ذخیره شد» next to «پروفایلت آماده‌ست» in the
same screen is the mixing error. Imperatives («ذخیره کنید»، «بزنید») are the same
in both registers.

## 2. Glossary (English → Persian UI)

| English | Persian | Note |
|---|---|---|
| Login / Sign in | ورود | not «لاگین» |
| Sign up / Register | ثبت‌نام | with ZWNJ |
| Log out | خروج | |
| Submit | ثبت / ارسال | «ثبت» for forms that save, «ارسال» for messages |
| Save | ذخیره | |
| Cancel | انصراف | «لغو» for cancelling an order |
| Delete | حذف | |
| Edit | ویرایش | |
| Continue / Next | ادامه / بعدی | |
| Back / Previous | بازگشت / قبلی | |
| Done / Finish | تمام / پایان | |
| Retry | تلاش دوباره | |
| Search | جست‌وجو | with ZWNJ; «جستجو» is common but less correct |
| Filter / Sort | فیلتر / مرتب‌سازی | |
| Settings | تنظیمات | |
| Profile / Account | پروفایل / حساب کاربری | |
| Dashboard | داشبورد | |
| Notifications | اعلان‌ها | |
| Cart / Checkout | سبد خرید / پرداخت | |
| Order / Orders | سفارش / سفارش‌ها | |
| Add to cart | افزودن به سبد | |
| Buy now | خرید | |
| Price / Total | قیمت / جمع کل | |
| Discount / Coupon | تخفیف / کد تخفیف | |
| Email / Password | ایمیل / رمز عبور | |
| Phone number | شماره موبایل | «شماره تلفن» only for landlines |
| Verification code | کد تأیید | |
| Resend code | ارسال دوباره‌ی کد | |
| Address / Postal code | آدرس / کد پستی | |
| Upload / Download | آپلود / دانلود | «بارگذاری» is fine for formal |
| Loading… | در حال بارگذاری… | |
| Help / Support | راهنما / پشتیبانی | |
| Terms / Privacy | قوانین و مقررات / حریم خصوصی | |
| Yes / No | بله / خیر | avoid on buttons; see section 5 |
| OK | باشه (light) / تأیید (formal) | |

## 3. Buttons and actions

- One verb, no «کلیک کنید»: «ذخیره»، «ادامه»، «پرداخت». The label is the
  outcome, not the gesture.
- Primary action first in the reading order (right side in RTL), secondary
  «انصراف» after it.
- Destructive actions name the object: «حذف سفارش» not «حذف»، and the confirm
  dialog repeats it.
- Persian labels run longer than English. Leave room; never truncate a button.

## 4. Forms

- Label above the field, always visible; placeholder is an example, not a
  label: label «شماره موبایل», placeholder «مثلاً ۰۹۱۲۳۴۵۶۷۸۹».
- Required fields: mark optional ones with «(اختیاری)» instead of starring
  everything.
- Error text sits under the field and says what to change:
  «شماره موبایل باید ۱۱ رقم باشد و با ۰۹ شروع شود.»
  Never «خطا!»، never «مقدار نامعتبر است»، never «Oops».
- Helper text is one short sentence: «کد تأیید به این شماره پیامک می‌شود.»
- Password rules are listed before the user fails them.
- Do not tell users «فقط با حروف انگلیسی» unless the backend truly requires it.

## 5. Confirmations and dialogs

- Title asks the real question: «سفارش حذف شود؟»
- Buttons carry the action, not yes/no: «حذف کن» / «منصرف شدم» (light) or
  «حذف» / «انصراف» (formal).
- One sentence of consequence if it matters: «این کار قابل بازگشت نیست.»

## 6. Empty, loading, success, failure

| State | Pattern | Example |
|---|---|---|
| Empty | what goes here + the next action | «هنوز سفارشی ثبت نکرده‌اید. اولین سفارش را از فروشگاه شروع کنید.» |
| Loading | «در حال …» + ellipsis | «در حال ارسال…» |
| Success toast | short past tense | «ذخیره شد»، «کد ارسال شد» |
| Failure toast | what failed + what to do | «اتصال برقرار نشد. دوباره تلاش کنید.» |
| Offline | plain | «اینترنت قطع است.» |
| 404 | plain + a way out | «این صفحه وجود ندارد. به خانه برگردید.» |

Never «مشکلی پیش آمد» alone; say which thing and what next.

## 7. Numbers, money, dates inside copy

- Persian digits: «۳ کالا»، «۲ ساعت پیش». Thousands with «٬»: «۱٬۲۵۰٬۰۰۰».
- Unit after the number: «۱۲٬۰۰۰ تومان». Never «$», never «Toman».
- Percent after the number with «٪»: «۲۰٪ تخفیف».
- Dates Jalali: «۲۹ شهریور ۱۴۰۵»، relative «دیروز»، «۳ روز پیش».
- Plurals with numbers stay singular: «۳ کالا» not «۳ کالاها».
- Counts of one: «۱ پیام جدید» is fine; «یک پیام جدید» reads warmer.

## 8. Wording hygiene

- Address the user with «شما» verbs; the verb carries it, so do not repeat
  «شما» in every sentence. No «کاربر گرامی».
- No تعارف in UI («لطفاً» once per screen at most; «خواهشمندیم» never).
- No exclamation marks on errors; at most one «!» on a celebration.
- ZWNJ everywhere it belongs: می‌شود، ثبت‌نام، اعلان‌ها، سفارش‌ها.
- Persian «،» «؟» and «گیومه»; no em dashes.
- Latin brand names stay Latin («Google»، «PayPing»); Persian brands stay
  Persian («زرین‌پال»).
- Keep one term per concept across the product: pick «سفارش» or «خرید», not
  both for the same object.

## 9. Before / after

| Prompt | ❌ | ✅ |
|---|---|---|
| Submit button on a signup form | ارسال نمایید | ثبت‌نام |
| Invalid phone | شماره تلفن وارد شده نامعتبر می‌باشد | شماره موبایل باید ۱۱ رقم باشد و با ۰۹ شروع شود. |
| Empty orders list | هیچ داده‌ای یافت نشد | هنوز سفارشی ثبت نکرده‌اید. |
| Delete confirm | آیا مطمئن هستید؟ بله / خیر | سفارش حذف شود؟ حذف / انصراف |
| Saved toast | عملیات با موفقیت انجام شد | ذخیره شد |
| Price | 12,000 Toman | ۱۲٬۰۰۰ تومان |

## 10. Checklist

1. Register chosen and consistent across the screen.
2. Every label from the glossary or a deliberate deviation.
3. Errors say what to fix; empty states say what to do next.
4. Persian digits, units after numbers, Jalali dates.
5. ZWNJ, Persian punctuation, no exclamation on errors.
```