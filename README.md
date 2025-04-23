# Di Google Apps Script, tambahkan fungsi doGet() seperti ini:

```javascript
function doGet() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Sheet1");
  const data = sheet.getDataRange().getValues();

  const headers = data[0];
  const records = data.slice(1).map(row => {
    let obj = {};
    headers.forEach((header, i) => obj[header] = row[i]);
    return obj;
  });

  return ContentService
    .createTextOutput(JSON.stringify(records))
    .setMimeType(ContentService.MimeType.JSON);
}
