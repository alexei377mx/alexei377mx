# Ruby on Rails Installation Guide (Ubuntu/Debian)

## Table of Contents

1. [Installing Ruby on Rails](#1-installing-ruby-on-rails)
   - 1.1 [Install Ruby](#11-install-ruby)
   - 1.2 [Configure Git and SSH (GitHub)](#12-configure-git-and-ssh-github)
   - 1.3 [Install Rails](#13-install-rails)
   - 1.4 [Install Database](#14-install-database)
2. [Cloning the Project (if needed)](#2-cloning-the-project-if-needed)
   - 2.1 [Clone Project](#21-clone-project)
   - 2.2 [Check and Install Ruby Version](#22-check-and-install-ruby-version)
   - 2.3 [Verify Ruby Version](#23-verify-ruby-version)
   - 2.4 [Create PostgreSQL User](#24-create-postgresql-user)
   - 2.5 [Install Dependencies and Run the Application](#25-install-dependencies-and-run-the-application)
3. [Set Up Rails App](#3-set-up-rails-app)
   - 3.1 [Create a New Rails App](#31-create-a-new-rails-app)
   - 3.2 [Create PostgreSQL User](#32-create-postgresql-user)
   - 3.3 [Install Dependencies and Run the Application](#33-install-dependencies-and-run-the-application)

---
---

## 1. Installing Ruby on Rails

### 1.1 Install Ruby

**1.1.1 Update and Install Dependencies**

```bash
sudo apt update && sudo apt full-upgrade -y && sudo apt install -y git build-essential rustc libssl-dev libyaml-dev zlib1g-dev libgmp-dev
```

**1.1.2 Install Mise (Ruby Version Manager)**

```bash
sudo apt install -y curl && curl https://mise.run | sh && echo 'eval "$(~/.local/bin/mise activate)"' >> ~/.bashrc && source ~/.bashrc
```

**1.1.3 Install Ruby Version**

```bash
mise use --global ruby@latest
```

**1.1.4 Verify Ruby Installation**

```bash
ruby --version
```

**1.1.5 Update RubyGems**

```bash
gem update --system
```

---

### 1.2 Configure Git and SSH (GitHub)

**1.2.1 Git Config**

```bash
git config --global color.ui true && \
git config --global user.name "YOUR_NAME" && \
git config --global user.email "YOUR_EMAIL@example.com" && \
git config --global core.editor "code --wait"
```

**1.2.2 Generate SSH Key**

```bash
ssh-keygen -t ed25519 -C "YOUR_EMAIL@example.com" && cat ~/.ssh/id_ed25519.pub
```

**1.2.3 Add SSH Key to GitHub and Test Connection**

Add the key to: [https://github.com/settings/ssh](https://github.com/settings/ssh)

```bash
ssh -T git@github.com
# Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### 1.3 Install Rails

**1.3.1 Install Rails**

```bash
gem install rails
```

```bash
# check rails version
rails -v
```

---

### 1.4 Install Database

**PostgreSQL (recommended)**

```bash
sudo apt install postgresql libpq-dev -y
```

---
---

## 2. Cloning the Project (if needed)

### 2.1 Clone Project

```bash
git clone git@github.com:username/repository.git
```

```bash
cd repository
```

---

### 2.2 Check and Install Ruby Version

**2.2.1 Check Required Ruby Version**

```bash
cat .ruby-version
```

**2.2.2 Install the Required Ruby Version**

```bash
mise use ruby@3.2.2 # Local ruby on project
```

---

### 2.3 Verify Ruby Version

```bash
ruby --version
```

---

### 2.4 Create PostgreSQL user

(If it doesn’t exist)

```bash
sudo -u postgres createuser user --superuser --createdb --pwprompt
```

### 2.5 Install Dependencies and Run the Application

```bash
# Install project dependencies
bundle install
```

```bash
# Create the database
rails db:create
```

```bash
# Run database migrations
rails db:migrate
```

```bash
# Start the Rails server
rails server
```

---
---

## 3. Set Up Rails App

### 3.1 Create a New Rails App

```bash
rails new myapp -d postgresql
```

---

### 3.2 Create PostgreSQL user

(If it doesn’t exist)

```bash
sudo -u postgres createuser user --createdb --pwprompt
```

---

````md
---

### 3.3 Install Dependencies and Run the Application

```bash
# Install project dependencies
bundle install
```

```bash
# Create the database
rails db:create
```

```bash
# Run database migrations
rails db:migrate
```

```bash
# Start the Rails server
rails server
```



REMOVER BLOQUE 'system-test:' DE    ci.yml github
