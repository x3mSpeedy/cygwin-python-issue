# cygwin-python-issue
Demonstration of cygwin's Embedded Python error

## HOWTO

Tutorial for python version 2.7 (for version 3.4 replace all `"27"` with `"34"`). Issue is present in both version 2.7 and 3.4 where one dll file such as `time.dll` is imported but other dll `binascii.dll` which is in the same dir as `time.dll` yeilds import error.

### Under cygwin
1. run ` make all27`
2. copy out all dependencies (DLLs) to `output` folder, you can use `make ldd27` to find out what to copy
3. copy whole python2.7 folder from `/usr/lib/python2.7/` to `output` folder

### Under Windows
 1. run wrapper27.bat

### Conclusion
Result should differ:

Cygwin `./output/embedpy27`:
```bash
Python path: /usr/lib/python27.zip:/usr/lib/python2.7/:/usr/lib/python2.7/plat-cygwin:/usr/lib/python2.7/lib-tk:/usr/lib/python2.7/lib-old:/usr/lib/python2.7/lib-dynload
Python prefix: /usr
Python exec prefix: /usr
------------------
Python version
sys.version_info(major=2, minor=7, micro=10, releaselevel='final', serial=0)
------------------
Test: time module
(<module 'time' from '/usr/lib/python2.7/lib-dynload/time.dll'>, '/usr/lib/python2.7/lib-dynload/time.dll')
__doc__             This module provides various functi...
__file__            /usr/lib/python2.7/lib-dynload/time.dll
__name__            time
__package__         None
accept2dyear        1
altzone             -7200
asctime             <built-in function asctime>
clock               <built-in function clock>
ctime               <built-in function ctime>
daylight            1
gmtime              <built-in function gmtime>
localtime           <built-in function localtime>
mktime              <built-in function mktime>
sleep               <built-in function sleep>
strftime            <built-in function strftime>
strptime            <built-in function strptime>
struct_time         <type 'time.struct_time'>
time                <built-in function time>
timezone            -3600
tzname              ('CET', 'CEST')
tzset               <built-in function tzset>
------------------
Test: binascii module
(<module 'binascii' from '/usr/lib/python2.7/lib-dynload/binascii.dll'>, '/usr/lib/python2.7/lib-dynload/binascii.dll')
Error               <class 'binascii.Error'>
Incomplete          <class 'binascii.Incomplete'>
__doc__             Conversion between binary data and...
__file__            /usr/lib/python2.7/lib-dynload/binascii.dll
__name__            binascii
__package__         None
a2b_base64          <built-in function a2b_base64>
a2b_hex             <built-in function a2b_hex>
a2b_hqx             <built-in function a2b_hqx>
a2b_qp              <built-in function a2b_qp>
a2b_uu              <built-in function a2b_uu>
b2a_base64          <built-in function b2a_base64>
b2a_hex             <built-in function b2a_hex>
b2a_hqx             <built-in function b2a_hqx>
b2a_qp              <built-in function b2a_qp>
b2a_uu              <built-in function b2a_uu>
crc32               <built-in function crc32>
crc_hqx             <built-in function crc_hqx>
hexlify             <built-in function hexlify>
rlecode_hqx         <built-in function rlecode_hqx>
rledecode_hqx       <built-in function rledecode_hqx>
unhexlify           <built-in function unhexlify>

```

Windows `wrapper27.bat`:
```
Could not find platform independent libraries <prefix>
Could not find platform dependent libraries <exec_prefix>
Consider setting $PYTHONHOME to <prefix>[:<exec_prefix>]
Python path: output/python2.7:output/python2.7/lib-dynload:/usr/lib/python27.zip:/usr/lib/python2.7/:/usr/lib/python2.7/plat-cygwin:/usr/lib/python2.7/lib-tk:/usr/lib/python2.7/lib-old:/usr/lib/lib-dynload
Python prefix: /usr
Python exec prefix: /usr
------------------
Python version
sys.version_info(major=2, minor=7, micro=10, releaselevel='final', serial=0)
------------------
Test: time module
(<module 'time' from '/output/python2.7/lib-dynload/time.dll'>, '/output/python2.7/lib-dynload/time.dll')
__doc__             This module provides various functi...
__file__            /output/python2.7/lib-dynload/time.dll
__name__            time
__package__         None
accept2dyear        1
altzone             -7200
asctime             <built-in function asctime>
clock               <built-in function clock>
ctime               <built-in function ctime>
daylight            1
gmtime              <built-in function gmtime>
localtime           <built-in function localtime>
mktime              <built-in function mktime>
sleep               <built-in function sleep>
strftime            <built-in function strftime>
strptime            <built-in function strptime>
struct_time         <type 'time.struct_time'>
time                <built-in function time>
timezone            -3600
tzname              ('   ', '   ')
tzset               <built-in function tzset>
------------------
Test: binascii module
Traceback (most recent call last):
  File "<string>", line 2, in <module>
ImportError: No such file or directory
```
