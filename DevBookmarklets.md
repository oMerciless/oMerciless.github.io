# Developer bookmarklets

## A list of useful bookmarklets. Many of these are **NOT** mine. Credits will be listed underneath the "back to main" button.

### Search links bookmarklet. Creates a complied list of links on the current page containing specified text. (E.G. looking for links containing "blah.")

javascript:(function(){var x,n,nD,z,i; function htmlEscape(s){s=s.replace(/&/g,'&amp;');s=s.replace(/>/g,'&gt;');s=s.replace(/</g,'&lt;');return s;} function attrQuoteEscape(s){s=s.replace(/&/g,'&amp;'); s=s.replace(/"/g, '&quot;');return s;} x=prompt("show links with this word/phrase in link text or target url (leave blank to list all links):", ""); n=0; if(x!=null) { x=x.toLowerCase(); nD = window.open().document; nD.writeln('<html><head><title>Links containing "'+htmlEscape(x)+'"</title><base target="_blank"></head><body>'); nD.writeln('Links on <a href="'+attrQuoteEscape(location.href)+'">'+htmlEscape(location.href)+'</a><br> with link text or target url containing &quot;' + htmlEscape(x) + '&quot;<br><hr>'); z = document.links; for (i = 0; i < z.length; ++i) { if ((z[i].innerHTML && z[i].innerHTML.toLowerCase().indexOf(x) != -1) || z[i].href.toLowerCase().indexOf(x) != -1 ) { nD.writeln(++n + '. <a href="' + attrQuoteEscape(z[i].href) + '">' + (z[i].innerHTML || 
htmlEscape(z[i].href)) + '</a><br>'); } } nD.writeln('<hr></body></html>'); nD.close(); } })();

### Linked images bookmarklet. Basically opens a tab that shows all links to other pages that the current page has. Actually pretty useful.

javascript:(function(){var dims,dimarray,wid,hei,dimstring,x,i,z,url; function linkIsSafe(u) { if (u.substr(0,7)=='mailto:') return false; if (u.substr(0,11)=='javascript:') return false; return true; } function htmlEscape(s){s=s.replace(/&/g,'&amp;');s=s.replace(/>/g,'&gt;');s=s.replace(/</g,'&lt;');return s;} dims = prompt('width, height for each frame', '760, 500'); if (dims!=null) { dimarray = dims.split(','); wid = parseInt(dimarray[0]); hei = parseInt(dimarray[1]); dimstring = 'width='+wid+' height='+hei; x = document.links; z = window.open().document; for (i = 0; i < x.length; ++i) { url = x[i].href; if(linkIsSafe(url)) { z.writeln('<p>' + x[i].innerHTML + ' (' + htmlEscape(url) + ')<br><iframe ' + dimstring + ' src="' + url.replace(/"/g, '&quot;') + '">[broken iframe]</iframe></p>'); } } z.close(); } })();

### Hide visited bookmarklet. Hides links you have already visited. For sites that use shortened links that all look the same, I guess.

javascript:(function(){var newSS, styles=':visited {display: none}'; if(document.createStyleSheet) { document.createStyleSheet("javascript:'"+styles+"'"); } else { newSS=document.createElement('link'); newSS.rel='stylesheet'; newSS.href='data:text/css,'+escape(styles); document.getElementsByTagName("head")[0].appendChild(newSS); } })();

### Link colour modifier bookmarklet. Makes internal links red, external links blue, and in-page links orange. Big help in my experience. 

javascript:(function(){var i,x; for (i=0;x=document.links[i];++i)x.style.color=["blue","red","orange"][sim(x,location)]; function sim(a,b) { if (a.hostname!=b.hostname) return 0; if (fixPath(a.pathname)!=fixPath(b.pathname) || a.search!=b.search) return 1; return 2; } function fixPath(p){ p = 
(p.charAt(0)=="/" ?%20%22%22%20:%20%22/%22)%20+%20p;/*many%20browsers*/%20p=p.split(%22?%22)[0];/*opera*/%20return%20p;%20}%20})()

### Open all links bookmarklet. Opens all links on a page. Use at your own risk. (It might blow up your computer if you are on a page with lots of links)

javascript:(function(){var n_to_open,dl,dll,i; function linkIsSafe(u) { if (u.substr(0,7)=='mailto:') return false; if (u.substr(0,11)=='javascript:') return false; return true; } n_to_open = 0; dl = document.links; dll = dl.length; for(i = 0; i < dll; ++i) { if (linkIsSafe(dl[i].href)) ++n_to_open; } if (!n_to_open) alert ('no links'); else { if (confirm('Open ' + n_to_open + ' links in new windows?%27))%20for%20(i%20=%200;%20i%20%3C%20dll;%20++i)%20if%20(linkIsSafe(dl[i].href))%20window.open(dl[i].href);%20}%20})();

### Open selected links bookmarklet. It's like the previous one, but only opens links you have selected. 

javascript:(function(){var n_to_open,dl,dll,i; function linkIsSafe(u) { if (u.substr(0,7)=='mailto:') return false; if (u.substr(0,11)=='javascript:') return false; return true; } n_to_open = 0; dl = document.links; dll = dl.length; if (window.getSelection && window.getSelection().containsNode) { /* mozilla */ for(i=0; i<dll; ++i) { if (window.getSelection().containsNode(dl[i], true) && linkIsSafe(dl[i].href)) ++n_to_open; } if (n_to_open && confirm('Open ' + n_to_open + ' selected links in new windows?%27))%20{%20for(i=0;%20i%3Cdll;%20++i)%20if%20(window.getSelection().containsNode(dl[i],%20true)%20&&%20linkIsSafe(dl[i].href))%20window.open(dl[i].href);%20}%20}%20/*%20/mozilla%20*/%20if%20(!n_to_open)%20{%20/*ie,%20or%20mozilla%20with%20no%20links%20selected:%20this%20section%20matches%20open_all_links,%20except%20for%20the%20alert%20text%20*/%20for(i%20=%200;%20i%20%3C%20dll;%20++i)%20{%20if%20(linkIsSafe(dl[i].href))%20++n_to_open;%20}%20if%20(!n_to_open)%20alert%20(%27no%20links%27);%20else%20{%20if%20(confirm(%27No%20links%20selected.%20%20Open%20%27%20+%20n_to_open%20+%20%27%20links%20in%20new%20windows?%27))%20for%20(i%20=%200;%20i%20%3C%20dll;%20++i)%20if%20(linkIsSafe(dl[i].href))%20window.open(dl[i].href);%20}%20}%20})();

### Full URL bookmarklet. Changes the text of hyperlinks to be their actual URL. Holy shit this one is useful. 

javascript:(function(){var i,c,x,h; for(i=0;x=document.links[i];++i) { h=x.href; x.title+=" " + x.innerHTML; while(c=x.firstChild)x.removeChild(c); x.appendChild(document.createTextNode(h)); } })()

### Full HREF bookmarklet. Changes text of hyperlinks to be their HTRF. It's essentially the full url bookmarklet.

javascript:(function(){var i,c,x,h; for(i=0;x=document.links[i];++i) { h=x.getAttribute("href"); x.title+=" " + x.innerHTML; while(c=x.firstChild)x.removeChild(c); x.appendChild(document.createTextNode(h)); } })()

### Remove redirects bookmarklet. It... well. It removes redirects. Also really useful.

javascript:(function(){var k,x,t,i,j,p; for(k=0;x=document.links[k];k++){t=x.href.replace(/[%]3A/ig,':').replace(/[%]2f/ig,'/');i=t.lastIndexOf('http');if(i>0){ t=t.substring(i); j=t.indexOf('&'); if(j>0)t=t.substring(0,j); p=/https?\:\/\/[^\s]*[^.,;%27%22%3E\s\)\]]/.exec(unescape(t));%20if(p)%20x.href=p[0];%20}%20else%20if%20(x.onmouseover&&x.onmouseout){x.onmouseover();%20if%20(window.status%20&&%20window.status.indexOf(%27://%27)!=-1)x.href=window.status;%20x.onmouseout();%20}%20x.onmouseover=null;%20x.onmouseout=null;%20}})();

### Target Page bookmarklet. Makes links open in the page you are in, instead of opening a new one. Useful for managment purposes.

javascript:(function(){var x,i; x=document.links; for(i=0;i<x.length;++i) { x[i].target="_self"; } })();


<button style="background-color: darkgrey; padding: 10px 20px; color: black; border: 2px solid black;" onclick="window.location.href='https://omerciless.github.io'">Back to main </button>

Much thanks to https://www.squarefree.com/bookmarklets/ for most of the bookmarklets.
