# ppp - whith enhanced ifname
------------------------------------

This version of PPP is the original Debian PPP 2.4.7-2+4
which I've added the patch **ppp-2.4.7-ifname-enhanced.patch**
for more flexibility of the interface naming.

The problem: when I have multiple services in the system like 
**l2tp**, **pppoe client**, **pppoe server** or **pptp** for example 
I want to name those connection in different names, not only pppN.
This patch gets the configuration argument **ifname** and expands
the character N to the ppp index and keeping the remained small caps
as the prefix for the interface. 

Example: let's say we have a PPPoE ISP connection on the same machine
where we are running a PPPoE server session.

To have a clear differences between PPPoE ISP connection and 
PPPoE server sessions we can set in PPP options for PPPoE ISP:

```
ifname pppoeN
```

And in the PPPoE server PPP configuration file:

```
ifname pppoecN
```

When we fireup the ISP interface the system will show you:

```
20: pppoe0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1492 qdisc pfifo_fast state UNKNOWN qlen 100
    link/ppp 
    inet 89.A.B.C peer 81.X.Y.Z/32 scope global pppoe0
       valid_lft forever preferred_lft forever
```

And for the clients:
```
5472: pppoes1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1480 qdisc pfifo_fast state UNKNOWN qlen 100
    link/ppp 
    inet 10.245.245.1 peer 5.X.Y.Z/32 scope global pppoes1
       valid_lft forever preferred_lft forever
5483: pppoes3: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1480 qdisc pfifo_fast state UNKNOWN qlen 100
    link/ppp 
    inet 10.245.245.1 peer 5.X.Y.Z/32 scope global pppoes3
       valid_lft forever preferred_lft forever
```

Or like this:
```
42: pptp1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1480 qdisc pfifo_fast state UNKNOWN qlen 100
    link/ppp 
    inet 10.245.245.1 peer 5.X.Y.Z/32 scope global pptp1
       valid_lft forever preferred_lft forever
```
