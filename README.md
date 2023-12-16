# postBasedXSS
Demo/lab of some ways to practically exploit post based reflected XSS



Requirements:
flask


Install requirements with:
pip install -r requirements.txt

Run the server with:
python postXssServer.py


In your browser (preferably configured to proxy through Burp) navigate to:
http://localhost:80



Demos ways to exploit POST based reflected XSS
* Method Tampering
* CSRF
* Spoofed JSON CSRF Attack




@hoodoer

Drew.Kirkpatrick@TrustedSec.com


  
* [INPUT from 0xgreyhound] You can try to find a Open Redirect, create some HTML like this:

 <script>
    function redirectToURL() {
      window.location.href = ex "https://target.com/xxxxx/@javascript:prompt()";
    }
  </script>
  <form method="GET(?)" action="https://target.com">
   <button type="button" onclick="redirectToURL()">Click</button>
  </form>
  
  And serve it on your own machine and the JavaScript pseudo protocol should trigger the alert/prompt during the open redirect.

  Also if you happen to stumble up on a CSTI or Client-Side-Template-Injection, you can use XSS/JavaScript on steriods and doesnt matter if its POST or GET based :D

  Also you may be lucky if you send your POST request using burpsuite but leaves the POST body empty and instead uses the parameters in the URL as you woul with a  GET request, but thats very context dependendant and more     of a hyptotesis of mine, as i know sendingg .

Also like you already said using CSRF, more or less 50/50 POST based forms that dont have a CSRF token and are public, aswell as the ability to hosting your own website with malicious code that executes either when the victim loads the site or presses some button getting the victim to send his own POST based XSS payload without knowing it, even tho SameSite cookies can be a struggle if set to strict. Then theres always the Clickjacking option that still exists and is surprisingly wide spread and rarelly done anthing about, like the X-Frame-Options header. For example almost 99% of the bug bounty programs have Clickjacking OOS but i guess as the domain the victim visit aint the BBP owners domains, but they could still implement the correct protection against it, atleast some. Also there actually was a worm on Twitter using clickjacking i dont remember when but jeez it spread fast haha.

Also! Im sorry if i just wrote here in the README.ME(?) file i just read the "If you have issues or ideas how this can be improved, or better methods of triggering reflected POST based XSS vulnerabilities, my DMs are always open! @hoodoer." in your article and found this :D And woops sorry i missed DMs you can delete it as this is abit offtopic atleast first time im forking something? ;) And if you want to join any of our groups "DM" me ;)

