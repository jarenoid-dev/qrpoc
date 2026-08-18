# Code component inventory (local snapshot, 2026-08-18)

Source: `loveable prototype/src/` inside this repo (jarenoid-dev/qrpoc).
Stack: Vite + React 19 + TypeScript + shadcn/ui "new-york" + Tailwind + lucide icons.
Package name: `tanstack_start_ts`. shadcn aliases: `@/components/ui`, `@/lib/utils`, `@/hooks`.

**Caveat:** this is a local snapshot. Canonical app code is `erkucman/qrpoc` (per repo
CLAUDE.md), intentionally not mirrored. Re-verify at Code Connect activation.

## shadcn/ui primitives — `src/components/ui/` (46)

accordion, alert, alert-dialog, aspect-ratio, avatar, badge, breadcrumb, button, calendar,
card, carousel, chart, checkbox, collapsible, command, context-menu, dialog, drawer,
dropdown-menu, form, hover-card, input-otp, input, label, menubar, navigation-menu,
pagination, popover, progress, radio-group, resizable, scroll-area, select, separator,
sheet, sidebar, skeleton, slider, sonner, switch, table, tabs, textarea, toggle-group,
toggle, tooltip

Verified `cva` variant vocabularies:
- `button.tsx`: variant `default|destructive|outline|secondary|ghost|link`; size `default|sm|lg|icon`
- `badge.tsx`: variant `default|secondary|destructive|outline`

## Feature / screen components (not DS primitives — map to Tablyx Templates, not connected individually)

- `src/components/inventory/`: alerts, dashboard, erp, franchise-aggregate, import-dialog,
  ingredients, purchase-orders, recipes, stock-takes, suppliers, waste
- `src/components/menu-editor/`: canva/, customiser, import-dialog, item-editor,
  menu-preview, template-picker, types
- `src/components/payments/`: payments-manager
- `src/components/` (root): auth-guard, buttons-manager, qr-manager, role-stub,
  users-manager, waiter-performance
