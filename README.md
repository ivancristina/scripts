# Arduino port script

Arduino script to gain permission at `ttyUSB*` ports. Needed just the first time.

It solves the `avrdude: stk500_recv(): programmer is not responding` & `avrdude: stk500_getsync() attempt 10 of 10: not in sync: resp=0x00` errors.

The script works with the port `/dev/ttyUSB0`, if you need to use it for any other port, just replace it.

```
# Change USB* with any device you want to gain permission
echo "Listing all the /dev/ttyUSB* ports"
echo "(Make sure to edit the .sh if you want to list other ports, like /dev/ttyACM*)"
echo ""
ls -l /dev/ttyUSB*
echo ""

# You'll get something like this:
# crw-rw-rw- 1 root dialout 188, 0 mar 11 17:42 /dev/ttyUSB0

# Add the user to the group
sudo usermod -a -G dialout $USER
echo "$USER added to the group"
echo ""

# And chmod it (replace ttyUSB0 with the port you want to gain permission for)
sudo chmod a+rw /dev/ttyUSB0
echo "Port has now a+rw permission"
echo ""

echo "You need to logout and login in order for changes to take effect"
```
