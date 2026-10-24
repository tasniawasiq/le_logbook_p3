# VMR Run Log — Prototype 3

A trucking activity and expense tracker developed by **Data Vibing** for testing with VMR and Violetta.

**Current build:** `prototype3-v4-test`  
**Status:** Functional browser prototype with owner testing enabled.

The prototype helps drivers record their day, delivery stops, signed delivery bills, fuel and other expenses. The **Analytics** tab brings these records together for review.

> Records and photos are saved in the current browser only. This version does not sync across devices or provide real user accounts. Use sample records for testing.

## Repository files

| File | Purpose |
| --- | --- |
| `index.html` | The application, including its HTML, CSS and JavaScript |
| `README.md` | Setup, testing instructions and current limitations |

Upload `VMR_Run_Log_P3.html` under the name **`index.html`**. No package installation or build step is required. The page uses Google Fonts, with fallback fonts when those cannot load.

## Open or publish the app

For a quick local preview, open `index.html` in a browser. For consistent testing, use the published website and the same browser each time; records entered in a downloaded file do not automatically move to the website.

To publish on GitHub Pages:

1. Upload `index.html` and this `README.md` to the repository's top level.
2. Open **Settings → Pages**.
3. Choose **Deploy from a branch**.
4. Select **main** and **/ (root)**, then click **Save**.
5. Once deployment finishes, open the website link shown on that page and share it with testers.

To update the website, replace `index.html` with the latest version and commit the change. See [GitHub's publishing instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Driver workflow

1. **Add a driver:** Enter a name and truck. This is a local profile, not a user account.
2. **Start my day:** Enter the starting odometer reading. The photo can be skipped during testing.
3. **Record arrival:** Enter the warehouse or customer name and select **I'm here**.
4. **Choose the stop type:** Select **Tow and hook** or **Live unload**. Enter the seal number where applicable.
5. **Complete the bill-of-delivery card:** Confirm receipt of the signed bill, attach its photos, and optionally enter the bill/reference number and amount to double-check against the image.
6. **Complete delivery & leave:** The app shows missing steps beside the button and in an alert. A stop type and signed-bill confirmation are still required during testing.
7. **Log expenses:** Record diesel, repairs, delays or other expenses. Personal expenses are excluded from business expense totals.
8. **End my day:** After the last delivery and all driving—including the return trip—enter the final odometer reading in the visible **End my day** card. An unfinished stop must be completed first. The app saves the finish time and final reading.

## Delivery bills and Thursday payments

The delivery document is essential paperwork for Violetta's Thursday payment process.

- Photos are attached to the specific delivery, alongside its driver, location and date.
- Multiple pages can be uploaded and viewed.
- The optional bill/reference number preserves leading zeros. The amount can be left blank if the document does not show one.
- Analytics includes **Delivery bills · Thursday payment paperwork**, with missing-document indicators and an option to add pages later.
- Tap a photo to enlarge it and access **Download photo**.
- Choose **All** in Analytics to find older documents saved in this browser.

**Paperwork ready does not mean payment received.** This prototype does not automatically submit bills, create Thursday payment batches or track confirmed payments.

## Owner testing: photos are temporarily optional

The current build uses:

```javascript
const OWNER_TEST_MODE = true;
```

The interface keeps the **Required** photo labels to show the intended workflow, but test mode allows the owner to skip delivery-bill and odometer photos, including diesel-log odometer photos. Missing paperwork remains visible in Analytics.

This exception does **not** bypass the stop-type selection, signed-bill confirmation, final-odometer validation or storage errors.

The project team can set `OWNER_TEST_MODE` to `false` to restore these photo requirements. This setting alone does not make the prototype ready for operational use.

## Analytics

Open **Analytics** and enter the demonstration PIN: **`1234`**.

The PIN is included in the application code. It is a demonstration screen lock, **not secure authentication**.

Analytics provides date and driver filters, mileage, expense categories, estimated revenue and profit, delivery paperwork, and a CSV export that can be opened in Excel or Google Sheets.

The export contains record details and photo counts. **It does not include the photo files or provide a complete backup.** Download document photos separately.

### Calculation assumptions

- Projected revenue combines entered bill amounts and estimated extra waiting pay; it is not confirmed cash received.
- Estimated profit subtracts logged business expenses from projected revenue. Unlogged costs are absent.
- The current waiting-pay assumptions are **120 free minutes**, then **$75 per hour** for live unloads. These are placeholders pending VMR confirmation.
- The displayed **14-hour window** is a simplified prototype indicator, not a complete hours-of-service compliance system.

## Report a problem

1. Note the screen and the steps that caused the issue.
2. Record what you expected and what actually happened.
3. Open **Error log** at the bottom of the app, or use **Error details** in an alert.
4. Select **Copy all** and paste the log into a message to the project team or a GitHub Issue.
5. Include the app version, browser/device and a screenshot if useful. Review the contents before sharing publicly.

The log keeps up to 50 recent errors and includes browser information, timestamps and technical details. Reports are **not sent automatically**. Incorrect totals may need a manual report even when no automatic error is recorded.

If **Changes NOT saved** appears, keep the tab open and follow the alert. Use **Retry saving** when available. Do not assume the change is saved, and do not clear the site's browser data to troubleshoot.

## Suggested acceptance checks

- [ ] Start a day without a photo while test mode is enabled.
- [ ] Click **Complete delivery** before choosing a stop type; confirm the app explains what is missing.
- [ ] Choose a stop type and confirm the signed bill; complete the delivery without a photo.
- [ ] Upload a sample bill with multiple pages and verify its delivery association in Analytics.
- [ ] Enter a reference such as `001245` and verify it remains unchanged.
- [ ] Check that **End my day** is unavailable while a stop is open.
- [ ] Finish the stop and end the day with a valid final reading; check the mileage.
- [ ] Verify that a final reading below the starting reading is rejected.
- [ ] Open Analytics using the demo PIN and test date/driver filters and CSV export.
- [ ] Reload the website in the same browser and confirm saved records remain.
- [ ] Use **Error log → Make a test error** to verify the visible alert and copy function.

Code-level checks covered completion validation, optional-photo behavior, end-of-day saving, storage-failure handling and bill references. Those checks used a simulated page environment. Full browser and device testing remains outstanding.

## Current limitations and next steps

- No shared database, cross-device syncing, secure login or server-backed photo storage is connected.
- Browser storage has limited capacity, especially for photos. Clearing site data can remove records and images.
- P3 retains the local storage key `vmr-runlog-v2` for continuity. P2 and P3 hosted on the same origin can access the same stored records; separate repository paths do not isolate this data.
- Driver workflows are organized around the current local date. Overnight shifts and stops crossing midnight need further handling and testing.
- Accident reporting is a placeholder.
- GitHub Pages publishes the interface; publishing does not add the missing shared services.

Before real operational use, the project needs shared records and document storage, authentication and access controls, backups, confirmed business rules, and testing on the devices VMR will use.
