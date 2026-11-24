# Step #1: Install and Configure Suricata

**Install Suricata on the Ubuntu Desktop VM.**

<img
src="screenshots/01.png"
style="width:6.5in;height:4.65278in" />

**Identify the correct network interface and configure it in
/etc/suricata/suricata.yaml. Set the correct NIC.**

<img
src="screenshots/02.png"
style="width:6.5in;height:4.72222in" />

<img
src="screenshots/03.png"
style="width:6.5in;height:4.75in" />

# Step #2: Create Custom Suricata Rules

**Run the command to create a new rule file named myCustom.rules within
the rules directory you set up in the previous step.**

<img
src="screenshots/04.png"
style="width:6.75in;height:0.23958in" />

**Add the following rule to detect ICMP Echo request. This also helps to
confirm Suricata is working. Also save changes and exit nano editor.**

<img
src="screenshots/05.png"
style="width:7.05729in;height:1.09543in" />

**Modify the rule-files section in /etc/suricata/suricata.yaml file.**

<img
src="screenshots/06.png"
style="width:6.37778in;height:0.25109in" />

<img
src="screenshots/07.png"
style="width:6.5in;height:1.03159in" />

**Run the command to validate Suricata configuration**

<img
src="screenshots/08.png"
style="width:6.64583in;height:0.67078in" />

**Enable Suricata to Start automatically and verify that Suricata is
running**

<img
src="screenshots/09.png"
style="width:5.16667in;height:0.44573in" />

# Step #3: Monitor Alerts

**From Kali, ping Ubuntu**

<img
src="screenshots/10.png"
style="width:5.23438in;height:2.68429in" />

**Check the Suricata Logs**

<img
src="screenshots/11.png"
style="width:7.04311in;height:0.33031in" />

# Step #4: Write 3 Custom Suricata Rules

<img
src="screenshots/12.png"
style="width:7.38021in;height:1.00935in" />

# Step #5: Simulate and Validate Alerts Locally

**From Kali Linux, generate test traffic that matches your chosen
rules.**

**TCP SYN Scan:**

<img
src="screenshots/13.png"
style="width:6.5in;height:1.98611in" />

**SSH Brute Force:**

<img
src="screenshots/14.png"
style="width:7.40104in;height:1.32708in" />

**FTP Login:**

<img
src="screenshots/15.png"
style="width:5.54167in;height:1.01042in" />

**Observe and confirm alerts**

<img
src="screenshots/16.png"
style="width:7.41146in;height:0.70585in" />

## Documentation Table

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<tbody>
<tr>
<td><p><strong>#</strong></p></td>
<td><p><strong>Rule Goal</strong></p></td>
<td><p><strong>SID</strong></p></td>
<td><p><strong>Test Command</strong></p></td>
<td><p><strong>Detected</strong></p></td>
<td><p><strong>Short Analysis</strong></p></td>
</tr>
<tr>
<td><p>1</p></td>
<td><p>ICMP</p></td>
<td><p>1000001</p></td>
<td><p>ping -c 4 192.168.121.24</p></td>
<td><p>Yes</p></td>
<td><p>Suricata was able to match it on the ICMP protocol to the
subnet.</p></td>
</tr>
<tr>
<td><p>2</p></td>
<td><p>TCP SYN</p></td>
<td><p>1000002</p></td>
<td><p>sudo nmap -sS -T4 192.168.121.24</p></td>
<td><p>Yes</p></td>
<td><p>The threshold correctly flagged the SYN packets from the Nmap
scan as port-scanning behaviour.</p></td>
</tr>
<tr>
<td><p>3</p></td>
<td><p>SSH</p></td>
<td><p>1000003</p></td>
<td><p>sudo gunzip /usr/share/wordlists/rockyou.txt.gz # only if it's
still .gz</p>
<p>hydra -l student -P /usr/share/wordlists/rockyou.txt
ssh://192.168.121.24 -t 4</p></td>
<td><p>Yes</p></td>
<td><p>Hydra exceeded the 5-attempts-in-60-seconds threshold.</p></td>
</tr>
<tr>
<td><p>4</p></td>
<td><p>FTP</p></td>
<td><p>1000004</p></td>
<td><p>printf "USER student\r\n" | nc 192.168.121.24 21</p></td>
<td><p>Yes</p></td>
<td><p>The alert fired on the “USER” content match because vsftpd was
active and listening on port 21.</p></td>
</tr>
</tbody>
</table>
