# Connect SMB using SMBClient

## Goal

Connect to shared SMB Folder

## Command

### Connect to SMB and get file
1. connect smb
```
smbclient --no-pass //*ip*/*shared-folder*
```
2. Get file (must be connected using step 1)
```
get *filename*
```

### Upload file

```
smbclient -N //*ip*/*shared-folder* -c 'put *local-file* *target-file*'
```