# Submit-Token-Funcaptcha
How to submit bypass token to HOTMAIL/OUTLOOK captcha?

## Run the browser with arguments 
```
--disable-web-security
--disable-site-isolation-trials
--disable-application-cache
```

#Get Token from any service (2captcha, dortcap...)

#Execute javascript below:
```
var anyCaptchaToken = 'INPUT_TOKEN_HERE';
var enc = document.getElementById('enforcementFrame');
var encWin = enc.contentWindow || enc;
var encDoc = enc.contentDocument || encWin.document;
let script = encDoc.createElement('SCRIPT');
script.append('function AnyCaptchaSubmit(token) { parent.postMessage(JSON.stringify({ eventId: "challenge-complete", payload: { sessionToken: token } }), "*") }');
encDoc.documentElement.appendChild(script);
encWin.AnyCaptchaSubmit(anyCaptchaToken);
```
