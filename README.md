# MikroTik Scripts

## Take Traffic Accounting Snapshot

`ssh alex@<host> "/ip accounting snapshot take"`

## Show Traffic Accounting

`ssh alex@<host> "/ip accounting snapshot print"`

## Pipes

### Sort Asc

`| sort -n -k 4`

### Upload + Amount (ungrouped)

`| awk '{print $2 "\t" $5}'`

### Download + Amount (ungrouped)

`| awk '{print $3 "\t" $5}'`

### Only local

`| grep <xxx.yyy.zzz>` (where xxx.yyy.zzz is the ip address "prefix")

### Group + Sum by Client

```awk
| awk '{
  arr[$1]+=$2
}
END {
for (key in arr) printf("%s\t%s\n", key, arr[key])
}'
```

## Full collection

```bash
ssh alex@<host> "/ip accounting snapshot take; /ip accounting snapshot print" | awk '{print $2 "\t" $5}' | grep 172.17.255 | awk '{                               
  arr[$1]+=$2
}
END {
for (key in arr) printf("%s\t%s\n", key, arr[key]/1024/8)
}' | sort -n -k 2
```
