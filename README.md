# ejenkins
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Example](https://img.shields.io/badge/Examples-2ca5e0?style=flat&logo=appveyor)](https://github.com/ego-component/ejenkins/tree/master/examples)

## About
A Jenkins API Client implemented in Golang based on [Jenkins doc](https://www.jenkins.io/doc/book/using/remote-access-api/).

## Installation
```bash
go get github.com/ego-component/ejenkins
```

## Configuration
```toml
[jenkins]
addr = "http://127.0.0.1:8080" # your jenkins server address
username = "admin"
credential = "PasswordOrTokenGoesHere"
readtimeout = "2s" # timeout seconds for requesting jenkins api
debug = false # enable debug mode or not.
rawdebug = false # show raw request and response data during requesting api
```

## Usage
```go
// assume you have below toml configuration
var conf = `
[jenkins]
addr = "http://127.0.0.1:8080"
username = "admin"
credential = "PasswordOrTokenGoesHere"
`
// load configuration above
if err := econf.LoadFromReader(strings.NewReader(conf), toml.Unmarshal); err != nil {
    panic("LoadFromReader fail," + err.Error())
}

// init ejenkins component
jenkinsC := ejenkins.Load("jenkins").Build()

// Make calls against desired resources:
// get jenkins server basic info:
serverInfo, err := jenkinsC.Info()
// get a job
job, err := jenkinsC.GetJob("jobName", "...[parent folders]")
// invoke building process of a job
build, err := job.Invoke(payload, buildParams, securityToken)
```

## Examples 
See more examples in [here](examples/main.go)