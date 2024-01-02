# Use-RESTCONF-with-Cisco-IOS-XE-Software

## Use GET to Access Resources with a Browser
1. Select the URL window, and enter the URL: https://csr1kv/restconf/. To send the request, press Enter.
2. In the editor window, the base RESTCONF GET URL is now displayed. Review the XML document

Another way to send requests is to use Visual Studio Code directly. Open Terminal by clicking on the terminal icon.

1. open the folder the files is placed.
2. using terminal. when you already in the folder run
```
code .
```
it will open visual studio. you can edit here.
3. create new file example : 
```
restconf.http
```
4. In the editor window, enter the following lines:
```
GET https://csr1kv/restconf
Authorization: Basic cisco:cisco
```
5. send the request by clicking on the Send Request link above the method and URL or by pressing Ctrl-Alt-R (Cmd-Alt-R for macOS). The response will be shown in a parallel window.
6. you can use other exampple:
```
https://csr1kv/restconf/data/Cisco-IOS-XE-native:native
```
```
https://csr1kv/restconf/data/Cisco-IOS-XE-native:native/interface
```
```
https://csr1kv/restconf/data/Cisco-IOS-XE-native:native/interface/GigabitEthernet=1
```
```
https://csr1kv/restconf/data/Cisco-IOS-XE-native:native/interface/GigabitEthernet=1?fields=name
```

## Use the Python Requests Library to Get Resources such as XML and JSON

1. create new file. called
```
restconf.http
```
2. In the editor window, enter the following lines:
```
GET https://csr1kv/restconf/data/Cisco-IOS-XE-native:native/interface
Authorization: Basic cisco:cisco
```
3. Generate a python script to communicate with the device.
After you prepare a request, use the shortcut Ctrl-Alt-C (Cmd-Alt-C for macOS), or right-click in the editor and click Generate Code Snippet in the menu. It will pop up the language pick list and library list.

4. In the drop-down list, press the Requests HTTP library option. A new tab will be opened and populated with the generated code.
5. Create a new file. Name it xe_restconf_get.py. Select the generated code in the right window and copy it to the clipboard (Ctrl+C).
6. below is the codes.
```
import requests
url = " https://csr1kv/restconf/data/Cisco-IOS-XE-native:native/interface"
headers = {
    'user-agent': "vscode-restclient",
    'authorization': "Basic cisco:cisco"
    }
response = requests.request("GET", url, headers=headers)
print(response.text)
```
This code will retrieve the same information about the resource interfaces that you already saw in the previous steps. The response data will be in the XML format, which is the default format.

The main parts of the code are as follows:

  1. The code imports the request library so that it can be used in the code.
  2. The definition of the URL is provided.
  3. The definition of auth is provided, using HTTP basic authentication.
  4. The send request to the resource is requests.request(…).
  5. The type of the request is specified explicitly: “GET”
  6. The last line prints the response to the standard output.

7. Run the code by using the play button (triangle).
8. Fix the certificate verification.
```
response = requests.request("GET", url, headers=headers, verify=False)
```
9. Fix the authentication problem and execute the script.
```
from requests.auth import HTTPBasicAuth
auth = HTTPBasicAuth('cisco', 'cisco')


response = requests.request("GET", url, headers=headers, verify=False, auth=auth)
```
10. Configure the request to receive a JSON formatted response.
```
headers = {
'Accept': 'application/yang-data+json'
}
```

FOR THE REST WE CAN JUST CRETE SIMILIAR CODE BUT WITH DIFFERENT FUNCTION LIKE POST PATCH DELETE ETC
