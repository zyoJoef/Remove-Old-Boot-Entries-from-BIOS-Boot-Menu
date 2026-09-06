# Remove Old Boot Entries from BIOS Boot Menu

<h2>A quick story</h2>
<p>
  A few weeks ago I was fiddling around with multi-distro Linux installed on my external SSD 
  (namely: Ubuntu, Debian and Fedora), each of them is shared across with other distro on 
  the single SSD (multi-boot), which I tried out on my main and test laptop, 
  but it's for testing or experiment purpose only, so I reverted back to Windows 11. 
  The problem is, the old boot entries still shows up in the boot menu.
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



<h2>Before and After</h2>
<p><b>Before</b></p>
  <img width="1691" height="649" alt="797023060_1622964012881391_1634266387993063110_n" src="https://github.com/user-attachments/assets/cd5883ea-d455-42e6-a01d-da2ddadd8a62" />
<p><b>After</b></p>
  <img width="1730" height="655" alt="798414015_1602521284901019_56685634989817680_n" src="https://github.com/user-attachments/assets/71847a16-955e-4784-b67e-d3a81abfedb1" />



<hr>
<h2>Reference Used</h2>
  <a href="https://izzylaif.com/en/clear-up-bios-boot-menu-entries/">Clear up BIOS boot menu entries</a>
<br>
  <a href="https://www.youtube.com/watch?v=255ltqk7xDM">Remove old EFI entries from Boot Menu</a>
