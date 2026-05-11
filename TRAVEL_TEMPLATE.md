# Travel Handbook Template

This project is a reusable mobile travel handbook.

For a new trip, edit `trip-data.js` first. Keep `index.html` as the app shell unless the feature set changes.

## Minimal Trip Config

```js
window.TRIP_CONFIG = {
  tripId: "japan-kansai-2026",
  today: "2026-04-01",
  documentTitle: "2026 日本關西旅行手冊",
  brand: "Kansai 2026",
  heroTitle: "日本關西<br />手機旅行手冊",
  heroSubtitle: "2026/4/1-4/8，8 天 7 夜。",
  heroHint: "往下滑看每日路線。",
  heroImage: "https://example.com/hero.jpg",
  themeColor: "#0f5a49",
  chips: ["KIX 進出", "大阪・京都・奈良", "可共編、可記帳"]
};
```

## Optional Data Overrides

Add `days` and `placeDetails` to replace the built-in Vietnam defaults:

```js
window.TRIP_CONFIG.days = [
  {
    date: "4/1",
    weekday: "三",
    city: "osaka",
    title: "抵達關西機場，前往大阪",
    hotel: "Hotel Name",
    note: "抵達後買交通卡，晚上心齋橋散步。",
    stops: [
      ["上午", "關西國際機場", "入境後前往大阪。", "Kansai International Airport"],
      ["晚餐", "道頓堀", "第一晚覓食。", "Dotonbori Osaka"]
    ]
  }
];

window.TRIP_CONFIG.placeDetails = {
  "Kansai International Airport": "關西國際機場是大阪、京都、奈良旅行常用機場。",
  "Dotonbori Osaka": "道頓堀是大阪代表性美食與夜景區。"
};
```

## Built-In Features

- Mobile itinerary cards
- Google Maps links inside itinerary only
- Place introduction modal
- Editable hotel names
- Expense tracker with category pie chart
- Document/ticket upload
- Booking document can update hotel date ranges
- Receipt/document amount detection from typed text or filenames
- Journal, photos, and voice input
- Offline map preparation checklist
- Google/Firebase sharing hooks for trip companions
