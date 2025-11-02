```markdown
# System Health Report Generator

This is a simple Bash script that generates a quick HTML-based **system health report** and serves it using **nginx**. It checks memory and disk usage, formats them nicely into an HTML table, and makes the report accessible via your local nginx server.

The idea is to have an easy, zero-fuss way to visualize system stats right in your browser.

---

## Features

- Checks for required dependencies (`docker`, `df`, `free`, `nginx`) before running  
- Automatically enables and starts the `nginx` service  
- Generates a styled HTML report with:
  - Current timestamp  
  - Memory usage (via `free -h`)  
  - Disk usage (via `df -h`)  
- Places the report in nginx’s web root (`/usr/share/nginx/html`)  
- Accessible at:  
```

[http://localhost](http://localhost)

````

---

## Requirements

This script is meant for **Linux systems** (tested on Arch and Ubuntu).  
Make sure you have `systemctl` and a working `sudo` user.

### Dependencies

The script uses the following tools:
- `docker`
- `df` (coreutils)
- `free` (procps-ng)
- `nginx`
- `systemctl`

You can install them with your package manager:

**Arch Linux:**
```bash
sudo pacman -S docker coreutils procps-ng nginx
````

**Ubuntu/Debian:**

```bash
sudo apt update
sudo apt install docker.io coreutils procps nginx -y
```

---

## Usage

1. **Clone the repo:**

   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```

2. **Make the script executable:**

   ```bash
   chmod +x healthreport.sh
   ```

3. **Run the script with a sudo user:**

   ```bash
   sudo ./healthreport.sh
   ```

   The script will:

   * Check for dependencies
   * Enable and start nginx
   * Generate the HTML report
   * Move it to `/usr/share/nginx/html/healthreport.html`

4. **View the report:**
   Open your browser and go to:

   ```
   http://localhost/healthreport.html
   ```

---

## Troubleshooting

* If nginx fails to start, check:

  ```bash
  sudo systemctl status nginx
  sudo journalctl -xeu nginx
  ```
* If you get permission errors moving files to `/usr/share/nginx/html`, make sure you’re running the script with `sudo`.
* For port conflicts, edit `/etc/nginx/nginx.conf` and change:

  ```
  listen 80;
  ```

  to another port like `8080`.

Then restart nginx:

```bash
sudo systemctl restart nginx
```

---

## Notes

* The report is generated each time you run the script, overwriting the old one.
* `docker` is checked for installation but not actually used yet — you can extend this script later to include container metrics.
* This is a quick, no-dependencies HTML generator — it doesn’t rely on Python, PHP, or any server-side frameworks.

---

## License

MIT License. Do whatever you want with it. Just don’t blame me if you blow up your nginx config.

```
```
