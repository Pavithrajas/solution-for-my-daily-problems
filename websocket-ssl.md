**Issue:**

Getting `ssl._create_default_https_context = ssl._create_unverified_context` error while trying to connect to web socket URL using (websocket.create_connection(url))

**Python Version:** 2.7.15

**OS:** Mac

**Stack Trace while getting issue:** 
```
File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/websocket/_core.py", line 511, in create_connection
    websock.connect(url, **options)
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/websocket/_core.py", line 220, in connect
    options.pop('socket', None))
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/websocket/_http.py", line 126, in connect
    sock = _ssl_socket(sock, options.sslopt, hostname)
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/websocket/_http.py", line 253, in _ssl_socket
    sock = _wrap_sni_socket(sock, sslopt, hostname, check_hostname)
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/websocket/_http.py", line 232, in _wrap_sni_socket
    server_hostname=hostname,
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/ssl.py", line 369, in wrap_socket
    _context=self)
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/ssl.py", line 617, in __init__
    self.do_handshake()
  File "/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/ssl.py", line 846, in do_handshake
    self._sslobj.do_handshake()
ssl.SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:726)
```

**Solution:** 
```
Go to:  /Applications/Python\ 2.7/
Click on: Install Certificates.command
```
It will open up terminal and you will get the following output: 
```
/Applications/Python\ 2.7/Install\ Certificates.command ; exit;
 -- pip install --upgrade certifi
Collecting certifi
  Downloading https://files.pythonhosted.org/packages/9f/e0/accfc1b56b57e9750eba272e24c4dddeac86852c2bebd1236674d7887e8a/certifi-2018.11.29-py2.py3-none-any.whl (154kB)
    100% |████████████████████████████████| 163kB 2.3MB/s 
Installing collected packages: certifi
  Found existing installation: certifi 2018.10.15
    Uninstalling certifi-2018.10.15:
      Successfully uninstalled certifi-2018.10.15
Successfully installed certifi-2018.11.29
 -- removing any existing file or link
 -- creating symlink to certifi certificate bundle
 -- setting permissions
 -- update complete

[Process completed]
```


**Issue:**

Getting `ssl.SSLError: [SSL: WRONG_VERSION_NUMBER] wrong version number (_ssl.c:997)` error while trying to connect to web socket URL using (websocket.create_connection(url)) for the private url (not hosted with any certificates) 

**Python Version:** 3.10

**OS:** Ubuntu (Docker) 

**Stack Trace while getting issue:** 

```
  File "/usr/local/lib/python3.10/dist-packages/websocket/_core.py", line 601, in create_connection
    websock.connect(url, **options)
  File "/usr/local/lib/python3.10/dist-packages/websocket/_core.py", line 244, in connect
    self.sock, addrs = connect(url, self.sock_opt, proxy_info(**options),
  File "/usr/local/lib/python3.10/dist-packages/websocket/_http.py", line 136, in connect
    sock = _ssl_socket(sock, options.sslopt, hostname)
  File "/usr/local/lib/python3.10/dist-packages/websocket/_http.py", line 272, in _ssl_socket
    sock = _wrap_sni_socket(sock, sslopt, hostname, check_hostname)
  File "/usr/local/lib/python3.10/dist-packages/websocket/_http.py", line 248, in _wrap_sni_socket
    return context.wrap_socket(
  File "/usr/lib/python3.10/ssl.py", line 512, in wrap_socket
    return self.sslsocket_class._create(
  File "/usr/lib/python3.10/ssl.py", line 1070, in _create
    self.do_handshake()
  File "/usr/lib/python3.10/ssl.py", line 1341, in do_handshake
    self._sslobj.do_handshake()
ssl.SSLError: [SSL: WRONG_VERSION_NUMBER] wrong version number (_ssl.c:997)
```

**Solution:** 
In this case, if we don't have the certficate for the URL for which we are trying to make connection using websocket, then check the URL and change it to connect via http only instead of https. 

For example: In my case, previously, the URL which we tried to connect is, `wss://abcd:8181/`. So changing this to `ws://abcd:8181/`, solved the problem. This will enable the non-secured connection. 

