Non HCX Migration

## Prerequesites
Ubuntu VM (fully loaded)
NSX Network on both domains
May need local VM on Console

## Cold Migration
Power off VM
Remove from Datastore
Copy local
upload to other datastore

## Cross vCenter vMotion
Initiate vMoton from mgmt domain, move to WLD (or vice versa)

## L2VPN
May want to do this first