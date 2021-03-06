# xmlrpc_common.repy

This module helps to implement the client-side XML-RPC protocol. See http://en.wikipedia.org/wiki/XML-RPC for more details. 

A programmer may use this module to initiate a communication between the client (via a XML-RPC HTTP request). If the protocol is properly initiated, then the client will then return one or more values through XML, which can then by parsed by the [wiki:SeattleLib/xmlparse.repy] or manipulated at will.

Note that this module is primarily used by [wiki:SeattleLib/xmlrpc_client.repy], which programmers should include instead of this file. This file contains many functions which allow the XML-RPC protocol to be used in Python and is primary used to build the strings necessary to implement XML-RPC.

### Functions
```
def xmlrpc_common_call2xml(method_name, params):
```
    Build a XML-RPC method call to send to a XML-RPC server.

    Notes:

    * params is the sequence type of XML-RPC parameters. A dictionary may also be passed here, but the keys are ignored.
    * Returns the XML-RPC method call string.

```
def xmlrpc_common_response2xml(param):
```
    Build a XML-RPC method response to send to a XML-RPC client. This is the XML document that represents the return values or fault from a XML-RPC call.

    Notes:

    * param is the value that is returned (aka the response).
    * The XML-RPC method response string.

```
def xmlrpc_common_fault2xml(message, code):
```
    Build a XML-RPC fault response to send to a XML-RPC client. A fault response can occur from a server failure, an incorrectly generated XML request, or bad program arguments.

    Notes:

    * message is the string describing the fault.
    * code is the integer code associated with the fault.
    * Returns the XML-RPC fault response string.

```
def xmlrpc_common_call2python(xml):
```
    Convert a XML-RPC method call to its Python equivalent. The request from a XML-RPC client is parsed into native Python types so that the server may use the data to execute a method, as appropriate.

    Notes:

    * xml is the XML-RPC string to be convert.
    * Raises xmlrpc_common_XMLParseError on a XML-RPC structural parse error.
    * Raises xmlparse_XMLParseError on other XML parse errors.
    * Returns a tuple containing (1) the method name and (2) a list of the parameters.

```
def xmlrpc_common_response2python(xml):
```
    Convert a XML-RPC method response to its Python equivalent. The response from a XML-RPC server is parsed into native Python types so that the client may use the data as appropriate.

    Notes:
  
    * xml is the XML-RPC string to be convert.
    * Raises xmlrpc_common_XMLParseError on a XML-RPC structural parse error.
    * Raises xmlparse_XMLParseError on other XML parse errors.
    * Returns the method results or a xmlrpc_common_Fault on reading a fault.

### Example Usage

```
client = xmlrpc_client_Client("http://phpxmlrpc.sourceforge.net/server.php")
print client.send_request("examples.getStateName", (1,))
```

### Includes
[base64.repy](base64.repy.md)

[xmlparse.repy](xmlparse.repy.md)
