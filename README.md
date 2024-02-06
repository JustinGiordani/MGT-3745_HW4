# Summary

First, a function is used to create the MGT3745 menu option in the spreadsheet toolbar (this is what will hold the filtered data). Next, the Google spreadsheet is called to iterate through each row and to filter out any bitcoin addresses with the frequency of "Seldom". Based on what filtered data is returned, the next chunk of code creates a sidebar for the filtered data to show. This sidebar is then filled with the filtered data so when the "MGT3745" tab in the toolbar is clicked, it will display all instances without a "Seldom" frequency.





```js

function onOpen() {
  
  var menu = document.createElement('div');
  menu.id = 'MGT3745';
  menu.innerText = 'MGT3745';
  menu.addEventListener('click', showFilteredData);

// ADDING THE MENU TO THE TOOLBAR 
  
  document.getElementById('toolbar').appendChild(menu);
}

// CALLING THE SPREADSHEET 

function showFilteredData() {
  var spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = spreadsheet.getActiveSheet();
  var data = sheet.getDataRange().getValues();

// FILTER ROWS BASED ON SELDOM FREQUENCY VALUE 
  
  var filteredData = data.filter(function(row) {
    return row[1].toString().toLowerCase() !== 'seldom';
  });

  // CREATE THE SIDEBAR FOR THE FILTERED DATA
  
  var sidebar = document.createElement('div');
  sidebar.style.fontFamily = 'Arial, sans-serif';
  sidebar.innerHTML = '<h2>Filtered Data</h2><table border="1"><tr><th>Bitcoin Address</th><th>Frequency</th></tr>' +
    filteredData.map(function(row) {
      return '<tr><td>' + row[0] + '</td><td>' + row[1] + '</td></tr>';
    }).join('') + '</table>';

  // APPENDING THE SIDEBAR WITH THE FILTERED DATA
  
  document.body.appendChild(sidebar);
}

```
