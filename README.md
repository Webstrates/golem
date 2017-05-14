# GOLEM


## Run the webstrates poxy

      $ docker run --name webstrates  -p 80:80 -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf:ro -d nginx

## Run a golem

      $ docker run -ti -p 9222:9222 -e "WEBSTRATEID=xxxxxx" --security-opt seccomp=${PWD}/chrome.json --name golem-xxxxxx --link webstrates webstrates/golem

## Basic-auth

Use e.g. a preconfigured proxy
https://wiki.apache.org/couchdb/Nginx_As_a_Reverse_Proxy

## Simplest case

        <body>
          <golem>
            // goes to a golem spawner which returns a script that is run partly in the browser, partly in the golem
            // the part in the browser simply uses the url to ensure a single golem is running for each webstrate
            // the part in the golem (guarded by a user-agent check) runs the actual golem code
            // User-agent check (headless chrome) 
            // Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome Safari/537.36
            <script src="golems.cs.au.dk/spawn" type="text/javascript"></script>
            <div id="counter">
            </div>
            <pre>
              var count = 0;
              setTimeout(1000, function() {
                document.querySelector("golem > #counter").innerText = count;
                count++;
              });
            </pre>
          </golem>
        </body>

## The golem soul

    <body>
      <golem id="golem.1">
        <pre class="package" type="application/json">
          {
            "name": "My golem"
          }
        </pre>
        <pre class="frontend" type="text/javascript">
          golem.on('message', function(msg) {

          });
        </pre>
        <pre class="backend" type="text/javascript">
        </pre>
