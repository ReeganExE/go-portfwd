# portfwd

A simple port forwarder listener.

## Example

```go
// node executable path
nodePath := "node"
// the public port that you want to open
port := 8080

// It will listen on a random port, localhost:<random-port>
// Then it will start a node.js process to listen on *:8080
fowarder, e := portfwd.ListenAndForward(port, nodePath)
if e != nil {
  panic(e)
}

// `fowarder.Listener` is a listener on the random port
// start your server
if err := http.Serve(fowarder.Listener, nil); err != nil {
  panic(err)
}

```

## Why

On some machines, the firewall will block your go application for opening a public port.
To work-around on it, I found that Node.js (is a signed application) is allowed to open port.
So, this module will start a Node.js process then "proxy" the connection from the public port to your Go listener.