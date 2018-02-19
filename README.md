<!DOCTYPE html>
<html>
    <head>
	<style>
      #map {
        height: 800px;
        width: 100%;
       }
    </style>
    <script type="text/javascript">

 //the file text data
 var text;
 var i;
 var num;  //number of rows inthe textfile
 var len;  //length of the textfile
 var csvdat;
 var x;
 var y;
 var point;
 var path
 var linedat;
 var map;
 var lines;
 var centerpoint;
 var markerpoint;
 var startpoint;
 function initMap()
	 {
	 
		centerpoint =new google.maps.LatLng(25.240041,55.36606)
	    var zm=16;
		map = new google.maps.Map(document.getElementById('map'), {
		
          zoom: zm,
          center: centerpoint,
		  
        });
		
		lines = new google.maps.Polyline({
				
				//geodesic: true,
				strokeColor: '#FF0000',
				strokeOpacity: 1.0,
				strokeWeight: 2
				});
			lines.setMap(map);
			
		var marker1 = new google.maps.Marker({
          position: markerpoint,
          map: map
        });
     }	  
 
 //start reading the textfile
 var openFile = function(event)
     {
        var input = event.target;

        var reader = new FileReader();
        reader.onload = function()
		 {
          text = reader.result;
		  text = text.replace(/\r/g, '');
		  linedat = text.split(/\n/g);
		  linedat = linedat.filter(Boolean);
		  //document.write(linedat);
		  //document.write("<br>");
		  len = linedat.length;  
		  
		  csvdat = linedat[0].split(",");
		  x = parseFloat(csvdat[3]);
		  y = parseFloat(csvdat[4]);
		  
		  
		  startpoint = new google.maps.LatLng(x,y);
		 
		  
		  for(i=0;i<len;i++)
			{
					
			csvdat = linedat[i].split(",");
			
			x = parseFloat(csvdat[3]);
			
			y = parseFloat(csvdat[4]);
			
			if ((!isNaN(csvdat[3]))&&(!isNaN(csvdat[4]))) {
			//document.write(csvdat[3]);
			//document.write(csvdat[4]);
			point=new google.maps.LatLng(x,y);
			//document.write(point);
			path = lines.getPath();
			path.push(point);
			//document.write(path);
			}	
		    
		   }
		   markerpoint = new google.maps.LatLng(x,y);
		   
		   //centerpoint = new google.maps.LatLng(x,y);
		   //map.panTo(centerpoint);
		   
		   var marker1 = new google.maps.Marker({
		   position: markerpoint,
		   map: map
		   });
		   
		   var bound = new google.maps.LatLngBounds(markerpoint,startpoint);
		   map.fitBounds(bound);
		  
		   };
		   		
				
		 //for printing the outpu
		 reader.readAsText(input.files[0]);
	  };	 
  </script>
 </head>
   <body>
    <input type='file' accept='text/plain' onchange='openFile(event)'><br>
	 <div id="map"></div>
	 <script async defer
    src="https://maps.googleapis.com/maps/api/js?key=AIzaSyA1VMJrkw2K8qgbPXQGheDYn9C80aLMMUQ&callback=initMap">
    </script>
   </body>
   </html>










