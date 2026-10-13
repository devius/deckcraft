# Georgian interface

> **Last reviewed:** 2026-10-13 · **Last updated:** 2026-10-13 · **Change:** minor (Georgian interface notes and terminology) · **Target:** DeckCraft 0.6.1

Choose **Review › Language** or **Preferences… (Cmd+,) › Interface language › ქართული**, or follow a
Georgian system locale (`ka`, `ka-GE`, `ka_GE.UTF-8`; the system choice is read through
`sys_locale` when the preference is **System language**). The catalog code is `ka`; the control and
MCP command `app.language` with `{"language":"ka"}` selects it explicitly. The choice is saved with
the other interface settings. Slide text, command ids, CLI/MCP/control responses and file paths do
not change.

`crates/ui-egui/src/i18n/ka.tsv` has 1,309 entries: all 1,232 keys of the Ukrainian catalog plus 77 labels upstream added since
(File › Print/Info, IME commands, new preset shapes, transition Effect Options). It
covers the ribbon tabs and commands, menus, dialogs, panes, the shape and gallery names, and status
captions. Diagnostics from lower layers (file import, rendering, media) keep their English wording,
as in the other languages. It is written from the meaning of the English labels; no proprietary
translation resources were consulted.

## Georgian script

- **No case.** Mkhedruli has no upper and lower case. Change Case › Sentence case and Capitalize
  Each Word leave Georgian letters alone; UPPERCASE and Toggle Case follow Unicode and give Mtavruli
  (`ᲐᲑᲒ`). The interface never uses Mtavruli, and commands are verbal nouns (`შენახვა`, `ჩასმა`).
- **Counts** are count-neutral: the noun comes first and stays singular (`სლაიდი: 5`), so `count()`
  takes a single Georgian form.
- **Dates:** short date fields use `dd.mm.yyyy`.
- **Fonts:** neither the bundle nor craft-fonts has a Georgian face yet. The desktop app adds an
  installed face as a UI fallback (SF Georgian or Arial Unicode on macOS, Sylfaen on Windows, Noto
  Sans Georgian or DejaVu Sans on Linux) and ships nothing. Slide text uses the system font fallback
  the same way. The web (WASM) build has no Georgian face, so Georgian shows as boxes there until
  an OFL face (such as Noto Sans Georgian) is added to craft-fonts.

## Terminology

| Source | Georgian |
|---|---|
| Home (ribbon tab) | მთავარი |
| Insert / Paste | ჩასმა |
| Design / Themes | დიზაინი / თემები |
| Transitions / Animations | გადასვლები / ანიმაციები |
| Slide Show / From Beginning | სლაიდშოუ / დასაწყისიდან |
| Review / Spelling | განხილვა / მართლწერა |
| View / Normal | ჩვენება / ჩვეულებრივი |
| New Slide / Duplicate Slide | ახალი სლაიდი / სლაიდის დუბლირება |
| Slide Master | მასტერ-სლაიდი |
| Slide Sorter | სლაიდების დამხარისხებელი |
| Presenter View | მომხსენებლის ხედი |
| Notes / Notes Page | შენიშვნები / შენიშვნების გვერდი |
| Layout | განლაგება |
| Shapes / Format Shape | ფიგურები / ფიგურის ფორმატირება |
| Shape Fill / Shape Outline | ფიგურის შევსება / ფიგურის კონტური |
| Picture / Chart / Table | სურათი / დიაგრამა / ცხრილი |
| Text Box | ტექსტური ბლოკი |
| Font / Paragraph | შრიფტი / აბზაცი |
| Change Case | რეგისტრის შეცვლა |
| Undo / Redo | დაბრუნება / ხელახლა შესრულება |
| Slide Size | სლაიდის ზომა |
| Hide Slide / Rehearse Timings | სლაიდის დამალვა / დროის გაზომვა |
| Link / Comments | ბმული / კომენტარები |
| Section | სექცია |

Please follow this table and the shared ArtCraft Georgian glossary when you add strings. Product and
format names stay as they are.

## Verification and maintenance

Add a string to `crates/ui-egui/src/i18n/ka.tsv` as `English source<TAB>Georgian` (`\n` for a line
break), next to the same key in the other catalogs. Keep placeholders (`{}`, `{n}`), ellipses and
`\n` breaks exactly; strings added later fall back to English until they are translated.

`cargo test -p deckcraft-ui-egui --lib i18n` checks that every catalog has the same keys, that
placeholders match, that every command, menu, gallery and literal `tr()` label has an entry, the
`ka`/`ka-GE` locale detection and saved preference, unchanged document data, and that the UI font
covers Georgian when an installed face exists. The ignored test
`i18n::tests::translated_interface_preview` (run with `DECKCRAFT_I18N_SHOTS=<dir>`) renders the
editor, Preferences and Table dialogs in every language for a visual check. A native-speaker skim
is welcome.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-13 | minor | Georgian interface notes and terminology |
