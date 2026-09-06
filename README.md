# Remove Old Boot Entries from BIOS Boot Menu

<h2>A quick story</h2>
<p>
  A few weeks ago I was fiddling around with a bunch of Linux distro
  installed on my external SSD (namely: Ubuntu, Debian and Fedora), 
  each of the distro's partition is shared across with other distro on the single SSD (multi-boot),
  which I tried out on my main and test laptop, but it's for testing or experiment purpose only, 
  so I reverted back to Windows 11. The problem is, the old boot entries still shows up in the boot menu.
</p>

<h2>Why it happens?</h2>
<p>
  Old boot menu entries still show up because they are stored in the motherboard's 
  non-volatile NVRAM (firmware memory, not on your hard drive. When you delete an 
  operating system or format a drive, the files are removed, but the motherboard's 
  pointer to those files remains saved in the system memory.
</p>

<h2>What should we do?</h2>
<p>
  In the case of Windows 10/11, we'll be using the utility <b>bcedit.exe</b>
</p>

<ol>
  <li>Run Command Prompt as administrator
  <li>Run the command:
    <pre><code>bcdedit /enum firmware</code></pre>
  </li>
It will show you a list of all entries in the BCD store. 
  <li>Export the list
    <pre><code>bcdedit /export newbcd</code></pre>
  </li>
  <li>Make a backup copy just in case
    <pre><code>copy newbcd bcdbackup</code></pre>
  </li>
  <li>Copy and paste the ID/s of the unused entries, then delete them one by one with this command
    <pre><code>bcdedit /store newbcd /delete {INSERT ENTRY ID}</code></pre>
  </li>
  </li>
  <li>Once removed, save the file using this command
    <pre><code>bcdedit /import newbcd /clean</code></pre>
  </li>
</ol>

<hr>
<h2>Reference Used</h2>
<a href="https://izzylaif.com/en/clear-up-bios-boot-menu-entries/">Clear up BIOS boot menu entries</a>
<br>
<a href="https://www.youtube.com/watch?v=255ltqk7xDM">Remove old EFI entries from Boot Menu</a>
