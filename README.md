# Resize the disk on EC2 without downtime

This is the procedure to resize a volume on EC2 instance without any downtime

*~take a snapshot of the volume for safety purpose ~*

### Pre-req :
- A running EC2 instance 


### Steps :
-  Check the current disk size and type using `df -hT` command

- Go to Volumes and **Modify Volume** , Increase the Volume size and Confirm it

Note : *Volumes can only be increased and cannot decreased*

- Check the Volume partitions using 

        lsblk

- Use the **growpart** command make the partion to take the available space

            growpart /dev/xvda 1

- Check the Volume partitions again using `lsblk`

-  use the `df -hT` command to see the Filesystem type and mount point

- Extend It using 

            #if FS is XFS
            sudo xfs_growfs -d /

            #if FS is Ext4
            resize2fs /dev/xvda1

- verify it using `df -hT` command


## Thanks & Reference
Link : https://www.youtube.com/watch?v=usOv-5_hzu0