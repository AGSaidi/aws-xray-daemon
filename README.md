[![Build Status](https://travis-ci.org/aws/aws-xray-daemon.svg?branch=master)](https://travis-ci.org/aws/aws-xray-daemon)

# AWS X-Ray Daemon  

The AWS X-Ray daemon is a software application that listens for traffic on UDP port 2000, gathers raw segment data, and relays it to the AWS X-Ray API.   
The daemon works in conjunction with the AWS X-Ray SDKs and must be running so that data sent by the SDKs can reach the X-Ray service. For more information,
 see [AWS X-Ray Daemon](https://docs.aws.amazon.com/xray/latest/devguide/xray-daemon.html).

## Getting Help  

Use the following community resources for getting help with the AWS X-Ray Daemon. We use the GitHub issues for tracking bugs and feature requests.  

* Ask a question in the [AWS X-Ray Forum](https://forums.aws.amazon.com/forum.jspa?forumID=241&start=0).  
* Open a support ticket with [AWS Support](http://docs.aws.amazon.com/awssupport/latest/user/getting-started.html).  
* If you think you may have found a bug, open an [issue](https://github.com/aws/aws-xray-daemon/issues/new).  
* For contributing guidelines refer [CONTRIBUTING.md](https://github.com/aws/aws-xray-daemon/blob/master/CONTRIBUTING.md).

## Sending Segment Documents

The X-Ray SDK sends segment documents to the daemon to avoid making calls to AWS directly. You can send the segment/subsegment in JSON over UDP port 2000
to the X-Ray daemon, prepended by the daemon header : `{"format": "json", "version": 1}\n`

```
{"format": "json", "version": 1}\n{<serialized segment data>}
```  
For more details refer : [Link](https://docs.aws.amazon.com/xray/latest/devguide/xray-api-sendingdata.html)  

## Installing  

The AWS X-Ray Daemon is compatible with Go 1.7 and later.  

Install the daemon using the following command:  

```  
go get -u github.com/aws/aws-xray-daemon/...  
```  

You can also use [Glide](https://github.com/Masterminds/glide) to manage dependencies by using:   

```  
glide install  
```  
## Daemon Usage (command line args)  

Usage: X-Ray [options]   
1. -a  --resource-arn Amazon Resource Name (ARN) of the AWS resource running the daemon.    
2. -o  --local-mode   Don't check for EC2 instance metadata.    
3. -m  --buffer-memory    Change the amount of memory in MB that buffers can use (minimum 3).    
4. -n  --region   Send segments to the X-Ray service in a specific region.    
5. -b  --bind    Overrides default UDP address (127.0.0.1:2000).    
6. -r  --role-arn Assume the specified IAM role to upload segments to a different account.    
7. -c  --config   Load a configuration file from the specified path.    
8. -f  --log-file Output logs to the specified file path.    
9. -l  --log-level    Log level, from most verbose to least: dev, debug, info, warn, error, prod (default).    
10. -p --proxy-address  Proxy address through which to upload segments.
11. -v --version  Show AWS X-Ray daemon version.
12. -h --help    Show this screen

## Build  

`make build` would build binaries and .zip files in `/build` folder for Linux, MacOS, and Windows platforms.    

### Linux  

`make build-linux` would build binaries and .zip files in `/build` folder for the Linux platform.  

### MAC  

`make build-mac` would build binaries and .zip files in `/build` folder for the MacOS platform.  

### Windows  

`make build-windows` would build binaries and .zip files in `/build` folder for the Windows platform.  

## Testing  

`make test` will run unit tests for the X-Ray daemon.  

## License

This library is licensed under the Apache 2.0 License.
