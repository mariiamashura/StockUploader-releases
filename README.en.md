# Stock Uploader

<img src="design/icon.png" width="96" align="right" alt="">

[Русский](README.md) · **English** · [Deutsch](README.de.md)

A Windows program that prepares photos for sale on Shutterstock: it checks the files, shows descriptions and keywords for editing, lets you touch up a photo and uploads everything to the stock site.

![Program window](design/light_en.png)

## About

- **File check.** Filters out photos the stock site will not accept: under 4 MP, over 150 MP, heavier than 50 MB, not JPEG.
- **Descriptions and keywords** in three ways: one click with an API key (Anthropic, OpenAI or Google), through any AI agent with access to the folder (Claude Code, Codex, Gemini CLI), or by hand. The API key is optional: with a subscription to an AI agent no paid API is needed.
- **Marks for manual editing.** Sections that need your knowledge (animal species, shooting location, people and logos in the frame) get an orange frame with a hint on what to do.
- **Editor.** Crop and horizon straightening, light and colour, patch and clone stamp for removing logos and spots. The originals are never changed.
- **Receiving photos from a phone** over Wi-Fi through a QR code, with no app on the phone.
- **Upload.** FTPS upload that resumes after a dropped connection, and a ready CSV for the Submit page.
- **Interface** in Russian, English and German, with dark and light themes.

**Idea:** M. Mashura
**Technical implementation:** Claude (Anthropic)

## Installation

1. Download `StockUploader-0.1.0-win64.zip` from the [Releases](../../releases/latest) page.
2. Unpack it into any folder.
3. Run `StockUploader.exe`.

Nothing needs to be installed and Python is not required. The program is not signed, so on first start
Windows may show a SmartScreen warning — click “More info” → “Run anyway”.

Descriptions can be obtained with an API key right in the program (Settings → “Descriptions (AI)”) or through
any AI agent: the “Copy request for AI” button puts the instructions into the photo folder.

## Quick guide

1. **Open a folder** with photos (JPEG). Files that are too small or too heavy go to “Rejected”.
2. **Photos from a phone.** Click “From phone”, point the phone camera at the QR code and choose photos on the page that opens. The phone and the computer must be on the same Wi-Fi network; on first use Windows asks for network access — allow it. The photos are saved to `Pictures\StockUploader\Phone`, in a subfolder named by today's date, and the program opens it right away. You can choose another folder in Settings.
3. **Touch up the photos** if needed: crop and horizon, light and colour, patch and clone stamp. Every tool has “Apply” and “Cancel”.
4. **Type the context** at the bottom left — place, event, species name (in English). This cannot be known from the picture.
5. **Get the descriptions.** Three ways. The “Describe with API key” button — the program sends reduced copies to the chosen provider itself (enter the key in Settings, “Descriptions (AI)” tab; this costs money, billed through your account with the provider). The “Copy request for AI” button — the program puts instructions into the photo folder, and you paste the copied request to any AI agent that can see that folder and look at images. Or type the descriptions by hand. The photos move to “Ready” or “Need attention” on their own.
6. **Go through the marked ones.** A section with an orange frame needs editing, or click “Keep as is”. Press **N** for the next marked photo.
7. **Upload.** “Upload to Shutterstock” sends the ready photos and creates a CSV file.
8. **Finish on the website.** On the Submit page click CSV, choose the created file, select the photos and click Submit.

The Shutterstock login and password are entered once in Settings; the password is kept in Windows Credential Manager. All edits are saved automatically.

## Where things are

| What | Where |
|---|---|
| Edited versions of photos | `_edited` subfolder in the photo folder |
| Copies for upload and the CSV | `_shutterstock` subfolder |
| Descriptions from AI | `_metadata.jsonl` file |
| Instructions for an AI agent | `_AI_INSTRUCTIONS.md` file in the photo folder |
| Photos from a phone | `Pictures\StockUploader\Phone\YYYY-MM-DD` |
| Settings | `%APPDATA%\StockUploader\config.json` |
| Your edits, log | `%LOCALAPPDATA%\StockUploader` |
| Category list and blocked words | `categories.txt`, `blocklist.txt` next to the program |

## Limitations

- JPEG only; video, vector, RAW and HEIC are not supported.
- The last step — uploading the CSV and clicking Submit — is done by hand on the website: Shutterstock offers no way to do it programmatically.
- Descriptions are written by an AI: through your own API key (paid, with the provider) or an external AI agent; the program invents nothing itself. API-key support was tested on stand-in answers, not on the providers' real servers; the quality of different models' descriptions has not been compared. Work with specific AI agents has not been tested.
- ExifTool is not included. Without it, descriptions and keywords reach the stock site through the CSV, which is enough; writing them into the files themselves turns on if you put `exiftool.exe` next to the program.

## Documentation and terms

- [User guide](docs/USER_GUIDE.md) (in Russian)
- [Changelog](CHANGELOG.md) (in Russian)
- [Terms of use](LICENSE.txt)

The program is free. The source code is not published.
