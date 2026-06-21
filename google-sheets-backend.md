# Google Sheets Backend

This project uses Google Sheets as the editable back office.

The production website uses Plan A: `index.html` reads Google Sheets CSV exports directly in the browser. `data/site-data.json` is now only a fallback shell and stores the fixed seven-galaxy rule cards.

## Sheets

### 社友清單

Required columns:

| 欄位 | 說明 |
| --- | --- |
| 姓名 | Must match names used in 摘星紀錄 |
| 寶(尊)眷 | Optional spouse/family display |
| 身份 | Example: 社長, 社友 |
| 狀態 | Use 啟用 or 停用. Empty means 啟用 |
| 備註 | Optional |

### 摘星地圖

Required columns:

| 欄位 | 說明 |
| --- | --- |
| 月份 | Example: 2026年8月 |
| 日期 | Example: 8/5 or 2026/8/5 |
| 活動 | Activity name |
| 星數 | Number of stars |
| 狀態 | 已完成, 可參加, or 規劃中 |

### 摘星紀錄

Required columns:

| 欄位 | 說明 |
| --- | --- |
| 姓名 | Must match 社友清單 |
| 日期 | Example: 2026/8/5 |
| 活動 | Activity or reason |
| 星數 | Number of stars |
| 備註 | Optional |

## Production Update Flow

For normal updates, edit Google Sheets only:

- Update `社友清單` to add, disable, or edit members
- Update `摘星地圖` to change monthly activities
- Update `摘星紀錄` to change member star records

After saving Google Sheets, refresh the website. GitHub Pages does not need a new upload for data-only changes.

The Google Sheet must remain viewable by anyone with the link.

## Manual Sync Files

These files are only for local backup, debugging, or generating fallback JSON.

Download these CSV files into the project root:

- `google-sheet-members.csv`
- `google-sheet-star-map.csv`
- `google-sheet-star-records.csv`

Then run:

```powershell
& 'C:\Users\neo\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe' 'tools\sync_google_csv.py'
```

If a sheet has only headers and no rows, the sync script preserves existing local website data for that section.
