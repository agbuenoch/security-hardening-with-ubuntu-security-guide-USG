# security-hardening-with-ubuntu-security-guide-USG

**Check out the [screenshots](screenshots) folder for all the screenshots.**

In the article [Installing Ubuntu Server 'Installer Image’ On VMware Workstation Pro](https://www.linkedin.com/pulse/installing-ubuntu-server-installer-image-vmware-workstation-agbu-pjidc), I walked through installing Ubuntu Server on VMware Workstation Pro. This article will guide you through the fundamental steps to secure the Ubuntu server before using it for log analysis, Wazuh management, or as a monitored endpoint.

The [Centre for Internet Security (CIS)](https://www.cisecurity.org/) benchmark has provided hundreds of configuration recommendations, but manually hardening and auditing a Linux system can be tedious and error-prone. 

[Ubuntu Security Guide (USG)](https://ubuntu.com/security/certifications/docs/usg) is a new and automated cybersecurity tool available with Ubuntu 20.04 LTS. It is part of [Ubuntu Pro Service](https://ubuntu.com/pro) and installed using the “Ubuntu Pro client.” With USG, hardening an Ubuntu system becomes much easier. USG is used to harden and audit Ubuntu systems to check if they are still compliant with the CIS Benchmark.

The Ubuntu Pro client is a tool designed to automate access to Ubuntu Pro services like Extended Security Maintenance (ESM), Ubuntu Security Guide (USG), Federal Information Processing Standards (FIPS), and more.

> **It is recommended to apply the security hardening on a freshly installed Ubuntu and not on a production system.**

> Pre-requisite:
  You must have or enable “Ubuntu Pro” as a prerequisite for using Ubuntu Security Guide (USG), this is because USG is one of the   
  services of “Ubuntu Pro”.

When you need help on how to install any command in Bash, and you have no idea how to do it, just type:
`<command name>`
or 
`<command name> --help`
Replace `<command name>` with the actual command you want to install. The terminal will provide you with the official/appropriate name and command to install it.

## Step 1: Register for Ubuntu Pro and attach it to your Ubuntu Server.
- Go to: https://ubuntu.com/pro/subscribe
- Sign in or create a free Ubuntu One account.
- Generate your free personal-use token (valid for up to 5 machines).
- Copy the token. This is used when attaching Ubuntu Pro to the Ubuntu server.

The above step has been explicitly explained in the article [Installing Ubuntu Server 'Installer Image’ on VMware Workstation Pro](https://www.linkedin.com/pulse/installing-ubuntu-server-installer-image-vmware-workstation-agbu-pjidc?).

## Step 2: Update and Upgrade Your System.
Run the green command to update and upgrade the Ubuntu server. As the arrow indicates, provide the Ubuntu server user password.<br>
**View: [step2A1](screenshots/step2A1.png)**

## Step 3: Install “Ubuntu Pro Client”.
The `Ubuntu Pro client` is a command-line utility (pro) that connects your Ubuntu machine to Ubuntu Pro services like Extended Security Maintenance (ESM), Compliance tools like `USG (Ubuntu Security Guide)`, `Federal Information Processing Standards (FIPS)` 140-2 certified cryptographic modules (for enterprise/government compliance), and more.

Run the command in green and provide the Ubuntu server user password when prompted, as pointed to by the 1st arrow. The 2nd, 3rd and 4th arrows point to the sequential steps for the installation of the Ubuntu Pro Client.<br>
**View: [step3A1](screenshots/step3A1.png)**

After it successfully installs the `pro` command-line tool. Let's verify/confirm that the `pro` command is installed in our terminal.

As pointed out by the 1st arrow, if the command is installed, the terminal will present you with the usage guide on how to use the command, and other vital information about the command as pointed to by the 2nd arrow.<br>
**View: [step3A2](screenshots/step3A2.png)**

## Step 4: Verify and view all Ubuntu Pro Services.
Let's view all the `Ubuntu Pro services` that `Ubuntu Pro clients` can access by running the command in green. As pointed to by the 1st arrow, the `esm-apps` service is enabled (This was done by completing `Step 1` above), which offers the Ubuntu system an extended 10+ years of security maintenance. The USG service is currently disabled as pointed to by the 2nd arrow. The 3rd arrow shows how to enable any of the Ubuntu Pro services, which can be achieved by using the Ubuntu Pro client (i.e pro command). This must be enabled so that we can use the service to perform an `audit` and `fix` our Ubuntu system following the CIS benchmark security. The 4th arrow points to the statement that we are using or subscribed to Ubuntu Pro on this Ubuntu system.<br>
**View: [step4A1](screenshots/step4A1.png)**

Ensure `esm` and `usg` are available or enabled.

## Step 5: Enable and install the USG Tool.
From the screenshot above, you can see that the `usg` Ubuntu Pro service is disabled as pointed to by the 2nd arrow. Let’s enable the `usg` service.

Run the command in green, and provide the Ubuntu server user password when prompted, as pointed to by the 1st arrow. The 2nd arrow points to the statement that confirms USG (Ubuntu Security Guide) is enabled.<br>
**View: [step5A1](screenshots/step5A1.png)**

This will enable the Ubuntu Security Guide (USG) utility. Checking the Ubuntu Pro Services again this time shows that the USG service is enabled as pointed to by the arrows below.<br>
**View: [step5A2](screenshots/step5A2.png)**

But I do not currently have the `usg` command installed yet on my Ubuntu server terminal, this will result in an error if you try to use the command.

Let’s first confirm if the “usg” command is NOT installed. As pointed to by the 1st arrow, the command is not found; meanwhile, the 2nd arrow points to the statement that provides the command to install the intended command, i.e usg.<br>
**View: [step5A3](screenshots/step5A3.png)**

Run the command in green to install the “usg” command. As pointed by the 1st arrow, provide the Ubuntu server password when prompted.<br>
**View: [step5A4](screenshots/step5A4.png)**

Let’s verify it is installed. As pointed by the 1st and 2nd arrow, the usage and additional information provided about the usg command imply that it is installed.<br>
**View: [step5A5](screenshots/step5A5.png)**

## Step 6: Audit Your Ubuntu Server Against CIS Benchmark.
Run the command in green to audit the Ubuntu server system against the CIS security benchmark. This process will take a couple of minutes to perform the system audit.

Each audit is presented as Title, Rule, and Result. The audit result for each rule will either be pass or fail, as shown below.<br>
**View: [step6A1](screenshots/step6A1.png)<br>**
**View: [step6A2](screenshots/step6A2.png)**

After it successfully performed the audit, the audit report can be found in the path I highlighted in yellow. Note also that the report is given in two formats, as `.html` and `.XML`, as pointed to by the 1st and 2nd arrow.<br>
**View: [step6A3](screenshots/step6A3.png)**

## Step 7: Access and open the Audit Report.
The `/var/lib/` directory is owned by system services, so most subfolders require sudo or completely switch to a `root user` for you to be able to access the subfolders in `/var/lib`, where the audit and fix reports are saved. 

Let's temporarily switch to a root user and navigate to the `/usg/` folder by running `cd /var/lib/usg/` to view our audit reports, which are highlighted in yellow and pink below. Type `exit` to switch back to a regular user at any time.

A regular user prompt is signified with a dollar sign `$` as pointed to by the 1st arrow. When we switch to a root user by running `sudo -i`, the prompt symbol changes to a hash sign `#` as pointed by the 3rd arrow. When we try to print the working directory `pwd`, you can see that it is `/root` as pointed by the 2nd arrow.<br>
**View: [step7A](screenshots/step7A.png)**

Alternatively, we can copy all the reports to the home directory for easier viewing without switching to the root user. We can then work with it later or copy the files from the home directory to our host machine. Since I am logged in as a root user, there is no need to use sudo in the command below.
```bash
cp /var/lib/usg/*.* ~/
```

The `*` means all file names with zero or more characters length, followed by a period `.`, and then all file extensions with zero or more characters length. This will copy all files that are in the `/var/lib/usg/` folder that satisfy the regular expression `*.*`

The `~/` means home directory (in my case, it is `/home/agbuenoch`).  Navigate to the home directory, and you will see all the files copied from the `/var/lib/usg/` directory in the home directory.

The 1st arrow points to the dollar sign `$`, implying we are currently operating as a regular user. Run `whoami` to print out the current username as pointed to by the 2nd arrow. The command `pwd` will print the current directory of the regular user, which is pointed to by the 3rd arrow.

The command `sudo -i` will switch the regular user to the root user as pointed to by the arrow immediately below the line where we run the sudo command. The hash symbol pointed to by the 4th arrow indicates we are now operating as the root user, and when you run `pwd`, it prints out that we are in the root directory, as pointed out by the 5th arrow. 

Still operating as the root user, we change the directory to `/var/lib/usg/`, and we run `ls -l` to print out all files and directories within the current directory `/var/lib/usg/`. The 6th arrow points to the files residing in the `/usg/` directory.

The command `cp ./*.* ~/` copied all the files `*.*` from the current directory `./` to the home directory `~/`. Run exit to log out the root user as pointed to by the 7th arrow, back to the regular user as pointed to by the 8th arrow, which now shows a dollar sign. At this point, we run whoami and pwd, and it prints the regular username `agbuenoch` and current directory `/home/agbuenoch` pointed by the 9th arrow, respectively.

Therefore, when we run `ls -l`, we can see the files we copied from `/var/lib/usg/` as the root user in the home directory as pointed to by the 10th arrow.<br>
**View: [step7B](screenshots/step7B.png)**

### Option A: How to view the .html file audit report.
Ubuntu Server is CLI-based; it does not have a GUI (Graphical User Interface) or a DISPLAY environment to launch GUI apps. To view the report, both files `.html` and `.xml` can be copied to the host machine (the computer running VMware) or to another Windows client virtual machine.

The two audit report files generated are pointed to by the 1st and 2nd arrows.<br>
**View: [step7C](screenshots/step7C.png)**

If you have a Windows Subsystem for Linux (WSL) running on a Windows client machine, with SSH installed and enabled, run the command below on your Ubuntu server terminal to copy the `.html` and `.xml` file report to the Windows client machine so you can view it in a browser.
```bash
sudo scp /ubuntu-server/path/to/filename <WSL-username>@<WSL-ip>:"/mnt/c/Users/windows-nameofuser/.../destination/"
```
**View: [step7D](screenshots/step7D.png)**

The article: [File Sharing using scp and rsync](https://www.linkedin.com/pulse/file-sharing-using-scp-rsync-enoch-agbu-yeynf) explains how to copy/share files between an Ubuntu server and a Windows client machine.

After running the command, you will be authenticated to provide the source system (Ubuntu server VM) user password as pointed to by the 1st arrow. You will also be authenticated against the Windows client machine (the destination system) you want to copy to, as pointed to by the 2nd arrow. The `.html` file was successfully copied to the Windows client machine as pointed to by the 3rd arrow and the 4th arrow, showing that the file was copied 100%.

Voila! The USG report file copied to the Windows client machine desktop is opened from the desktop as pointed to by the 1st arrow, using the Chrome browser.<br>
**View: [step7E](screenshots/step7E.png)**

Scroll through to view the security checks that passed and/or failed, including other security statistics. The 1st arrow points to the target system that was audited, and the 2nd arrow points to the username that performed the audit.<br>
**View: [step7F](screenshots/step7F.png)**

Scrolling further down is the compliance and scoring. The Ubuntu server failed to satisfy the conditions of 124 rules. 224 conditions rules were passed, and 124 failed, with a 70.87% pass rate as pointed by the 4th arrow. This report will be compared with the subsequent report generated after applying the CIS benchmark security.<br>
**View: [step7G](screenshots/step7G.png)**

## Option B: How to view the `.xml` file audit report.
The `.xml` file can be copied to and viewed on the host machine with any browser or code editor like `VS Code Studio` or `Sublime`. To copy the `.xml` file, run exactly the above command shown in the screenshot above, replacing the `.html` file name with the `.xml` file name.

Viewing the `.xml` file in VS Code.<br>
**View: [step7H](screenshots/step7H.png)**

You can view the `.xml` file right in the Ubuntu server terminal like any text file, although it may look unreadable/unorganised.

Scroll through the file neatly by using the “less” command, press `ENTER` to keep reading through each page, and press `CTRL+Z` to opt out of the reading.<br>
**View: [step7I](screenshots/step7I.png)**

After running the command above, below is a snippet of the `.xml` file contents.<br>
**View: [step7J](screenshots/step7J.png)**

## Step 8: Apply CIS Benchmark Fixes Automatically.
**`HIGHLY RECOMMENDED:`** Before applying the CIS benchmark security hardening, it's best to back up your virtual machine (VM) or take a snapshot. We will take a snapshot of the VM. While your Ubuntu server is running, follow the marked arrows sequentially to take a snapshot of the server. This is important because you can easily roll back to your Ubuntu server stable version/state in the event you break something or get stuck somewhere in your server.<br>
View: **[step8A](screenshots/step8A.png)**

Provide a snapshot name of your choice as pointed by the 1st arrow.<br>
**View: [step8B](screenshots/step8B.png)**

To revert to any of your snapshots, follow the sequence of the arrows below and click on the name of the snapshot you want to revert to. The 3rd arrow points to the name of a snapshot I created.<br>
**View: [step8C](screenshots/step8C.png)**

We have saved the current state of the freshly installed Ubuntu server using a snapshot. Let’s apply the security recommendations:

Run the command in green, and provide the Ubuntu server password as pointed to by the 1st arrow for authentication before the CIS benchmark is applied. Before the CIS benchmark security is fixed/applied, the system will always be audited first, as pointed out by the 2nd arrow. Each time you run the command to fix/apply the CIS benchmark, an audit must first be carried out. If you read along to the second line of the line pointed to by the 2nd arrow, you will see `--results` followed by a path; this is where the audit report will be saved.<br>
**View: [step8D](screenshots/step8D.png)**

The 1st arrow points to just a part of the audit carried out. After successfully auditing the system, the CIS benchmark will be applied. The 1st, 2nd and 3rd arrows point to the system files that will get executed to implement the CIS benchmark security. The 4th arrow points to the commencement of the fixing process, starting with the first one remediating rule `1/402` down until it remediates `402/402`.<br>
**View: [step8D2](screenshots/step8D2.png)**

The USG fix is done as pointed to by the 1st arrow.<br>

After remediating rule `402/402`, reboot the system to complete the process, as pointed to by the 2nd arrow. Perform another audit as pointed to by the 3rd arrow, after you have applied the CIS benchmark security. This will help to compare whether the security hardening has improved.

Run `sudo reboot` to reboot the server as shown in the screenshot below.<br>
**View: [step8D3](screenshots/step8D3.png)**

This fix process will: Harden SSH settings, configure file permissions, disable unnecessary services, apply password policies, and more. The Ubuntu server security is hardened and stricter now, as pointed out by the 1st arrow.<br>
**View: [step8D4](screenshots/step8D4.png)**

## Step 9: Re-audit After Reboot.
After reboot, rerun the audit, and compare the audit report with the previous report generated before applying the CIS benchmark security hardening:

Before running the audit, let's check and mark the audit report generated earlier, before we applied the CIS benchmark security above in `Step 8`. The 1st and 2nd arrows point to the audit report generated from the last audit we performed in `Step 6`. The other reports you see were generated when we ran the fix command to apply the CIS benchmark security. I have run the fix command multiple times, which is why you can see multiple reports there. Remember, each time we apply the CIS benchmark, an audit is first performed before the fix.<br>
**View: [step9A](screenshots/step9A.png)**

Run `sudo usg audit cis_level1_server` to check the compliance scores after we have fixed/applied the CIS benchmark security.

Currently, we are operating as the root user, as pointed to by the 1st arrow. Run exit to log out from the root user pointed to by the 2nd arrow. The 3rd arrow points to the dollar sign `$`, meaning a regular user.

After running the audit command, the 4th arrow points to the flag/option `--result`, meanwhile the 5th arrow points to the path/directory where the result is stored `/var/lib/usg/`, the `.xml` file is the file name containing the audit report.<br>
**View: [step9B](screenshots/step9B.png)**

Just as shown above, once the audit is complete, the 1st arrow points that the audit is complete and shows us where to find the audit report as pointed to by the 2nd and 3rd arrows.<br>
**View: [step9C](screenshots/step9C.png)**

To access the audit report, we need root user privileges. Run `sudo -i` to switch to the root user. We navigate to the `/var/lib/usg/` directory and `ls -l` out the path contents. The 1st and 2nd arrows point to the audit report (.html and .xml) just generated.<br>
**View: [step9D](screenshots/step9D.png)**

Run the command pointed to by the 1st arrow to copy the `.html` file pointed to by the 2nd arrow to the home directory so that we can access it anytime without root user privileges.<br>
**View: [step9E](screenshots/step9E.png)**

After we have successfully copied the file to the home directory. Let's copy the file to a Windows client machine so that we can view the .html file.

Using a different approach, from the Windows Subsystem for Linux (WSL) running on the Windows client machine, `SSH` into the Ubuntu server VM, and copy the `.html` file in the home directory to the Windows client machine desktop folder/path.

To remotely `SSH` connect to the Ubuntu server, run: 
```bash
ssh <Ubuntu-server-username>@<Ubuntu-server-ip>
```

You will be required to enter the remote machine (Ubuntu server VM) password to be able to connect to it. I have successfully remotely connected to the Ubuntu server, so I run `whoami` to print the Ubuntu server username as pointed out by 1st arrow, `pwd` to print the current directory as pointed out by 2nd arrow, and `ls -l` to list the directory contents as pointed out by 3rd arrow. The 4th arrow points to the command (spanning two lines) that will copy the `.html` file from the remote machine (Ubuntu server VM) home directory to the Windows client machine desktop path. You will provide the destination system (Windows client machine) password to authenticate you to copy to the machine, as pointed out by the 5th arrow. The 6th and 7th arrows point to the file successfully copied to the Windows client machine.<br>
**View: [step9F](screenshots/step9F.png)**

Let’s confirm that the compliance score has improved. Below is a snippet of the audit report before we applied the CIS benchmark security, with just a 70.87% success rate and 124 rule results failed.<br>
**View: [step9F2](screenshots/step9F2.png)**

Meanwhile, here is the audit report after applying the CIS benchmark security. There is a clear improvement compared to the initial report, where only 9 rule conditions failed.<br>
**View: [step9G](screenshots/step9G.png)**

The 1st arrow points to the target system audited, the 2nd arrow points to the username that performed the audit.<br>
**View: [step9H](screenshots/step9H.png)**

The post-hardening audit results show significantly improved CIS Level 1 Server Benchmark compliance, with only 9 rules, results that failed and a 92.24% success rate.<br>
**View: [step9I](screenshots/step9I.png)**

## LinkedIn Article.
- [Ubuntu Server Security Hardening with Ubuntu Security Guide (USG)]([https://www.linkedin.com/pulse/file-sharing-using-scp-rsync-enoch-agbu-yeynf/](https://www.linkedin.com/pulse/ubuntu-server-security-hardening-guide-usg-enoch-agbu-qdj3f?)

## Connect with me.
[🔗 LinkedIn](https://www.linkedin.com/in/agbuenoch)<br>
[🔗 X](https://www.x.com/agbuenoch)
