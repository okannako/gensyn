<p align="center">
  <a href="https://orbisworlds.org">
    <img alt="Hero" src="https://github.com/user-attachments/assets/f476f067-3a68-4765-8388-48d022a50ddf" width="75%" />
  </a>
</p>

## Ön Bilgi
- Yapay zeka alanında olan Gensyn testnetinde aşağıda verilen sistem gereksinimlerine uyan lokal veya bir vps de çalıştırabilirsiniz. Ekran kartı sistemlerde daha ön planda ama sadece işlemci olan makinalarla da katılabiliyorsunuz.

## Tavsiye Edilen Sistem Gereksinimleri
- CPU: Minumum Bir Değer Yok
- RAM: 16+ GB
- - İşletim Sistemi: Ubuntu 22.04LTS
  
Ya da aşağıda verilmiş 4 ekran kartında birinin olduğu bir sistem

- RTX 3090, RTX 4090, A100, H100
- RAM: 16+ GB
- - İşletim Sistemi: Ubuntu 22.04LTS

## Yükleme Adımları
- Aşğıdaki adımları sırayla uygulayarak testente katılabilirsiniz.

1-) Sistem Güncellemeleri
```
sudo apt update && sudo apt install lz4 ocl-icd-opencl-dev ocl-icd-libopencl1 tar wget make libopencl-clang-dev tmux build-essential git jq  libgomp1 -y && sudo apt install wget -y && cd $HOME
```

2-) Python kurulumu
```
sudo apt-get install python3
sudo apt-get -y install python3-pip
sudo apt install python3.10-venv
```

3-) Node Yükleme
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 22
node -v
sudo apt install npm
npm -v
```

4-) Docker Yükleme
```
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh
```

5-) Proje Dosyaları
```
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
```

6-) Tmux Ekranı Açamak ve Run Swarm (İlk soruda Y'ye ikinci soruda N'ye basın ve gelen ekranlarda Enter'a basın geçin)
```
tmux new-session -t gensyn
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

7-) Giriş
