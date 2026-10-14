# Flask Web App

GitHub Actions 在推送到 `main` 时运行测试，并在配置好头歌服务器后通过 SSH 自动部署。页面返回 `Hello,NEU!`。

仓库地址：https://github.com/jokerzsd/flask-web-app

## 本地测试

```bash
python -m venv .venv
python -m pip install -r requirements.txt
python -m unittest discover -s tests -v
```

## 头歌服务器

应用由 Supervisor 管理，监听 5000 端口。首次部署需在服务器安装 Python、Git、Supervisor，克隆本仓库到 `/root/flask-web-app`，使用 `python3.8 -m venv .venv` 创建环境，并将 `deploy/flask-web-app.conf` 复制到 `/etc/supervisor/conf.d/`。随后执行 `supervisorctl reread`、`supervisorctl update`。

仓库 Actions Secrets：`TOUGE_SERVER_IP`、`TOUGE_SSH_PRIVATE_KEY`、`TOUGE_SSH_KNOWN_HOSTS`。部署准备完成后，将仓库变量 `TOUGE_DEPLOY_ENABLED` 设为 `true`，再运行工作流。SSH 私钥和服务器密码不要提交到仓库。
