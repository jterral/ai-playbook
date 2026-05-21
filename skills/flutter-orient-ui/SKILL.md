---
name: flutter-orient-ui
description: "Guidelines for using Orient UI components in Flutter. Use automatically when creating or modifying Flutter widgets (buttons, navigation, toasts, popups, toggles, search fields, cards, tiles). Orient UI components are copied from GitHub templates, never imported as a package."
user-invocable: false
tools: [bash, read, write, edit]
---

# Flutter Orient UI

## When to use this skill

Whenever a Flutter task requires creating or modifying a UI component (button, navigation, toast, popup, selection, toggle, search field, etc.).

---

## Prerequisites

- Flutter project with an existing `lib/app/app.style.dart` style file
- Target directory `lib/shared/widgets/` exists (or will be created)
- Internet access to fetch templates from GitHub
- Determine the package name from `pubspec.yaml` (`name:` field) — replace all occurrences of `your_app` in the examples below with this value

---

## Core principle

This project uses **Orient UI** as its component library. Orient UI is **not a package to add to `pubspec.yaml`**: it is a collection of `.dart` files that you copy directly into the project. You own the code and can modify anything freely.

- Documentation (read-only reference, do NOT install): https://pub.dev/packages/orient_ui
- Source templates (fetch from here): https://github.com/UserOrient/orient-ui/tree/main/templates

---

## Golden rule: always copy, never import

When an Orient UI component is needed:

1. **Fetch** the source file from `https://github.com/UserOrient/orient-ui/blob/main/templates/<component_name>.dart`
2. **Copy it** into `lib/shared/widgets/<component_name>.dart`
3. **Update the style import** inside the copied file — replace whatever style import is there with:

```dart
import 'package:your_app/app/app.style.dart';
```

4. **Use the widget** normally throughout the rest of the code.

Never add `orient_ui` to `pubspec.yaml`. Never import from the pub.dev package.

---

## Style file

The project's reference style file is always located at:

```
lib/app/app.style.dart
```

Every copied Orient UI component **must** point to this path. If the copied file contains an import such as `import 'package:your_app/style.dart'` or `import '../style.dart'`, always replace it with:

```dart
import 'package:your_app/app/app.style.dart';
```

---

## Available components

These components exist in the `templates/` folder of the repository:

| Component           | Template file             | Usage                                           |
| ------------------- | ------------------------- | ----------------------------------------------- |
| AlertPopup          | `alert_popup.dart`        | Alert modal                                     |
| Button (6 variants) | `button.dart`             | Primary, secondary, ghost buttons…              |
| CardBox             | `card_box.dart`           | Card container                                  |
| ConfirmationPopup   | `confirmation_popup.dart` | Confirmation modal                              |
| CopyButton          | `copy_button.dart`        | Copy to clipboard button                        |
| EmptyState          | `empty_state.dart`        | Empty screen / placeholder                      |
| InfoBanner          | `info_banner.dart`        | Informational banner                            |
| MultiChoice         | `multi_choice.dart`       | Multiple selection (chips)                      |
| MultiChoiceTile     | `multi_choice_tile.dart`  | Multiple selection (list)                       |
| NavBar              | `nav_bar.dart`            | Navigation rail (desktop) + bottom bar (mobile) |
| Picker              | `picker.dart`             | Picker / selection wheel                        |
| PopoverMenu         | `popover_menu.dart`       | Contextual popover menu                         |
| Popup               | `popup.dart`              | Generic modal window                            |
| SearchField         | `search_field.dart`       | Search input field                              |
| SegmentBar          | `segment_bar.dart`        | Segmented control / tab bar                     |
| SingleChoice        | `single_choice.dart`      | Single selection (chips)                        |
| SingleChoiceTile    | `single_choice_tile.dart` | Single selection (list)                         |
| Spinner             | `spinner.dart`            | Loading indicator                               |
| Tabs                | `tabs.dart`               | Tab navigation                                  |
| Tag                 | `tag.dart`                | Label / badge tag                               |
| TappableIcon        | `tappable_icon.dart`      | Icon button with tap feedback                   |
| Tile                | `tile.dart`               | Clickable list item                             |
| Toast               | `toast.dart`              | Ephemeral notifications                         |
| Toggle              | `toggle.dart`             | On/off switch                                   |
| ToggleTile          | `toggle_tile.dart`        | Tile with built-in toggle                       |

> **Note:** The `style.dart` template in the repository is the base style reference — it is already covered by `lib/app/app.style.dart` in the project.

> **This list may become outdated.** If the user mentions an Orient UI component not listed here, check `https://github.com/UserOrient/orient-ui/tree/main/templates` for its availability before refusing.

---

## Concrete example: adding a Toggle

Need a toggle switch in the UI?

1. Fetch `https://github.com/UserOrient/orient-ui/blob/main/templates/toggle.dart`
2. Place it at `lib/shared/widgets/toggle.dart`
3. In `toggle.dart`, update the import:

```dart
import 'package:your_app/app/app.style.dart';
```

4. Use it anywhere in the project:

```dart
import 'package:your_app/shared/widgets/toggle.dart';
```

---

## Accessing the theme from any widget

```dart
import 'package:your_app/app/app.style.dart';

// Inside a widget:
final colors = context.style.colors;
final typography = context.style.typography;
```

---

## Dark mode (if needed)

Wrap `MaterialApp` with `Style` to control brightness manually:

```dart
Style(
  brightness: Brightness.dark,
  child: MaterialApp(
    home: MyHomePage(),
  ),
)
```

By default, widgets follow system brightness — no wrapper required.

---

## Gotchas

- **Never** add `orient_ui` to `pubspec.yaml` — this library is template-based, not a package dependency. Adding it will create version conflicts and defeat the purpose of owning the source.
- **Always** check the "Available components" table before fetching — components listed as "not yet available" do not exist in the templates folder and will result in a 404.
- **Some components depend on others** — e.g., `ConfirmationPopup` may internally use `Button`. If a copied component fails to compile, check its imports for references to other Orient UI widgets and copy those too.
- **Every `.dart` file you copy may contain multiple internal imports** — don't just fix the style import. Scan the entire file for any `import 'package:orient_ui/...'` or relative imports and replace them with the correct project paths.
- **The raw GitHub URL format** for fetching is `https://raw.githubusercontent.com/UserOrient/orient-ui/main/templates/<file>.dart` — do not use the `github.com/blob/` URL for programmatic fetching.
- **If the GitHub repository structure changes**, verify the templates path still exists before fetching. The template list in this skill may become outdated.

---

## Not yet available

Do **not** attempt to fetch or use these components — they are not yet published in the `templates/` folder:

- Typography
- TextField
- Dropdown
- InlineTabs
- Checkbox
- Label
- Tip
- PickerPopup
- VerticalTile
- SocialButton
- AdaptivePageTransition

> If the user mentions a component not in either list, check the [templates folder](https://github.com/UserOrient/orient-ui/tree/main/templates) — new components may have been added since this skill was last updated. Ask the user to update this skill if they confirm a new component exists.
