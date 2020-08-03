## Welcome to Thanks

Thanks is a page where Igor and I can log a view messages of graditude we've left for each other.

<button name="button" onclick="window.open('https://forms.gle/A8oPMNc4kJKKskCt5')">Add Thanks</button>

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>

<script>
var JSONURL = 'https://spreadsheets.google.com/feeds/list/1iw-Evbc7GJPtSG-NmgWxT6iuaP2dG98LLOiJUAEdT7Y/1/public/basic?alt=json';

function callback(data){
    
    var cells = data.feed.entry;
    console.log(data);
    console.log(cells);
    
    var rows = [];
    var cells = data.feed.entry;

    for (var i = 0; i < cells.length; i++){
      var rowObj = {};
      rowObj.name = cells[i].title.$t;
      var rowCols = cells[i].content.$t.split(',');
      for (var j = 0; j < rowCols.length; j++){
        var keyVal = rowCols[j].split(':');
        rowObj[keyVal[0].trim()] = keyVal[1].trim();
      }
      rows.push(rowObj);
      var raw = document.createElement('p');
    	raw.innerText = JSON.stringify(rowObj.name + ' ' + rowObj.date + ' ' + rowObj.thanks);
    	document.body.appendChild(raw);
    }
}

$(document).ready(function(){
    
    $.ajax({
        url:JSONURL,
        success: function(data){
            callback(data);
        }
    });

});

</script>



