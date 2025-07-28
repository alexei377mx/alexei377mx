# 1. Install Vue.js with Mise

## Table of Contents

1. [Set Up Vue.js Environment with Mise](#1-set-up-vuejs-environment-with-mise)
   - 1.1 [Update system and install basic dependencies](#11-update-system-and-install-basic-dependencies)
   - 1.2 [Install Mise (version manager)](#12-install-mise-version-manager)
   - 1.3 [Install Node.js with Mise](#13-install-nodejs-with-mise)
2. [Create Vue project with Vite](#2-create-vue-project-with-vite)

---
---

## 1. Set Up Vue.js Environment with Mise

### 1.1 Update system and install basic dependencies

```bash
sudo apt update && sudo apt -y full-upgrade && sudo apt install -y curl git
```

---

### 1.2 Install Mise (version manager)

```bash
sudo apt install -y curl && curl https://mise.run | sh && echo 'eval "$(~/.local/bin/mise activate)"' >> ~/.bashrc && source ~/.bashrc
```

Verify:

```bash
mise --version
```

---

### 1.3 Install Node.js with Mise

```bash
mise use --global node@lts
```

Verify:

```bash
node -v
```

```bash
npm -v
```

---

---

## 2. Create Vue project with Vite

```bash
npm create vite@latest my-vue-app
```

Select:

* Framework: **Vue**
* Variant: **JavaScript** or **TypeScript**
* Install dependencies and start now: **Yes** (recommended)
