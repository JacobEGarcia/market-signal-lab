# Market Signal Lab

Three paper-only categorization projects, one local server and a shared UI:

- `http://127.0.0.1:4545/?lane=day` - intraday setup categories
- `http://127.0.0.1:4545/?lane=stocks` - company and macro event categories
- `http://127.0.0.1:4545/?lane=predictions` - Kalshi/Polymarket question categories

Run with Node 20+: `npm start`. No install or package download is required. Run `npm test` for parsing, model contract and lane tests. Load clearly labeled synthetic demo data or import your own local CSV. CSV header: `timestamp,symbol,title,price,change,volume,source` (`title` is required). Imported data stays local until the user explicitly clicks **Sort with free JEV**. The CSV export remains local.

## Optional JEV

Free `jev-1.13-free` requires a BeatAPI key supplied by the owner. In your local shell set `BEATAPI_API_KEY` as an environment variable, then start `npm start`. Do not paste credentials in chat, upload `.env` or put a key in frontend code. The server sends batches of up to 20 stripped-down metadata rows to `POST https://api.beatapi.io/v1/systemone`; it does not send a brokerage, exchange, wallet, or account credential. The vendor documents one successful request per minute for never-topped-up free accounts. The app waits 61 seconds between batches, rejects unknown response choices, stops on errors and never silently switches to the paid model. A local keyword-rules sorter is always available with no key or API call. JEV is a bounded classifier, not a price-prediction or generative model. See https://docs.beatapi.io/decisions and https://beatapi.io/jev-api.

## Limits

No broker or exchange integration, no order entry, no trades, no positions, no portfolio tracking, no live data feed, no claims of profitability. Demo data is synthetic and not backtest evidence. For real public-data analysis, import timestamped public observations and retain their source URL in `source`; source and time should be checked before relying on the classification. Classification alone has no predictive validity. Do not use any category as a trade recommendation.

This adapts the reference post's batch progress, category mix and timeline design to three market-event taxonomies. The original post classifies 207 *bank transactions*; it does not demonstrate a trading strategy: https://x.com/willdjthrill/status/2103556432729870627 .
