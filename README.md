# AutoMautic
Bash script taking care of Mautic installation.
And then some more stuff...

#       _         _        __  __             _   _        ____   ____    ___
#      / \  _   _| |_ ___ |  \/  | __ _ _   _| |_(_) ___  | ___| |___ \  / _ \
#     / _ \| | | | __/ _ \| |\/| |/ _` | | | | __| |/ __| |___ \   __) || | | |
#    / ___ \ |_| | || (_) | |  | | (_| | |_| | |_| | (__   ___) | / __/ | |_| |
#   /_/   \_\__,_|\__\___/|_|  |_|\__,_|\__,_|\__|_|\___| |____(_)_____(_)___/
#
#                Fully Automatic Mautic installer with SSL cert.
#
# This Bash script is a one-command Mautic installer for people capable of launching a VPS
# and running some basic commands in it but without the need for actual Linux Knowledge requirements.
#
# This particular file is intended for documentation.
# There is an optimized verion of this dockerfile without comments.
# The production script is usually stripped of most comments, todo list, etc. but in this version
# for GitHub I keep (or add) very verbose comments and some extra sections.
#
# Intended uses:
# - A simple way to test Mautic with one single copy and paste command.
# - A live overview of Mautic requirements.
# - A starting point for Mautic code exploration and tinkering.
# - A way to learn about Bash Scripting.
#
# It is NOT meant as a production ready image.
#
# If you have any ideas how to make it clearer or simpler, please send me an email, submit a PR or an Issue.
# Also consider checking these other repos:
# KISSmauticDKR for a one-container, all-in-one Dockerfile, Docker Imagecontaining everything needed to run Mautic.
#
# While Ubuntu 24.04 is the only OS supported by this Script, you should be able to run it on other Debian-based distros.
#
# All the files for this dockerfile are on this GitHub repository:
# https://github.com/Martech-WorkShop/AutoMautic
#
#
#
#     This script installs the following components:
#
#      - Apache 2.4 http web server
#      - PHP 8.2 FPM with all the required packages
#      - Maria DB 11.4 LTS
#      - Mautic 5.1.1
#      - Snap daemon
#      - Certbot
#
#      It will also install an SSL cert and configure your Apache2 web server to use this certificate.



###--------------------------------###
###           To Do List           ###
###--------------------------------###

# TODO: Implement usage statistics
#   Option 1: Use ssmtp to send install statistics.
#   Option 2: Create an API endpoint and send data via curl.
#
# TODO:  Improve MySQL root password generation and handling
#   Current method: MYSQL_PASSWORD=\$(cat /dev/urandom | tr -dc '...' | head -c32)
#   Improvements:
#       a) Allow user to type a password.
#       b) Allow user to generate a random pasword.
#       c) Automatically use a robust random password generator (e.g., openssl rand).
#
#   In all cases:
#       - Store the generated password securely (e.g., in a temporary file or environment variable).
#       - Avoid using the root MySQL user directly for Mautic; create a dedicated user with limited privileges.
#
# TODO: Investigate and handle kernel version-related reboot issue
#   Problem: Script sometimes prompts for a reboot due to kernel version changes.
#   Solution:  Determine the exact conditions causing the reboot prompt and implement appropriate handling (e.g., conditional reboot, restarting specific services instead of the entire system).
#
# ToDo: Add user imput for the email to be used for the Let's Encrypt notifications.
#
# ToDo: Send email containing the installation information.
# Ask the user if he wants to be sent an email witht hat information.
# Ask the user if he wants to be notified of new versions.
# Ask the user if he wants to subscribe to the newsletter.


 #info: Switch to mpm prefork for package libapache2-mod-php8.2
 #Module mpm_event disabled.
 #Enabling module mpm_prefork.
 #info: Executing deferred 'a2enmod php8.2' for package libapache2-mod-php8.2

 #Processing triggers for libc-bin (2.39-0ubuntu8.3) ...
 #Scalar found where operator expected (Missing operator before "$nrconf"?) at (eval 12) line 237, near "'a'
 #$nrconf"
 #Error parsing /etc/needrestart/needrestart.conf: syntax error at (eval 12) line 237, near "'a'
 #$nrconf"
 #Execution of (eval 12) aborted due to compilation errors.


 #mysql: Deprecated program name. It will be removed in a future release, use '/usr/bin/mariadb' instead
 #mysql: Deprecated program name. It will be removed in a future release, use '/usr/bin/mariadb' instead
 #mysql: Deprecated program name. It will be removed in a future release, use '/usr/bin/mariadb' instead


 ### Get files from toolBelt.

 #wget https://files.mktg.dev/pub/install-mautic/m5-tuto-basic.conf.txt -O /etc/apache2/sites-available/000-default.conf
 #todo: Change this to the proper AutoMautic directory #wget https://mauteam.org/wp-content/uploads/2019/10/000-default.txt -O /etc/apache2/sites-available/000-default.conf
 # Link does not exist: wget https://files.mktg.dev/pub/instal-mautic/mautic5-cron-jobs.txt -O /tmp/cron-jobs.txt
 #wget https://files.mktg.dev/pub/AutoMautic/m9cronjobs.txt -O /tmp/cron-jobs.txt
 #crontab /tmp/cron-jobs.txt
 #rm /tmp/cron-jobs.txt


