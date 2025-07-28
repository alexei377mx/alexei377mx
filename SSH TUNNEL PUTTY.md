# To set up an SSH tunnel in PuTTY that forwards port 3000 on your local machine to port 3000 on a remote server:

1. **Open PuTTY**: Launch the PuTTY application on your computer.

2. **Configure the SSH connection**:

   * In the **"Host Name (or IP address)"** field, enter `user@server_ip`.

3. **Set up the tunnel**:

   * In the left panel, expand the **"SSH"** section and select **"Tunnels"**.
   * In **"Source port"**, enter `3000`.
   * In **"Destination"**, enter `localhost:3000`.
   * Select the **Local** and **Auto** radio buttons to indicate that this is a local tunnel.
   * Click **"Add"** to include the tunnel configuration in the list.

4. **Save the session (optional)**:

   * Go back to the **"Session"** category in the left panel.
   * In **"Saved Sessions"**, enter a name for this configuration.
   * Click **"Save"** to store the session for future use.

Once authenticated, the SSH tunnel will be active. Any connection you make to `localhost:3000` on your local machine will be forwarded to port `3000` on the remote server `192.168.1.73`.

---

# **To back up PuTTY settings (Windows):**

1. Open **Regedit**.

2. Navigate to:

   ```
   Computer\HKEY_CURRENT_USER\SOFTWARE\SimonTatham\PuTTY
   ```

3. Right-click the **PuTTY** folder → **Export**.

4. Save the file (e.g., `putty_backup.reg`).

To restore the settings, simply run the exported `.reg` file (e.g., `putty_backup.reg`).
