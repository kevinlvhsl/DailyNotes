## cookie管理

```
/*cookie管理*/
var Cookie = {
    getExpiresDate:function(days, hours, minutes) {
        var ExpiresDate = new Date();
        if (typeof days == "number" && typeof hours == "number" &&
            typeof hours == "number") {
            ExpiresDate.setDate(ExpiresDate.getDate() + parseInt(days));
            ExpiresDate.setHours(ExpiresDate.getHours() + parseInt(hours));
            ExpiresDate.setMinutes(ExpiresDate.getMinutes() + parseInt(minutes));
            return ExpiresDate.toGMTString();
        }
    },
    _getValue:function(offset) {
        var endstr = document.cookie.indexOf (";", offset);
        if (endstr == -1) {
            endstr = document.cookie.length;
        }
        return unescape(document.cookie.substring(offset, endstr));
    },
    get:function(name) {
        var arg = name + "=";
        var alen = arg.length;
        var clen = document.cookie.length;
        var i = 0;
        while (i < clen) {
            var j = i + alen;
            if (document.cookie.substring(i, j) == arg) {
                return this._getValue(j);
            }
            i = document.cookie.indexOf(" ", i) + 1;
            if (i == 0) break;
        }
        return "";
    },
    set:function(name, value, expires, path, domain, secure) {
        document.cookie = name + "=" + escape (value) +
            ((expires) ? "; expires=" + expires : "") +
            ((path) ? "; path=" + path : "") +
            ((domain) ? "; domain=" + domain : "") +
            ((secure) ? "; secure" : "");
    },
    remove:function(name,path,domain) {
        if (this.get(name)) {
            document.cookie = name + "=" +
                ((path) ? "; path=" + path : "") +
                ((domain) ? "; domain=" + domain : "") +
                "; expires=Thu, 01-Jan-70 00:00:01 GMT";
        }
    },
    clear:function(){
        var cookies = document.cookie.split(';');
        for(var i=0; i < cookies.length; i++)
            var cookieName = cookies[i].split('=')[0];
            if(cookieName=='ProductListIds')
            {
                this.remove(cookieName);
            }
    }
};
```