# YarnBop

An interactive PDF pattern reader and row-tracking workspace for knitters and crocheters, built with Flutter.

I built YarnBop for one person: Tina. She crochets and knits from PDF patterns bought on Etsy, Ravelry, and from independent designers — and the apps that offer nice interactive pattern tracking tend to lock you inside their own pattern stores and paywalls. YarnBop is the way out of the walled garden: bring your own PDFs, get the tracking tools, keep your patterns and your progress on your own device.

It's a personal project and a learning project, and it's designed first as a daily-use crafting companion — an app that sits quietly next to the yarn and stays out of the way.

## Who it's for

- Crafters who already own PDF patterns and want to actually work from them on a phone or tablet
- Anyone tired of printing patterns and losing their place with a ruler and a pencil
- One specific crocheter, first — everyone else is welcome along

## What it does

- **Universal PDF import** — load any standard PDF pattern from device storage. No copy-pasting, no re-formatting in an editor, no store account.
- **Project library** — a home screen for managing active and completed patterns.
- **Mobile PDF reader** — patterns render in a viewer laid out for small screens, with the page position remembered per project.
- **Movable line highlighter** — a warm yellow band you drag to the instruction you're on, so your eyes land back in the right place every time you look up from your work.
- **Floating row and stitch counters** — rigid, semi-transparent overlay badges that stay on screen over the PDF, paired with each pattern so every project keeps its own counts.
- **Automatic progress saving** — row counts, stitch counts, page position, and highlighter position save as you go. Close the app, reopen it, resume exactly where you left off. There's no save button because there shouldn't need to be.
- **Text pattern mode** — paste in raw pattern text and YarnBop parses it line by line into numbered rows you can step through and mark complete as you finish them. Parsing runs off the UI thread, so pasting a long pattern doesn't freeze the app.

## Local-first, on purpose

This is a rule of the project, not a feature list item:

- **No accounts, no cloud, no sync.** No Firebase, no Supabase, no REST APIs. Everything lives on the device and the app works offline.
- **Your progress is stored in Hive boxes encrypted with AES.** The encryption key is held in the device's secure storage (`flutter_secure_storage`), not in the app data.
- **Imported PDFs stay yours.** Files are picked from your own storage and referenced locally — nothing is uploaded anywhere, because there's nowhere to upload to.

## The look

YarnBop has a deliberate design system (`DESIGN_SYSTEM.md`): 2010s web nostalgia instead of modern Material 3. Classic web blue and Tumblr navy, content in white cards with visible 1px borders on a light gray canvas, buttons that look like buttons, sharp corners, system fonts at comfortable reading sizes. Crafting tools contrast hard against the pattern — dark counter badges with white text, and that yellow highlighter band. It should feel like the cozy, structured web, not a floating glass dashboard.

## Stack

- **Flutter / Dart** (SDK `>=3.0.0 <4.0.0`), targeting **Android**
- **Riverpod** for state management
- **Hive + Hive Flutter** for local storage, AES-encrypted, keys via **flutter_secure_storage**
- **flutter_pdfview** for PDF rendering, **file_picker** for import, **path_provider** for local paths
- Code is organized feature-first under `lib/features/` (library, pdf_reader, counters, highlighter, pattern_rows), with business logic kept separate from widgets

## Running it

This is a standard Flutter project:

```bash
flutter pub get
flutter run        # with an Android device or emulator attached
flutter test       # unit tests — currently covering the pattern row parser
```

The design and scope rules the code is built against live in the repo: `VISION.md`, `MVP.md`, `DESIGN_SYSTEM.md`, and `PROJECT_RULES.md`.

## Honest status

YarnBop is at MVP stage and in personal use — it's a working local-first pattern reader with the core flow in place (import → read → track → resume), and it's the app Tina crafts with. It is **not** published: there's no Play Store listing and no release build attached to this repo yet, and I'm not going to pretend otherwise. The strict scope boundary in `MVP.md` is real — anything not listed under "What it does" above isn't in the app, even if it sounds like it should be.

Deliberately not here yet (from the vision doc, in roughly this order of interest): pulling text steps straight out of PDFs instead of paste-in, highlighting only your garment size's stitch counts, unit and needle/hook conversion tools, annotations on pattern pages, and yarn stash notes attached to projects.
