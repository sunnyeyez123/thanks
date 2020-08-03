## Welcome to Thanks

Thanks is a page where Igor and Jasmine can log and view messages of graditude they've left for each other.


<a href="#" class="myButton">green</a>

.myButton {
	box-shadow: 0px 10px 14px -7px #3dc21b;
	background:linear-gradient(to bottom, #44c767 5%, #5cbf2a 100%);
	background-color:#44c767;
	border-radius:4px;
	border:1px solid #18ab29;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:13px;
	font-weight:bold;
	padding:6px 12px;
	text-decoration:none;
	text-shadow:0px 1px 0px #2f6627;
}
.myButton:hover {
	background:linear-gradient(to bottom, #5cbf2a 5%, #44c767 100%);
	background-color:#5cbf2a;
}
.myButton:active {
	position:relative;
	top:1px;
}

<button name="button" onclick="window.open('https://forms.gle/A8oPMNc4kJKKskCt5')">Add Thanks</button>

<table id="thanksTable">
    <tr>
      <th>Timestamp</th>
      <th>Who do you want to thank?</th>
      <th>What are you thankful for?</th>
      <th>Who are you?</th>
    </tr>
</table>

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>

<script>
var JSONURL = 'https://spreadsheets.google.com/feeds/list/1iw-Evbc7GJPtSG-NmgWxT6iuaP2dG98LLOiJUAEdT7Y/1/public/basic?alt=json';

function callback(data){
    var cells = data.feed.entry;

    for (var i = 0; i < cells.length; i++){;
      var rowObj = {};
      rowObj.timestamp = cells[i].title.$t;
      var rowCols = cells[i].content.$t.split(',');
      for (var j = 0; j < rowCols.length; j++){
        var keyVal = rowCols[j].split(':');
        rowObj[keyVal[0].trim()] = keyVal[1].trim();
      }
      var row = '<tr>' +
      		  '<td>'+rowObj.timestamp+'</td>' +
                  '<td>'+rowObj.whodoyouwanttothank+'</td>' +
                  '<td>'+rowObj.whatareyouthankfulfor +'</td>' + 
                  '<td>'+rowObj.whoareyou +'</td>' + 
                '</tr>';
    	$('#thanksTable').append(row);
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



