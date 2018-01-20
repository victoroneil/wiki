Lua RTOS include a port of the well-known [dropbear](https://matt.ucc.asn.au/dropbear/dropbear.html) SSH server. This allow to establish secure shell connections to any Lua RTOS device, with minimal RAM requirements.

Notes about the dropbear port:

  * Only 1 client connection is allowed.
  * Only the root user is allowed.
  * The server keys are created on the fly the first time that dropbear are starts.
  * SCP transfers are not supported by now.
  * Remote SSH command execution are not supported by now.

How to use:

1. Set your's device root password:

   ```lua
   /> os.pass()
   ```

   or (if shell is enabled in your device)

   ```lua
   /> passwd
   ```

2. Initiate a network as usual (wifi or ethernet), and get your device's ip address:

   ```lua
   /> net.eth.setup(.....)
   /> net.eth.start()
   ```

   ```lua
   /> net.stat()
   ```

   or (if shell is enabled in your device)

   ```lua
   /> netstat
   ```

3. Start the ssh server:

   ```lua
   /> net.service.ssh.start()
   ```

4. From you desktop computer connect to your device through a ssh client:

   ```lua
   $ ssh root@device-ip
   ```