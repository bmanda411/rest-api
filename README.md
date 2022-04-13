# rest-api
<!DOCTYPE html>
<html>
	<head>
		<title>PIJON</title>
		
		<script>
			function getPersonInfo(){
				var name = document.getElementById('name').value;
				
				var ajaxRequest = new XMLHttpRequest();
				ajaxRequest.onreadystatechange = function(){
					if(ajaxRequest.readyState == 4){
						if(ajaxRequest.status == 200){
							var person = JSON.parse(ajaxRequest.responseText);
							document.getElementById('birthYear').value = person.birthYear;
							document.getElementById('about').value = person.about;
						}
					}			
				}
				ajaxRequest.open('GET', 'http://localhost:8080/people/' + name);
				ajaxRequest.send();
			}
			
			function setPersonInfo(){
				var name = document.getElementById('name').value;
				var about = document.getElementById('about').value;
				var birthYear = document.getElementById('birthYear').value;
				
				var postData = 'name=' + name;
				postData += '&about=' + encodeURIComponent(about);
				postData += '&birthYear=' + birthYear;
				
				var ajaxRequest = new XMLHttpRequest();
				ajaxRequest.open('POST', 'http://localhost:8080/people/' + name);
				ajaxRequest.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
				ajaxRequest.send(postData);
			}
		</script>
	</head>
	<body>
		<h1>PIJON</h1>
		<p>(Person Info in JavaScript Object Notation)</p>
		<p><input type="text" value="Ada" id="name"><button type="button" onclick="getPersonInfo()">Get</button></p>
		<p>Birth year:</p>
		<input type="text" id="birthYear">
		<p>About:</p>
		<textarea id="about"></textarea>
		<p><button type="button" onclick="setPersonInfo()">Save</button></p>
	</body>
</html>
