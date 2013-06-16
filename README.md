## ![eppz!tools](http://eppz.eu/layout/common/eppz_50_GitHub.png) reachability!bug
A proof project to reproduce Reachability bug when SCNetworkReachability callback function never get called when SCNetworkReachabilityRef was initialized with an address. You can easily switch wbetween the two implementation and see the error reproduced. The bottleneck code is the following.
```Objective-C
if (asynchronous) //The asynchronous way, NOT WORKS (!!!) with IP addresses as host.
{
    //Set callback, dispatch callbacks on a background thread.
    SCNetworkReachabilitySetCallback(reachabilityRef, reachabilityCallback, &context);
    SCNetworkReachabilitySetDispatchQueue(reachabilityRef, dispatch_queue_create("com.eppz.reachability", nil));
}
else //The synchronous way, works well with IP addresses as host.

{
    //Get flags.
    SCNetworkReachabilityFlags flags;
    if (SCNetworkReachabilityGetFlags(reachabilityRef, &flags))
        [self.statusView showReachabilityFlags:flags];
}
```
- - -
If you can explain me what is going on here, any comment is welcome on the corresponding blog post at [http://eppz.eu/blog/?p=260](http://eppz.eu/blog/?p=260).

#### License
> Licensed under the [Open Source MIT license](http://en.wikipedia.org/wiki/MIT_License).