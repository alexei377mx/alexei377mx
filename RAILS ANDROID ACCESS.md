# Access Your Rails App (on Linux) from Android or iOS

> These steps work on **Ubuntu**, **Linux Mint**, **Debian**, **Fedora**, **Arch**, and most other Linux distributions. 
They also apply if you’re accessing your Rails app from an **iPhone** ,**iPad** or **Android**.

## Step 1: Make Rails Listen on Your Local IP

By default, Rails only listens on `localhost`, so you need to change that:

```bash
rails server -b 0.0.0.0 -p 3000
```

This makes Rails listen on **all network interfaces**, not just `localhost`.

## Step 2: Find Your PC’s Local IP Address

On Linux (any distro), open a terminal and run:

```bash
ip a
```

Or, if you prefer a shorter command:

```bash
hostname -I
```

Look for your **WiFi** or **Ethernet** IP, e.g.:

```
192.168.1.10
```

## Step 3: Connect Your Mobile Device to the Same WiFi

Make sure your **Android** or **iPhone/iPad** is connected to the **same local network** as your PC.

## Step 4: Access from Mobile Browser

Open a browser on your Android (Chrome) or iPhone (Safari) and go to:

```
http://192.168.1.10:3000
```

(Replace `192.168.1.10` with your actual computer’s IP.)
