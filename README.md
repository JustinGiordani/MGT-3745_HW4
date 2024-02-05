# MGT-3745_HW4
description of HW #4 GAS code

 // CREATING A CUSTOM MENU MGT3745 //

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
