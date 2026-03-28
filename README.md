# Equity Valuation Tool

## The Thesis
Market prices often diverge from fundamental value. This tool runs a 
two-method valuation framework — DCF and comparable company multiples — 
on any publicly listed company using live market data. It automatically 
calibrates assumptions from analyst estimates and flags when valuation 
methods are inappropriate (e.g. negative FCF, financial sector stocks).

## The Data
- **Live prices, financials & estimates**: Yahoo Finance API (`yfinance`)
- **Growth rate**: Pulled from analyst revenue growth estimates (TTM)
- **Discount rate**: Auto-calculated from company beta using CAPM logic
- **Sector multiples**: Calibrated to industry averages (P/E, EV/EBITDA)

## The Logic
1. Input any ticker — assumptions are calculated automatically
2. Viability check runs first — blocks DCF if FCF is negative or missing
3. DCF projects free cash flows forward 5 years, fades growth in years 4-5,
   then applies a Gordon Growth terminal value
4. Comps values the company on sector-average P/E and EV/EBITDA multiples
5. A blended average across valid methods produces the final price target
6. Football field chart visualises the range of implied values vs market price

## The Result
The tool correctly identifies when stocks are fundamentally overvalued 
relative to current earnings — for example, flagging high-growth 
infrastructure companies like SEI where the market is pricing in future 
growth not yet visible in the financials. This distinction between 
"expensive" and "uninvestable" is a core part of the analytical output.

## Example Output
| Company | Method | Implied Price | Current Price | Upside |
|---|---|---|---|---|
| Apple | DCF | $194 | $185 | +4.9% |
| Apple | P/E Comps | $201 | $185 | +8.6% |
| Apple | EV/EBITDA | $188 | $185 | +1.6% |

## Tech
`Python` · `Pandas` · `NumPy` · `yfinance` · `Matplotlib` · `Jupyter`

## How to Use
1. Open `equity_valuation_tool.ipynb`
2. Change `TICKER` and `COMPANY_NAME` in Cell 2
3. Run **Kernel → Restart & Run All**
4. All assumptions are calculated automatically from live data
