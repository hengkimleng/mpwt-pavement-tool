MPWT Pavement Design & Compliance Tool
A free, self-contained web app for designing and checking road pavements against Cambodia's Ministry of Public Works and Transport (MPWT) Road Design Specification, Part 2 – Pavement (D3 102-2024).

Open the live tool →

(Update the link above once GitHub Pages is enabled — see Deployment below.)


What it does
The tool combines a design calculator and a compliance checker in one page, with five tabs:

Tab
Function
1. Design Traffic (ESA)
Calculates cumulative Design Traffic (Equivalent Standard Axles) from AADT, heavy-vehicle %, growth rate, and traffic load distribution, per D3 102-2024 §7.1–7.8 and Appendix E.
2. Flexible Pavement
Looks up the required granular pavement structure from the Section 11.8.3 catalogue (Figure 11.3 / TRL Road Note 31, 2023) based on subgrade CBR and design traffic category, and lets you compare a proposed design against it layer by layer. Also includes the Section 8.3.1 general empirical design chart (Figure 8.4), valid for the wider 10⁵–10⁸ ESA range.
3. Rigid Pavement
Checks a proposed concrete pavement design (base thickness, subbase, flexural strength, dowel bar diameter) against the minimum requirements in Section 9 (Tables 9.1, 9.7, 9.8).
4. Mechanistic-Empirical (Experimental)
⚠️ Experimental, unvalidated. An independently-built n-layer layered-elastic (Burmister-type) solver implementing the general theory that D3 102-2024 §8.2 itself delegates to external software (AustPADS/CIRCLY). Computes critical strains directly beneath a single standard-axle wheel load and checks them against the Section 5/6 fatigue criteria (Equations 5.2, 6.8, 6.15). See Scope and limitations below before using this tab for anything beyond exploration.
5. Compliance Report
Compiles the results from all other tabs into a formatted, printable MPWT-style compliance review report with pass/fail status indicators.


All reference tables, thresholds, and catalogue values are transcribed directly from the official D3 102-2024 PDF (First Edition 2024, approved under Prakas No. 133 សក.ប្រក, 20 August 2024) and cite the exact clause, table, or figure number they come from.
Scope and limitations
Tabs 1–3 and 5 cover the parts of D3 102-2024 that are catalogue- or table-based and fully closed-form:

Flexible pavements (catalogue method, Tab 2): valid only for design traffic up to 3×10⁶ ESA (the range covered by the Section 11.8.3 catalogue). The Figure 8.4 general method on the same tab extends this to 10⁵–10⁸ ESA.
Rigid pavements: checks the minimum requirement tables only (Section 9.2–9.4.4). It does not perform the full base-thickness design procedure (fatigue/erosion nomograph analysis, §9.4) — that requires specialist software.
Subgrade CBR, material test results, and site data must be supplied by the user (from geotechnical investigation per D1-101); the tool does not verify these inputs independently.
Tab 4 (Mechanistic-Empirical) — read before using
D3 102-2024 §8.2 does not itself provide a formula for layered-elastic strain calculation — it explicitly requires "computer programs such as AustPADS" capable of modelling a multi-layer elastic pavement. Tab 4 is an independent, from-scratch implementation of that general theory (n-layer axisymmetric elastic / Burmister-type analysis, via a Love strain-function and Hankel-transform formulation), built because no AustPADS/CIRCLY-equivalent tool is available in this environment. It is not part of the official MPWT specification and has not been reviewed by MPWT.

What has been checked: the solver's output matches the closed-form Boussinesq single-layer solution to machine precision, and matches a published 3-layer benchmark (Jones 1962, cross-checked by Wang/Roesler/Guo 2011) to 4–5 significant figures. What has not been checked: there is no AustPADS, CIRCLY, or other MPWT-recognised software available here to cross-validate real project inputs. The module also only evaluates the critical strain directly beneath the centre of a single circular wheel load (on-axis) — it does not implement multi-wheel (dual-tyre) superposition or the "between tyres" check that Figure 8.2 / Table 8.2 of the Specification call for, which can govern for some geometries.

Do not use Tab 4 results for an MPWT submission or construction decision without independent verification by a qualified pavement engineer using MPWT-recognised software.

This tool is a design aid, not a substitute for review and sign-off by a licensed pavement/civil engineer. Always verify figures against the current official copy of D3 102-2024 before submission.
Technology
Single self-contained HTML file — all CSS and JavaScript are inline, no build step, no external dependencies, no API calls.
Runs entirely in the browser (client-side only). No data is sent anywhere, no internet connection is required once the page is loaded, and no server or backend is involved.
Works fully offline after the first load; can be opened directly from disk (index.html) or hosted anywhere that serves static files.
Usage
Open index.html in any modern browser (Chrome, Edge, Firefox, Safari).
Go to Tab 1 and enter road/traffic data to calculate Design ESA — or skip straight to Tab 2/3 if you already have a design traffic figure.
Tab 2 — enter subgrade CBR and traffic category to get the required flexible pavement structure, and optionally enter a proposed design to compare.
Tab 3 — enter a proposed rigid pavement design to check it against minimum requirements.
Tab 4 — generate a compliance report summarizing all checks; use the print button to export as PDF.
Deployment
This is a static site, so GitHub Pages is the simplest way to host it:

Push this repo to GitHub with the tool saved as index.html at the repo root.
In the repo, go to Settings → Pages.
Under Build and deployment, set Source to Deploy from a branch, branch main, folder / (root).
Save — GitHub will publish the site at https://<your-username>.github.io/<repo-name>/ within a minute or two.
Source
Ministry of Public Works and Transport, Kingdom of Cambodia. Road Design Specification, Part 2 – Pavement (D3 102-2024), First Edition, 2024. Approved under Prakas No. 133 សក.ប្រក, dated 20 August 2024. Pavement catalogue methodology adapted from TRL Road Note 31 (2023) and the Austroads Guide to Pavement Technology.
Disclaimer
This is an unofficial, independently-built tool and is not published or endorsed by MPWT. Values were transcribed carefully from the official specification and spot-checked, but no guarantee of accuracy is made — always cross-check against the current official document. The authors accept no liability for designs produced using this tool.

