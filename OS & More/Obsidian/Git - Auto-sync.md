

# 🔐 Obsidian Git – SSH Setup (Linux Mint)

---

## 1️⃣ Install Git Plugin

Install the **Git** plugin:

```
obsidian://show-plugin?id=obsidian-git
```

---

## 2️⃣ Generate SSH Key (with passphrase)

```bash
ssh-keygen -t ed25519 -C "parsajfr1385oo@gmail.com"
```

- Press **Enter** to accept default path: `~/.ssh/id_ed25519`
    
- Set a passphrase

---

## 3️⃣ Start SSH Agent & Add the Key

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

## 4️⃣ Add Public Key to GitHub

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output →

GitHub → **Settings** →  
[SSH and GPG keys](https://github.com/settings/keys) →  
**New SSH key** → Paste → **Save**

---

## 5️⃣ Test SSH Connection

```bash
ssh -T git@github.com
```

- Type `yes` on first connect
    
- Expect a greeting with your username
    

---

## 6️⃣ Point Your Vault Repo to SSH

```bash
cd /path/to/your/obsidian/vault
```

Set `YOUR_USER` / `YOUR_REPO` accordingly:

```bash
git remote set-url origin git@github.com:YOUR_USER/YOUR_REPO.git
git remote -v
```

### Example

```bash
cd /home/reza/Documents/GitHub/obsidian-class

git remote set-url origin git@github.com:realpj10101/obsidian-class.git
git remote -v
```

---

## 7️⃣ Use in Obsidian

Open vault → **Obsidian Git** → Pull / Commit / Push

> You may unlock the key once per login session.
