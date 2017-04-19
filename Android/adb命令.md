# adb命令
---
## adb
```
tengxp@Harry-mac:~ $ adb -h
Android Debug Bridge version 1.0.35
Revision 102d0d1e73de-android

 -a                            - directs adb to listen on all interfaces for a connection
 -d                            - directs command to the only connected USB device
                                 returns an error if more than one USB device is present.
 -e                            - directs command to the only running emulator.
                                 returns an error if more than one emulator is running.
 -s <specific device>          - directs command to the device or emulator with the given
                                 serial number or qualifier. Overrides ANDROID_SERIAL
                                 environment variable.
 -p <product name or path>     - simple product name like 'sooner', or
                                 a relative/absolute path to a product
                                 out directory like 'out/target/product/sooner'.
                                 If -p is not specified, the ANDROID_PRODUCT_OUT
                                 environment variable is used, which must
                                 be an absolute path.
 -H                            - Name of adb server host (default: localhost)
 -P                            - Port of adb server (default: 5037)
 devices [-l]                  - list all connected devices
                                 ('-l' will also list device qualifiers)
 connect <host>[:<port>]       - connect to a device via TCP/IP
                                 Port 5555 is used by default if no port number is specified.
 disconnect [<host>[:<port>]]  - disconnect from a TCP/IP device.
                                 Port 5555 is used by default if no port number is specified.
                                 Using this command with no additional arguments
                                 will disconnect from all connected TCP/IP devices.

device commands:
  adb push <local>... <remote>
                               - copy files/dirs to device
  adb pull [-a] <remote>... <local>
                               - copy files/dirs from device
                                 (-a preserves file timestamp and mode)
  adb sync [ <directory> ]     - copy host->device only if changed
                                 (-l means list but don't copy)
  adb shell [-e escape] [-n] [-Tt] [-x] [command]
                               - run remote shell command (interactive shell if no command given)
                                 (-e: choose escape character, or "none"; default '~')
                                 (-n: don't read from stdin)
                                 (-T: disable PTY allocation)
                                 (-t: force PTY allocation)
                                 (-x: disable remote exit codes and stdout/stderr separation)
  adb emu <command>            - run emulator console command
  adb logcat [ <filter-spec> ] - View device log
  adb forward --list           - list all forward socket connections.
                                 the format is a list of lines with the following format:
                                    <serial> " " <local> " " <remote> "\n"
  adb forward <local> <remote> - forward socket connections
                                 forward specs are one of:
                                   tcp:<port>
                                   localabstract:<unix domain socket name>
                                   localreserved:<unix domain socket name>
                                   localfilesystem:<unix domain socket name>
                                   dev:<character device name>
                                   jdwp:<process pid> (remote only)
  adb forward --no-rebind <local> <remote>
                               - same as 'adb forward <local> <remote>' but fails
                                 if <local> is already forwarded
  adb forward --remove <local> - remove a specific forward socket connection
  adb forward --remove-all     - remove all forward socket connections
  adb reverse --list           - list all reverse socket connections from device
  adb reverse <remote> <local> - reverse socket connections
                                 reverse specs are one of:
                                   tcp:<port>
                                   localabstract:<unix domain socket name>
                                   localreserved:<unix domain socket name>
                                   localfilesystem:<unix domain socket name>
  adb reverse --no-rebind <remote> <local>
                               - same as 'adb reverse <remote> <local>' but fails
                                 if <remote> is already reversed.
  adb reverse --remove <remote>
                               - remove a specific reversed socket connection
  adb reverse --remove-all     - remove all reversed socket connections from device
  adb jdwp                     - list PIDs of processes hosting a JDWP transport
  adb install [-lrtsdg] <file>
                               - push this package file to the device and install it
                                 (-l: forward lock application)
                                 (-r: replace existing application)
                                 (-t: allow test packages)
                                 (-s: install application on sdcard)
                                 (-d: allow version code downgrade)
                                 (-g: grant all runtime permissions)
  adb install-multiple [-lrtsdpg] <file...>
                               - push this package file to the device and install it
                                 (-l: forward lock application)
                                 (-r: replace existing application)
                                 (-t: allow test packages)
                                 (-s: install application on sdcard)
                                 (-d: allow version code downgrade)
                                 (-p: partial application install)
                                 (-g: grant all runtime permissions)
  adb uninstall [-k] <package> - remove this app package from the device
                                 ('-k' means keep the data and cache directories)
  adb bugreport                - return all information from the device
                                 that should be included in a bug report.

  adb backup [-f <file>] [-apk|-noapk] [-obb|-noobb] [-shared|-noshared] [-all] [-system|-nosystem] [<packages...>]
                               - write an archive of the device's data to <file>.
                                 If no -f option is supplied then the data is written
                                 to "backup.ab" in the current directory.
                                 (-apk|-noapk enable/disable backup of the .apks themselves
                                    in the archive; the default is noapk.)
                                 (-obb|-noobb enable/disable backup of any installed apk expansion
                                    (aka .obb) files associated with each application; the default
                                    is noobb.)
                                 (-shared|-noshared enable/disable backup of the device's
                                    shared storage / SD card contents; the default is noshared.)
                                 (-all means to back up all installed applications)
                                 (-system|-nosystem toggles whether -all automatically includes
                                    system applications; the default is to include system apps)
                                 (<packages...> is the list of applications to be backed up.  If
                                    the -all or -shared flags are passed, then the package
                                    list is optional.  Applications explicitly given on the
                                    command line will be included even if -nosystem would
                                    ordinarily cause them to be omitted.)

  adb restore <file>           - restore device contents from the <file> backup archive

  adb disable-verity           - disable dm-verity checking on USERDEBUG builds
  adb enable-verity            - re-enable dm-verity checking on USERDEBUG builds
  adb keygen <file>            - generate adb public/private key. The private key is stored in <file>,
                                 and the public key is stored in <file>.pub. Any existing files
                                 are overwritten.
  adb help                     - show this help message
  adb version                  - show version num

scripting:
  adb wait-for[-<transport>]-<state>
                               - wait for device to be in the given state:
                                 device, recovery, sideload, or bootloader
                                 Transport is: usb, local or any [default=any]
  adb start-server             - ensure that there is a server running
  adb kill-server              - kill the server if it is running
  adb get-state                - prints: offline | bootloader | device
  adb get-serialno             - prints: <serial-number>
  adb get-devpath              - prints: <device-path>
  adb remount                  - remounts the /system, /vendor (if present) and /oem (if present) partitions on the device read-write
  adb reboot [bootloader|recovery]
                               - reboots the device, optionally into the bootloader or recovery program.
  adb reboot sideload          - reboots the device into the sideload mode in recovery program (adb root required).
  adb reboot sideload-auto-reboot
                               - reboots into the sideload mode, then reboots automatically after the sideload regardless of the result.
  adb sideload <file>          - sideloads the given package
  adb root                     - restarts the adbd daemon with root permissions
  adb unroot                   - restarts the adbd daemon without root permissions
  adb usb                      - restarts the adbd daemon listening on USB
  adb tcpip <port>             - restarts the adbd daemon listening on TCP on the specified port

networking:
  adb ppp <tty> [parameters]   - Run PPP over USB.
 Note: you should not automatically start a PPP connection.
 <tty> refers to the tty for PPP stream. Eg. dev:/dev/omap_csmi_tty1
 [parameters] - Eg. defaultroute debug dump local notty usepeerdns

adb sync notes: adb sync [ <directory> ]
  <localdir> can be interpreted in several ways:

  - If <directory> is not specified, /system, /vendor (if present), /oem (if present) and /data partitions will be updated.

  - If it is "system", "vendor", "oem" or "data", only the corresponding partition
    is updated.

environment variables:
  ADB_TRACE                    - Print debug information. A comma separated list of the following values
                                 1 or all, adb, sockets, packets, rwx, usb, sync, sysdeps, transport, jdwp
  ANDROID_SERIAL               - The serial number to connect to. -s takes priority over this if given.
  ANDROID_LOG_TAGS             - When used with the logcat option, only these debug tags are printed.
```

## logcat
```
tengxp@Harry-mac:~ $ adb logcat -help
logcat: invalid option -- h
Unrecognized Option
Usage: logcat [options] [filterspecs]
options include:
  -s              Set default filter to silent.
                  Like specifying filterspec '*:s'
  -f <filename>   Log to file. Default to stdout
  -r [<kbytes>]   Rotate log every kbytes. (16 if unspecified). Requires -f
  -n <count>      Sets max number of rotated logs to <count>, default 4
  -v <format>     Sets the log print format, where <format> is one of:

                  brief process tag thread raw time threadtime long

  -c              clear (flush) the entire log and exit
  -d              dump the log and then exit (don't block)
  -t <count>      print only the most recent <count> lines (implies -d)
  -t '<time>'     print most recent lines since specified time (implies -d)
  -T <count>      print only the most recent <count> lines (does not imply -d)
  -T '<time>'     print most recent lines since specified time (not imply -d)
                  count is pure numerical, time is 'MM-DD hh:mm:ss.mmm'
  -g              get the size of the log's ring buffer and exit
  -b <buffer>     Request alternate ring buffer, 'main', 'system', 'radio',
                  'events', 'crash' or 'all'. Multiple -b parameters are
                  allowed and results are interleaved. The default is
                  -b main -b system -b crash.
  -B              output the log in binary.
  -S              output statistics.
  -G <size>       set size of log ring buffer, may suffix with K or M.
  -p              print prune white and ~black list. Service is specified as
                  UID, UID/PID or /PID. Weighed for quicker pruning if prefix
                  with ~, otherwise weighed for longevity if unadorned. All
                  other pruning activity is oldest first. Special case ~!
                  represents an automatic quicker pruning for the noisiest
                  UID as determined by the current statistics.
  -P '<list> ...' set prune white and ~black list, using same format as
                  printed above. Must be quoted.

filterspecs are a series of
  <tag>[:priority]

where <tag> is a log component tag (or * for all) and priority is:
  V    Verbose
  D    Debug
  I    Info
  W    Warn
  E    Error
  F    Fatal
  S    Silent (supress all output)

'*' means '*:d' and <tag> by itself means <tag>:v

If not specified on the commandline, filterspec is set from ANDROID_LOG_TAGS.
If no filterspec is found, filter defaults to '*:I'

If not specified with -v, format is set from ANDROID_PRINTF_LOG
or defaults to "brief"
```

## am
``` sh
root@yama:/ # am -help
usage: am [subcommand] [options]
usage: am start [-D] [-W] [-P <FILE>] [--start-profiler <FILE>]
               [--sampling INTERVAL] [-R COUNT] [-S] [--opengl-trace]
               [--user <USER_ID> | current] <INTENT>
       am startservice [--user <USER_ID> | current] <INTENT>
       am stopservice [--user <USER_ID> | current] <INTENT>
       am force-stop [--user <USER_ID> | all | current] <PACKAGE>
       am kill [--user <USER_ID> | all | current] <PACKAGE>
       am kill-all
       am broadcast [--user <USER_ID> | all | current] <INTENT>
       am instrument [-r] [-e <NAME> <VALUE>] [-p <FILE>] [-w]
               [--user <USER_ID> | current]
               [--no-window-animation] [--abi <ABI>] <COMPONENT>
       am profile start [--user <USER_ID> current] <PROCESS> <FILE>
       am profile stop [--user <USER_ID> current] [<PROCESS>]
       am dumpheap [--user <USER_ID> current] [-n] <PROCESS> <FILE>
       am set-debug-app [-w] [--persistent] <PACKAGE>
       am clear-debug-app
       am monitor [--gdb <port>]
       am hang [--allow-restart]
       am restart
       am idle-maintenance
       am screen-compat [on|off] <PACKAGE>
       am to-uri [INTENT]
       am to-intent-uri [INTENT]
       am to-app-uri [INTENT]
       am switch-user <USER_ID>
       am start-user <USER_ID>
       am stop-user <USER_ID>
       am stack start <DISPLAY_ID> <INTENT>
       am stack movetask <TASK_ID> <STACK_ID> [true|false]
       am stack resize <STACK_ID> <LEFT,TOP,RIGHT,BOTTOM>
       am stack list
       am stack info <STACK_ID>
       am lock-task <TASK_ID>
       am lock-task stop
       am get-config

am start: start an Activity.  Options are:
    -D: enable debugging
    -W: wait for launch to complete
    --start-profiler <FILE>: start profiler and send results to <FILE>
    --sampling INTERVAL: use sample profiling with INTERVAL microseconds
        between samples (use with --start-profiler)
    -P <FILE>: like above, but profiling stops when app goes idle
    -R: repeat the activity launch <COUNT> times.  Prior to each repeat,
        the top activity will be finished.
    -S: force stop the target app before starting the activity
    --opengl-trace: enable tracing of OpenGL functions
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am startservice: start a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am stopservice: stop a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am force-stop: force stop everything associated with <PACKAGE>.
    --user <USER_ID> | all | current: Specify user to force stop;
        all users if not specified.

am kill: Kill all processes associated with <PACKAGE>.  Only kills.
  processes that are safe to kill -- that is, will not impact the user
  experience.
    --user <USER_ID> | all | current: Specify user whose processes to kill;
        all users if not specified.

am kill-all: Kill all background processes.

am broadcast: send a broadcast Intent.  Options are:
    --user <USER_ID> | all | current: Specify which user to send to; if not
        specified then send to all users.
    --receiver-permission <PERMISSION>: Require receiver to hold permission.

am instrument: start an Instrumentation.  Typically this target <COMPONENT>
  is the form <TEST_PACKAGE>/<RUNNER_CLASS>.  Options are:
    -r: print raw results (otherwise decode REPORT_KEY_STREAMRESULT).  Use with
        [-e perf true] to generate raw output for performance measurements.
    -e <NAME> <VALUE>: set argument <NAME> to <VALUE>.  For test runners a
        common form is [-e <testrunner_flag> <value>[,<value>...]].
    -p <FILE>: write profiling data to <FILE>
    -w: wait for instrumentation to finish before returning.  Required for
        test runners.
    --user <USER_ID> | current: Specify user instrumentation runs in;
        current user if not specified.
    --no-window-animation: turn off window animations while running.
    --abi <ABI>: Launch the instrumented process with the selected ABI.
        This assumes that the process supports the selected ABI.

am profile: start and stop profiler on a process.  The given <PROCESS> argument
  may be either a process name or pid.  Options are:
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to profile; uses current user if not specified.

am dumpheap: dump the heap of a process.  The given <PROCESS> argument may
  be either a process name or pid.  Options are:
    -n: dump native heap instead of managed heap
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to dump; uses current user if not specified.

am set-debug-app: set application <PACKAGE> to debug.  Options are:
    -w: wait for debugger when application starts
    --persistent: retain this value

am clear-debug-app: clear the previously set-debug-app.

am bug-report: request bug report generation; will launch UI
    when done to select where it should be delivered.

am monitor: start monitoring for crashes or ANRs.
    --gdb: start gdbserv on the given port at crash/ANR

am hang: hang the system.
    --allow-restart: allow watchdog to perform normal system restart

am restart: restart the user-space system.

am idle-maintenance: perform idle maintenance now.

am screen-compat: control screen compatibility mode of <PACKAGE>.

am to-uri: print the given Intent specification as a URI.

am to-intent-uri: print the given Intent specification as an intent: URI.

am to-app-uri: print the given Intent specification as an android-app: URI.

am switch-user: switch to put USER_ID in the foreground, starting
  execution of that user if it is currently stopped.

am start-user: start USER_ID in background if it is currently stopped,
  use switch-user if you want to start the user in foreground.

am stop-user: stop execution of USER_ID, not allowing it to run any
  code until a later explicit start or switch to it.

am stack start: start a new activity on <DISPLAY_ID> using <INTENT>.

am stack movetask: move <TASK_ID> from its current stack to the top (true) or   bottom (false) of <STACK_ID>.

am stack resize: change <STACK_ID> size and position to <LEFT,TOP,RIGHT,BOTTOM>.

am stack list: list all of the activity stacks and their sizes.

am stack info: display the information about activity stack <STACK_ID>.

am lock-task: bring <TASK_ID> to the front and don't allow other tasks to run

am get-config: retrieve the configuration and any recent configurations
  of the device

<INTENT> specifications include these flags and arguments:
    [-a <ACTION>] [-d <DATA_URI>] [-t <MIME_TYPE>]
    [-c <CATEGORY> [-c <CATEGORY>] ...]
    [-e|--es <EXTRA_KEY> <EXTRA_STRING_VALUE> ...]
    [--esn <EXTRA_KEY> ...]
    [--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE> ...]
    [--ei <EXTRA_KEY> <EXTRA_INT_VALUE> ...]
    [--el <EXTRA_KEY> <EXTRA_LONG_VALUE> ...]
    [--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE> ...]
    [--eu <EXTRA_KEY> <EXTRA_URI_VALUE> ...]
    [--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>]
    [--eia <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
    [--ela <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
    [--efa <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
    [--esa <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (to embed a comma into a string escape it using "\,")
    [-n <COMPONENT>] [-p <PACKAGE>] [-f <FLAGS>]
    [--grant-read-uri-permission] [--grant-write-uri-permission]
    [--grant-persistable-uri-permission] [--grant-prefix-uri-permission]
    [--debug-log-resolution] [--exclude-stopped-packages]
    [--include-stopped-packages]
    [--activity-brought-to-front] [--activity-clear-top]
    [--activity-clear-when-task-reset] [--activity-exclude-from-recents]
    [--activity-launched-from-history] [--activity-multiple-task]
    [--activity-no-animation] [--activity-no-history]
    [--activity-no-user-action] [--activity-previous-is-top]
    [--activity-reorder-to-front] [--activity-reset-task-if-needed]
    [--activity-single-top] [--activity-clear-task]
    [--activity-task-on-home]
    [--receiver-registered-only] [--receiver-replace-pending]
    [--selector]
    [<URI> | <PACKAGE> | <COMPONENT>]
```

## pm
```
root@yama:/ # pm -h
Error: unknown command '-h'
usage: pm list packages [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
       pm list permission-groups
       pm list permissions [-g] [-f] [-d] [-u] [GROUP]
       pm list instrumentation [-f] [TARGET-PACKAGE]
       pm list features
       pm list libraries
       pm list users
       pm path PACKAGE
       pm dump PACKAGE
       pm install [-lrtsfd] [-i PACKAGE] [PATH]
       pm install-create [-lrtsfdp] [-i PACKAGE] [-S BYTES]
       pm install-write [-S BYTES] SESSION_ID SPLIT_NAME [PATH]
       pm install-commit SESSION_ID
       pm install-abandon SESSION_ID
       pm uninstall [-k] [--user USER_ID] PACKAGE
       pm set-installer PACKAGE INSTALLER
       pm clear [--user USER_ID] PACKAGE
       pm enable [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable-user [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable-until-used [--user USER_ID] PACKAGE_OR_COMPONENT
       pm hide [--user USER_ID] PACKAGE_OR_COMPONENT
       pm unhide [--user USER_ID] PACKAGE_OR_COMPONENT
       pm grant PACKAGE PERMISSION
       pm revoke PACKAGE PERMISSION
       pm set-install-location [0/auto] [1/internal] [2/external]
       pm get-install-location
       pm set-permission-enforced PERMISSION [true|false]
       pm trim-caches DESIRED_FREE_SPACE
       pm create-user [--profileOf USER_ID] [--managed] USER_NAME
       pm remove-user USER_ID
       pm get-max-users

pm list packages: prints all packages, optionally only
  those whose package name contains the text in FILTER.  Options:
    -f: see their associated file.
    -d: filter to only show disbled packages.
    -e: filter to only show enabled packages.
    -s: filter to only show system packages.
    -3: filter to only show third party packages.
    -i: see the installer for the packages.
    -u: also include uninstalled packages.

pm list permission-groups: prints all known permission groups.

pm list permissions: prints all known permissions, optionally only
  those in GROUP.  Options:
    -g: organize by group.
    -f: print all information.
    -s: short summary.
    -d: only list dangerous permissions.
    -u: list only the permissions users will see.

pm list instrumentation: use to list all test packages; optionally
  supply <TARGET-PACKAGE> to list the test packages for a particular
  application.  Options:
    -f: list the .apk file for the test package.

pm list features: prints all features of the system.

pm list users: prints all users on the system.

pm path: print the path to the .apk of the given PACKAGE.

pm dump: print system state associated with the given PACKAGE.

pm install: install a single legacy package
pm install-create: create an install session
    -l: forward lock application
    -r: replace existing application
    -t: allow test packages
    -i: specify the installer package name
    -s: install application on sdcard
    -f: install application on internal flash
    -d: allow version code downgrade
    -p: partial application install
    -S: size in bytes of entire session

pm install-write: write a package into existing session; path may
  be '-' to read from stdin
    -S: size in bytes of package, required for stdin

pm install-commit: perform install of fully staged session
pm install-abandon: abandon session

pm set-installer: set installer package name

pm uninstall: removes a package from the system. Options:
    -k: keep the data and cache directories around after package removal.

pm clear: deletes all data associated with a package.

pm enable, disable, disable-user, disable-until-used: these commands
  change the enabled state of a given package or component (written
  as "package/class").

pm grant, revoke: these commands either grant or revoke permissions
  to applications.  Only optional permissions the application has
  declared can be granted or revoked.

pm get-install-location: returns the current install location.
    0 [auto]: Let system decide the best location
    1 [internal]: Install on internal device storage
    2 [external]: Install on external media

pm set-install-location: changes the default install location.
  NOTE: this is only intended for debugging; using this can cause
  applications to break and other undersireable behavior.
    0 [auto]: Let system decide the best location
    1 [internal]: Install on internal device storage
    2 [external]: Install on external media

pm trim-caches: trim cache files to reach the given free space.

pm create-user: create a new user with the given USER_NAME,
  printing the new user identifier of the user.

pm remove-user: remove the user with the given USER_IDENTIFIER,
  deleting all data associated with that user
```

