# Exegol
 Exegol is a kali light base with a few useful additional tools and some basic configuration. It can be used in pentest engagements and BugBounty. Exegol's first use was to be a ready-to-hack docker in case of emergencies during engagements.
 
 ![Screenshot Empire/DeathStar/mitm6/Responder/ntlmrelayx](https://i.imgur.com/JMvtgYG.png)
 
# Tools
 The tools installed in Exegol are mostly installed from sources in order to have the latest version when deploying Exegol. Some of the tools can be found in a complete kali install though. Some installs are made with go, pip, apt, gem etc. The installs are not perfect but hey, it works!
 Some of the tools:
 - Responder (https://github.com/lgandx/Responder)
 - CrackMapExec (https://github.com/mpgn/CrackMapExec)
 - lsassy (https://github.com/Hackndo/lsassy)
 - sprayhound (https://github.com/Hackndo/sprayhound)
 - Impacket (https://github.com/SecureAuthCorp/impacket)
 - BloodHound.py (https://github.com/fox-it/BloodHound.py)
 - mitm6 (https://github.com/fox-it/mitm6)
 - dementor (https://gist.github.com/3xocyte/cfaf8a34f76569a8251bde65fe69dccc)
 - aclwpn (https://github.com/fox-it/aclpwn.py)
 - icebreaker (https://github.com/DanMcInerney/icebreaker)
 - Powershell Empire (https://github.com/BC-SECURITY/Empire)
 - DeathStar (https://github.com/byt3bl33d3r/DeathStar)
 - Sn1per (https://github.com/1N3/Sn1per)
 - ntlm-scanner (https://github.com/preempt/ntlm-scanner)
 - Sublist3r (https://github.com/aboul3la/Sublist3r)
 - ReconDog (https://github.com/s0md3v/ReconDog)
 - CloudFail (https://github.com/m0rtem/CloudFail)
 - OneForAll (https://github.com/shmilylty/OneForAll)
 - EyeWitness (https://github.com/FortyNorthSecurity/EyeWitness)
 - wafw00f (https://github.com/EnableSecurity/wafw00f)
 - JSParser (https://github.com/nahamsec/JSParser)
 - LinkFinder (https://github.com/GerbenJavado/LinkFinder)
 - SSRFmap (https://github.com/swisskyrepo/SSRFmap)
 - fuxploider (https://github.com/almandin/fuxploider)
 - CORScanner (https://github.com/chenjj/CORScanner)
 - Blazy (https://github.com/UltimateHackers/Blazy)
 - XSStrike (https://github.com/UltimateHackers/Blazy)
 - Bolt (https://github.com/s0md3v/Bolt)
 - subjack (https://github.com/haccer/subjack)
 - assetfinder (https://github.com/tomnomnom/assetfinder)
 - subfinder (https://github.com/projectdiscovery/subfinder/cmd/subfinder)
 - gobuster (https://github.com/OJ/gobuster)
 - amass (https://github.com/OWASP/Amass)
 - ffuf (https://github.com/ffuf/ffuf)
 - gitrob (https://github.com/michenriksen/gitrob)
 - shhgit (https://github.com/eth0izzle/shhgit)
 - waybackurls (https://github.com/tomnomnom/waybackurls)
 - subzy (https://github.com/lukasikic/subzy)
 - findomain (https://github.com/Edu4rdSHL/findomain)
 - timing attack (https://github.com/ffleming/timing_attack)
 - updog (https://github.com/sc0tfree/updog)

# Pre-requisites
 Docker is needed here if you want to run Exegol in a docker (intended). You can also use the `install.sh` in order to deploy Exegol elsewhere but I don't guarantee it'll work. (That being said I don't guarantee anything bro)
 
 Need a quick install of docker & docker-compose ? (intended for kali users but I guess it could work on any other Debian based system)
 ```
 sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 echo 'deb [arch=amd64] https://download.docker.com/linux/debian buster stable' | sudo tee /etc/apt/sources.list.d/docker.list
 sudo apt-get update
 sudo apt-get install -y docker-ce docker-ce-cli containerd.io
 sudo curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose
 sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
 sudo curl -L https://raw.githubusercontent.com/docker/compose/1.25.3/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
 sudo groupadd docker
 sudo usermod -aG docker $USER
 ```

# Install, run & stop
 The build can be long, build exegol before needing it.
 ```
 git clone https://github.com/ShutdownRepo/Exegol
 cd Exegol
 docker build --tag exegol .
 ```
 
 For the run, I use the option `--network=host` in order to inherit and share the host's IPv4/6 config, `--volume` in order to share a folder with the host and `--name=exegol` in order to get a shell later with `docker exec -it exegol zsh`.
 ```
 docker run --interactive --tty --detach --network host --volume /mnt/exegol:/share --name exegol exegol
 ```
 
 To get a shell (it is possible to pop multiple shells)
 ```
 docker exec -it exegol zsh
 ```
 
 To stop
 ```
 docker stop exegol && docker rm exegol
 ```

# Need a shortcut ?
 I personnaly use these aliases to go fast ([very fast](https://www.youtube.com/watch?v=KsBjVvxBj84))
  ```
  alias exegol-build='docker build --tag exegol /PATH/TO/Exegol/'
  alias exegol-run='docker run --interactive --tty --detach --network host --volume /PATH/TO/Exegol/shared-volume:/share --name exegol exegol'
  alias exegol-shell='docker exec -it exegol zsh'
  alias exegol-stop='docker stop exegol && docker rm exegol'
  ```
 
 # Credits & thanks
  Credits and thanks go to every infosec addicts that contribute and share but most specifically to my friends:
  - [@th1b4ud](https://twitter.com/th1b4ud) for the base ["Kali Linux in 3 seconds with Docker"](https://thibaud-robin.fr/articles/docker-kali/)
  - [@HackAndDo](https://twitter.com/HackAndDo) for [lsassy](https://github.com/Hackndo/lsassy), [sprayhound](https://github.com/Hackndo/sprayhound) and for being one of the greatest coworker that I've ever had
  - [@mpgn_x64](https://twitter.com/mpgn_x64) for your work on [CrackMapExec](https://github.com/mpgn/crackmapexec) in Python 3
