---
name: flutter-style
description: "Flutter UI styling guidelines to avoid Apple App Store rejections for looking too much like Android/Material. Use automatically when creating, modifying, or styling Flutter widgets. Defines which Material widgets to replace, which to customize, and how to avoid unnecessary rewrites with GestureDetector."
user-invocable: false
tools: [read, write, edit]
---

# Flutter Style — Apple Compliance

## When to use this skill

Whenever a Flutter task involves creating, modifying, or styling UI components — especially when choosing between Material widgets and custom implementations.

---

## Context

Apple rejects apps that look too much like stock Android / Material Design. The goal is **not** to avoid the `material.dart` package entirely — it is to ensure the app does not visually resemble a default Android application.

---

## Decision criteria

Ask yourself: **"Would an Apple reviewer recognize this component as Android?"**

- If **yes** → replace it with a custom component (or a project-specific component library if available)
- If **no** → keep the Material widget and customize its styling (colors, shapes, spacing)

The package import is irrelevant. `ListTile` from `material.dart` is fine. A stock `FloatingActionButton` with its default shadow and shape is not.

---

## Widgets to REPLACE (strong Material identity)

These widgets have a distinctive Android look that is hard to remove through styling alone. Replace them with custom implementations:

| Widget                              | Why                                                  | Alternative                              |
| ----------------------------------- | ---------------------------------------------------- | ---------------------------------------- |
| `FloatingActionButton`              | Signature Android pattern, Apple has no equivalent   | Custom positioned button                 |
| `BottomNavigationBar`               | Material 3 styling, pill-shaped indicator            | Custom tab bar (`CupertinoTabBar`-style) |
| `NavigationRail`                    | Desktop Material pattern                             | Custom navigation panel                  |
| `MaterialBanner`                    | Material-specific pattern                            | Custom banner                            |
| `Drawer`                            | Android hamburger menu pattern                       | Custom slide panel or bottom sheet       |
| `SnackBar`                          | Bottom-anchored Material toast                       | Custom toast / overlay notification      |
| `Chip` / `InputChip` / `FilterChip` | Material 3 shape and elevation                       | Custom tag or selection widget           |
| `ExpansionTile`                     | Material ripple + divider styling                    | Custom expandable with Cupertino feel    |
| `BottomSheet` (default)             | Material drag handle + rounded corners Android-style | Custom modal with iOS-style presentation |

---

## Widgets OK to CUSTOMIZE (structural, no visual identity)

These widgets are layout primitives or structural containers. They have no inherent "Android look" when properly themed. **Keep them and customize via ThemeData or widget parameters:**

| Widget                        | Why it's fine                     | Customization needed                                                   |
| ----------------------------- | --------------------------------- | ---------------------------------------------------------------------- |
| `ListTile`                    | Layout helper, no visual identity | Adjust `contentPadding`, `shape`, `splashColor`                        |
| `AppBar`                      | Structural, fully customizable    | Remove elevation, customize `backgroundColor`, `surfaceTintColor`      |
| `Scaffold`                    | Pure structure                    | None                                                                   |
| `Card`                        | Container with elevation          | Adjust `elevation`, `shape`, `margin`                                  |
| `Switch`                      | Can be styled to look like iOS    | Use `Switch.adaptive()` or custom track/thumb colors                   |
| `Checkbox`                    | Can be styled                     | Use `Checkbox.adaptive()` or custom shape                              |
| `Slider`                      | Structural input                  | Customize `trackShape`, `thumbShape`                                   |
| `TextField` / `TextFormField` | Input primitive                   | Use `OutlineInputBorder` or `UnderlineInputBorder` with custom styling |
| `IconButton`                  | Tappable icon, universal pattern  | Adjust `splashRadius`, padding                                         |
| `InkWell` / `InkResponse`     | Tap feedback, invisible when idle | Customize `splashColor`, `highlightColor`                              |
| `TabBar`                      | Can be restyled completely        | Custom `indicator`, remove Material divider                            |
| `AlertDialog`                 | Can be styled to look like iOS    | Customize shape, padding, button layout                                |
| `PopupMenuButton`             | Contextual menu, universal        | Customize `shape`, `elevation`, `color`                                |

---

## Anti-pattern: rewriting structural widgets from scratch

**Never** replace a structural widget with a manual `GestureDetector` + layout tree just because it comes from `material.dart`.

### Bad: rewriting ListTile

```dart
// ❌ 30+ lines, loses accessibility, semantics, and ink splash
GestureDetector(
  onTap: onTap,
  child: Container(
    padding: EdgeInsets.symmetric(horizontal: 16, vertical: 12),
    child: Row(
      children: [
        icon,
        SizedBox(width: 16),
        Expanded(child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(title, style: ...),
            Text(subtitle, style: ...),
          ],
        )),
        trailing,
      ],
    ),
  ),
)
```

### Good: customized ListTile

```dart
// ✅ 8 lines, accessible, semantic, maintains ripple feedback
ListTile(
  leading: icon,
  title: Text(title),
  subtitle: Text(subtitle),
  trailing: trailing,
  onTap: onTap,
  contentPadding: EdgeInsets.symmetric(horizontal: 16, vertical: 4),
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
)
```

### When IS a GestureDetector appropriate?

Only when the interaction pattern genuinely doesn't match any existing widget:

- Custom drag-to-reorder behavior
- Complex gesture recognition (pinch, long-press + drag)
- Fully custom painted components

---

## Theming strategy

Prefer global theming over per-widget styling to maintain consistency:

```dart
ThemeData(
  // Remove Material 3 visual signatures
  splashFactory: InkSparkle.splashFactory, // or NoSplash.splashFactory for iOS feel
  cardTheme: CardTheme(
    elevation: 0,
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
  ),
  listTileTheme: ListTileThemeData(
    contentPadding: EdgeInsets.symmetric(horizontal: 16),
    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
  ),
  appBarTheme: AppBarTheme(
    elevation: 0,
    scrolledUnderElevation: 0,
  ),
)
```

---

## Gotchas

- **Never** avoid a widget solely because its import path contains `material.dart` — almost every Flutter widget lives there, including `Scaffold`, `Text`, and `Column`.
- **`adaptive()` constructors exist** for `Switch`, `Checkbox`, `CircularProgressIndicator` — prefer these when available, they automatically use Cupertino styling on iOS.
- **Ripple effects** are not inherently "Android" — tap feedback is expected on both platforms. Adjust `splashColor` and `highlightColor` rather than removing feedback entirely.
- **Elevation/shadows** are the biggest visual tell for Material — prefer `elevation: 0` with subtle `border` or `boxShadow` instead of Material's default lifted cards.
- **Material 3 pill indicators** (on NavBar, TabBar) are distinctly Android — replace these with underline or dot indicators.
- **Do not use `CupertinoApp`** unless the entire app is Cupertino — mixing `MaterialApp` with Cupertino widgets is fine and is the standard approach for cross-platform Flutter apps.
