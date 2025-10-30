# Project 6: Static Site Server with Nginx and rsync

This project involved setting up a live web server on an AWS EC2 instance (Ubuntu) to serve a static HTML/CSS website using Nginx.

Deployment is automated using `rsync` and a simple Bash script (`deploy.sh`).

---

## Live Site URL

**The static site is live at:** `http://16.171.90.89/`

---

## Steps Taken

1.  **Server Setup:** Launched a `t2.micro` Ubuntu EC2 instance on AWS.
2.  **Firewall Configuration:** Configured the AWS Security Group to allow:
    * `SSH` (Port 22) from my IP.
    * `HTTP` (Port 80) from anywhere.
3.  **SSH & Alias:** Set up an Elastic IP and configured an SSH alias (`aws-server`) in `~/.ssh/config` for easy login.
4.  **Nginx Installation:** Installed and configured Nginx (`sudo apt install nginx`).
5.  **Nginx Configuration:**
    * Created a new web root directory at `/var/www/my-static-site`.
    * Gave ownership to the `ubuntu` user (`sudo chown -R ubuntu:ubuntu /var/www/my-static-site`) to allow `rsync` to write files.
    * Edited `/etc/nginx/sites-available/default` to change the `root` directive to point to our new folder.
    * Restarted Nginx (`sudo systemctl restart nginx`).
6.  **Local Website:** Created a simple static site locally (`index.html`, `style.css`, `logo.png`) in the `my-static-site` folder.
7.  **`rsync` Deployment:** Wrote a `deploy.sh` script that uses `rsync -avz` to sync the local `my-static-site/` contents directly to the server's web root (`aws-server:/var/www/my-static-site/`).

## How to Deploy

To deploy any local changes to the website:

1.  Make changes to files inside the `my-static-site` folder.
2.  Run the deployment script:



    ```bash
    ./deploy.sh
    ```
