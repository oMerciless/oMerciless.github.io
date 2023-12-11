# Developer bookmarklets
## A list of useful bookmarklets. Many of these are **NOT** mine. Credits will be listed underneath the "back to main" button.

### Search links bookmarklet. Creates a complied list of links on the current page containing specified text. (E.G. looking for links containing "blah.")

javascript:(function(){var x,n,nD,z,i; function htmlEscape(s){s=s.replace(/&/g,'&amp;');s=s.replace(/>/g,'&gt;');s=s.replace(/</g,'&lt;');return s;} function attrQuoteEscape(s){s=s.replace(/&/g,'&amp;'); s=s.replace(/"/g, '&quot;');return s;} x=prompt("show links with this word/phrase in link text or target url (leave blank to list all links):", ""); n=0; if(x!=null) { x=x.toLowerCase(); nD = window.open().document; nD.writeln('<html><head><title>Links containing "'+htmlEscape(x)+'"</title><base target="_blank"></head><body>'); nD.writeln('Links on <a href="'+attrQuoteEscape(location.href)+'">'+htmlEscape(location.href)+'</a><br> with link text or target url containing &quot;' + htmlEscape(x) + '&quot;<br><hr>'); z = document.links; for (i = 0; i < z.length; ++i) { if ((z[i].innerHTML && z[i].innerHTML.toLowerCase().indexOf(x) != -1) || z[i].href.toLowerCase().indexOf(x) != -1 ) { nD.writeln(++n + '. <a href="' + attrQuoteEscape(z[i].href) + '">' + (z[i].innerHTML || 
htmlEscape(z[i].href)) + '</a><br>'); } } nD.writeln('<hr></body></html>'); nD.close(); } })();

### Linked images bookmarklet. Basically opens a tab that shows all links to other pages that the current page has. Actually pretty useful.

javascript:(function(){var dims,dimarray,wid,hei,dimstring,x,i,z,url; function linkIsSafe(u) { if (u.substr(0,7)=='mailto:') return false; if (u.substr(0,11)=='javascript:') return false; return true; } function htmlEscape(s){s=s.replace(/&/g,'&amp;');s=s.replace(/>/g,'&gt;');s=s.replace(/</g,'&lt;');return s;} dims = prompt('width, height for each frame', '760, 500'); if (dims!=null) { dimarray = dims.split(','); wid = parseInt(dimarray[0]); hei = parseInt(dimarray[1]); dimstring = 'width='+wid+' height='+hei; x = document.links; z = window.open().document; for (i = 0; i < x.length; ++i) { url = x[i].href; if(linkIsSafe(url)) { z.writeln('<p>' + x[i].innerHTML + ' (' + htmlEscape(url) + ')<br><iframe ' + dimstring + ' src="' + url.replace(/"/g, '&quot;') + '">[broken iframe]</iframe></p>'); } } z.close(); } })();


<button style="background-color: darkgrey; padding: 10px 20px; color: black; border: 2px solid black;" onclick="window.location.href='https://omerciless.github.io'">Back to main </button>

Much thanks to https://www.squarefree.com/bookmarklets/ for many of the bookmarklets.
