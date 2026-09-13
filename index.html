import customtkinter as ctk
import json
import os
import requests
import subprocess
import shutil
import threading
from cryptography.fernet import Fernet
from tkinter import filedialog

# === CONFIGURAÇÃO VISUAL IOXEU (ALTO CONTRASTE & ACESSÍVEL) ===
ctk.set_appearance_mode("Dark")
ctk.set_default_color_theme("green")

CORES = {
    "bg": "#050505", "card": "#121212", "neon": "#00FF41",
    "text": "#FFFFFF", "dim": "#AAAAAA", "border": "#333333",
    "input_bg": "#1A1A1A", "terminal_bg": "#000000"
}

class IOXeuDeployManager(ctk.CTk):
    def __init__(self):
        super().__init__()
        self.title("IOXEU DEPLOY MANAGER v3.0 [FINAL ENGINE]")
        self.geometry("1400x900")
        self.configure(fg_color=CORES["bg"])
        
        # Segurança e Credenciais
        self.key_file = "ioxeu_master_key.bin"
        self.creds_file = "luis_accounts.json"
        self.init_security()
        self.load_credentials()
        
        # Layout Grid
        self.grid_columnconfigure(1, weight=1)
        self.grid_rowconfigure(1, weight=1)
        
        self.create_header()
        self.create_sidebar()
        self.create_main_area()
        self.check_first_run()

    # --- SEGURANÇA E DADOS ---
    def init_security(self):
        if not os.path.exists(self.key_file):
            with open(self.key_file, 'wb') as f: 
                f.write(Fernet.generate_key())
        with open(self.key_file, 'rb') as f: 
            self.cipher = Fernet(f.read())

    def load_credentials(self):
        try:
            with open(self.creds_file, 'r') as f:
                self.credentials = json.loads(self.cipher.decrypt(f.read().encode()).decode())
        except: 
            self.credentials = {"git": [{} for _ in range(4)], "cloud": [{} for _ in range(4)]}

    def save_credentials(self):
        with open(self.creds_file, 'wb') as f: 
            f.write(self.cipher.encrypt(json.dumps(self.credentials).encode()))

    # --- INTERFACE PRINCIPAL ---
    def create_header(self):
        h = ctk.CTkFrame(self, height=70, fg_color=CORES["card"], border_width=1, border_color=CORES["border"])
        h.grid(row=0, column=0, columnspan=2, sticky="ew")
        ctk.CTkLabel(h, text=" IOXEU DEPLOY MANAGER", font=("Inter Black", 28, "bold"), text_color=CORES["neon"]).pack(side="left", padx=30, pady=15)
        ctk.CTkLabel(h, text="ENTERPRISE ORCHESTRATOR // REAL GIT.PAGE ENGINE", font=("Consolas", 14), text_color=CORES["dim"]).pack(side="left", padx=(0,30))

    def create_sidebar(self):
        sf = ctk.CTkFrame(self, width=320, fg_color=CORES["card"], border_width=1, border_color=CORES["border"])
        sf.grid(row=1, column=0, sticky="nsew")
        
        ctk.CTkLabel(sf, text="CREDENTIAL VAULT", font=("Inter Black", 16, "bold")).pack(pady=(20,15), padx=20, anchor="w")
        
        tv = ctk.CTkTabview(sf, width=280, height=700, fg_color=CORES["card"], segmented_control_fg_color=CORES["border"])
        tv.pack(padx=20, pady=10, fill="both", expand=True)
        
        git_tab = tv.add("GIT PROVIDERS")
        cloud_tab = tv.add("CLOUD HOSTS")
        
        self._create_cred_inputs(git_tab, "git")
        self._create_cred_inputs(cloud_tab, "cloud")

    def _create_cred_inputs(self, tab, cred_type):
        scroll = ctk.CTkScrollableFrame(tab, fg_color="transparent")
        scroll.pack(fill="both", expand=True, padx=5, pady=5)
        
        for i in range(4):
            frame = ctk.CTkFrame(scroll, fg_color=CORES["input_bg"], corner_radius=8, border_width=1, border_color=CORES["border"])
            frame.pack(fill="x", pady=8, padx=5)
            
            ctk.CTkLabel(frame, text=f"SLOT #{i+1}", font=("Consolas", 12, "bold"), text_color=CORES["neon"]).pack(anchor="w", padx=15, pady=(10,5))
            
            name_e = ctk.CTkEntry(frame, placeholder_text="Provider Name", fg_color=CORES["terminal_bg"], text_color=CORES["text"], height=35)
            name_e.pack(fill="x", padx=15, pady=5)
            if self.credentials[cred_type][i].get("name"): name_e.insert(0, self.credentials[cred_type][i]["name"])
            
            token_e = ctk.CTkEntry(frame, placeholder_text="API Token / PAT", show="*", fg_color=CORES["terminal_bg"], text_color=CORES["text"], height=35)
            token_e.pack(fill="x", padx=15, pady=5)
            
            def save(idx=i, t=cred_type, n=name_e, tk=token_e):
                self.credentials[t][idx] = {"name": n.get(), "token": tk.get()}
                self.save_credentials()
                self.log(f"[OK] Credential {t.upper()} #{idx+1} encrypted locally.")
            
            ctk.CTkButton(frame, text="ENCRYPT & SAVE", height=35, fg_color=CORES["neon"], text_color="#000", command=save).pack(fill="x", padx=15, pady=(5,10))

    def create_main_area(self):
        mf = ctk.CTkFrame(self, fg_color=CORES["bg"])
        mf.grid(row=1, column=1, sticky="nsew", padx=20, pady=20)
        mf.grid_columnconfigure((0,1), weight=1)
        mf.grid_rowconfigure((0,1), weight=1)
        
        # Drop Zone
        dz = ctk.CTkFrame(mf, height=200, fg_color=CORES["card"], border_width=3, border_color=CORES["neon"], corner_radius=12)
        dz.grid(row=0, column=0, columnspan=2, sticky="ew", padx=5, pady=5)
        ctk.CTkLabel(dz, text="📂 DRAG PROJECT FOLDER HERE\n(Or click to select)", font=("Inter Black", 18, "bold")).pack(expand=True)
        dz.bind("<Button-1>", lambda e: self.select_folder())
        
        # Botões de Ação Principal
        btn_frame = ctk.CTkFrame(mf, fg_color="transparent", height=60)
        btn_frame.grid(row=1, column=0, columnspan=2, sticky="ew", pady=(0,10))
        
        self.deploy_btn = ctk.CTkButton(btn_frame, text="DEPLOY TO GIT.PAGE (REAL)", height=45, fg_color=CORES["neon"], text_color="#000", font=("Inter", 14, "bold"), command=self.start_deploy)
        self.deploy_btn.pack(side="left", padx=10, fill="x", expand=True)
        
        # Botão para Montador de Setup (Novidade)
        setup_btn = ctk.CTkButton(btn_frame, text="PREPARE PROFESSIONAL SETUP", height=45, fg_color="transparent", border_width=2, border_color=CORES["neon"], text_color=CORES["neon"], hover_color=CORES["card"], command=self.prepare_setup)
        setup_btn.pack(side="right", padx=10, fill="x", expand=True)

        # Terminals
        self.terminals = {}
        configs = [("SYSTEM LOG", 2, 0), ("GIT LOG", 2, 1), ("CLOUD LOG", 3, 0), ("CODE PREVIEW", 3, 1)]
        for title, r, c in configs:
            f = ctk.CTkFrame(mf, fg_color=CORES["terminal_bg"], border_width=1, border_color=CORES["border"])
            f.grid(row=r, column=c, sticky="nsew", padx=5, pady=5)
            f.grid_rowconfigure(1, weight=1); f.grid_columnconfigure(0, weight=1)
            
            ctk.CTkLabel(f, text=title, font=("Consolas", 12, "bold"), text_color=CORES["neon"], anchor="w").grid(row=0, column=0, sticky="ew", padx=10, pady=5)
            txt = ctk.CTkTextbox(f, font=("Consolas", 12), fg_color="transparent", text_color="#FFF")
            txt.grid(row=1, column=0, sticky="nsew", padx=10, pady=(0,10))
            self.terminals[title] = txt
            
        self.log("[INIT] IOXEU DEPLOY MANAGER v3.0 READY")
        self.log("[ENGINE] Real Git + GitHub Pages API loaded")

    def log(self, msg):
        if "SYSTEM LOG" in self.terminals:
            self.terminals["SYSTEM LOG"].insert("end", f"> {msg}\n")
            self.terminals["SYSTEM LOG"].see("end")

    # --- LÓGICA DE SELEÇÃO DE PASTA ---
    def select_folder(self):
        folder = filedialog.askdirectory(title="Select Project Folder")
        if folder:
            self.selected_folder = folder
            self.log(f"[SCAN] Project selected: {os.path.basename(folder)}")
            self.log(f"[PATH] {folder}")

    # --- MOTOR DE DEPLOY REAL ---
    def start_deploy(self):
        if not hasattr(self, 'selected_folder'):
            self.log("[ERROR] No project folder selected! Click the drop zone first.")
            return
        threading.Thread(target=self._deploy_logic, daemon=True).start()

    def _deploy_logic(self):
        try:
            # 1. Pegar credencial ativa (Slot #1 do Git)
            git_token = self.credentials["git"][0].get("token", "")
            git_name = self.credentials["git"][0].get("name", "GitHub")
            
            if not git_token:
                self.log("[ERROR] No active Git credential found in Slot #1!")
                return

            self.log(f"[AUTH] Connected to {git_name}")
            
            # 2. Preparar estrutura
            project_name = os.path.basename(self.selected_folder)
            deploy_dir = os.path.join(os.path.expanduser("~"), "Desktop", f"ioxeu-deploy-{project_name}")
            
            self.log(f"[BUILD] Creating deploy structure at: {deploy_dir}")
            if os.path.exists(deploy_dir):
                shutil.rmtree(deploy_dir)
            shutil.copytree(self.selected_folder, deploy_dir)
            
            # Criar index.html básico se não existir (para GitHub Pages funcionar)
            index_path = os.path.join(deploy_dir, "index.html")
            if not os.path.exists(index_path):
                with open(index_path, 'w', encoding='utf-8') as f:
                    f.write(f"""<!DOCTYPE html>
<html>
<head><title>{project_name}</title></head>
<body>
<h1>{project_name}</h1>
<p>Deployed by IOXEu Deploy Manager</p>
</body>
</html>""")
                self.log("[FIX] Generated default index.html for GitHub Pages")

            # 3. Git Init + Commit
            self.log("[GIT] Initializing repository...")
            os.chdir(deploy_dir)
            subprocess.run(["git", "init"], capture_output=True, check=True)
            subprocess.run(["git", "add", "."], capture_output=True, check=True)
            subprocess.run(["git", "commit", "-m", f"ioxeu-deploy: {project_name}"], capture_output=True, check=True)
            subprocess.run(["git", "branch", "-M", "main"], capture_output=True, check=True)
            self.log("[GIT] Local repository ready")

            # 4. Criar Repo Remoto via API
            self.log("[API] Creating remote repository...")
            headers = {
                "Authorization": f"token {git_token}",
                "Accept": "application/vnd.github.v3+json"
            }
            repo_payload = {"name": f"ioxeu-{project_name.lower().replace(' ', '-')}", "private": False}
            resp = requests.post("https://api.github.com/user/repos", json=repo_payload, headers=headers)
            
            if resp.status_code == 201:
                repo_data = resp.json()
                owner = repo_data["owner"]["login"]
                repo_name = repo_data["name"]
                self.log(f"[API] Repository created: {owner}/{repo_name}")
                
                # 5. Push Real
                remote_url = f"https://{git_token}@github.com/{owner}/{repo_name}.git"
                self.log("[PUSH] Uploading files to GitHub...")
                push_result = subprocess.run(["git", "push", "-u", "origin", "main"], capture_output=True, text=True)
                
                if push_result.returncode == 0:
                    self.log("[PUSH] Upload successful!")
                    
                    # 6. Ativar GitHub Pages via API
                    self.log("[PAGES] Enabling GitHub Pages automatically...")
                    pages_payload = {"source": {"branch": "main", "path": "/"}}
                    pages_resp = requests.post(
                        f"https://api.github.com/repos/{owner}/{repo_name}/pages",
                        json=pages_payload, headers=headers
                    )
                    
                    if pages_resp.status_code in [201, 409]:  # 409 = já estava ativo
                        live_url = f"https://{owner}.github.io/{repo_name}/"
                        self.log(f"[SUCCESS] 🚀 LIVE: {live_url}")
                        self.log("[DONE] Deployment finished successfully!")
                    else:
                        self.log(f"[WARN] Pages activation returned {pages_resp.status_code}. Check repo settings manually.")
                        self.log(f"[INFO] URL should be: https://{owner}.github.io/{repo_name}/")
                else:
                    self.log(f"[ERROR] Push failed: {push_result.stderr}")
            else:
                self.log(f"[ERROR] API Error {resp.status_code}: {resp.json().get('message')}")
                
        except Exception as e:
            self.log(f"[FATAL] {str(e)}")
            import traceback
            self.log(traceback.format_exc())

    # --- MONTADOR DE SETUP PROFISSIONAL ---
    def prepare_setup(self):
        if not hasattr(self, 'selected_folder'):
            self.log("[ERROR] No project folder selected!")
            return
        
        self.log("[SETUP] Preparing professional installer structure...")
        project_name = os.path.basename(self.selected_folder)
        setup_dir = os.path.join(os.path.expanduser("~"), "Desktop", f"{project_name}-SETUP-PACK")
        
        if os.path.exists(setup_dir):
            shutil.rmtree(setup_dir)
        os.makedirs(setup_dir)
        
        # Copiar arquivos do projeto
        dest_project = os.path.join(setup_dir, "APP_FILES")
        shutil.copytree(self.selected_folder, dest_project)
        
        # Criar script de instalação simples (batch para Windows)
        installer_script = os.path.join(setup_dir, "INSTALL.bat")
        with open(installer_script, 'w') as f:
            f.write(f"""@echo off
echo ==========================================
echo INSTALLING {project_name.upper()}
echo ==========================================
mkdir "%USERPROFILE%\\Documents\\{project_name}"
xcopy "APP_FILES\\*" "%USERPROFILE%\\Documents\\{project_name}\\*" /E /Y
echo.
echo Installation Complete!
echo You can find your app in Documents\\{project_name}
pause
""")
        
        self.log(f"[SETUP] Professional package created at: {setup_dir}")
        self.log("[SETUP] Ready for distribution or further packaging.")

    # --- TUTORIAL INTEGRADO ---
    def check_first_run(self):
        if not os.path.exists("ioxeu_tutorial_done.flag"):
            self.after(500, self.show_tutorial)

    def show_tutorial(self):
        overlay = ctk.CTkToplevel(self)
        overlay.title("Welcome to IOXeu")
        overlay.geometry("600x400")
        overlay.configure(fg_color="#000000E6")
        overlay.transient(self)
        overlay.grab_set()
        
        ctk.CTkLabel(overlay, text="WELCOME TO IOXEU DEPLOY MANAGER", font=("Inter Black", 24), text_color=CORES["neon"]).pack(pady=(40,20))
        ctk.CTkLabel(overlay, text="1. Save your Git Token in the left sidebar\n2. Click the drop zone to select your project\n3. Choose DEPLOY or SETUP", font=("Consolas", 14), text_color=CORES["text"], justify="left").pack(padx=40)
        
        def close_tut():
            open("ioxeu_tutorial_done.flag", "w").close()
            overlay.destroy()
            
        ctk.CTkButton(overlay, text="GET STARTED", fg_color=CORES["neon"], text_color="#000", command=close_tut).pack(pady=40)

if __name__ == "__main__":
    app = IOXeuDeployManager()
    app.mainloop()
