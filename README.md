<p align="center">
  <a href="">
    <img alt="Hero" src="https://github.com/user-attachments/assets/f476f067-3a68-4765-8388-48d022a50ddf" width="75%" />
  </a>
</p>

## Ön Bilgi
- Yapay zeka alanında olan Gensyn testnetinde aşağıda verilen sistem gereksinimlerine uyan lokal veya bir vps de çalıştırabilirsiniz. Ekran kartı sistemlerde daha ön planda ama sadece işlemci olan makinalarla da katılabiliyorsunuz.

## Tavsiye Edilen Sistem Gereksinimleri
- CPU: Minumum Bir Değer Yok
- RAM: 16+ GB
- İşletim Sistemi: Ubuntu 22.04LTS
  
ya da aşağıda verilmiş 4 ekran kartında birinin olduğu bir sistem

- RTX 3090, RTX 4090, A100, H100
- RAM: 16+ GB
- - İşletim Sistemi: Ubuntu 22.04LTS

## Yükleme Adımları
- Aşğıdaki adımları sırayla uygulayarak testente katılabilirsiniz.

1-) Sistem Güncellemeleri ve Tmux Ekranı
```
sudo apt update && sudo apt install lz4 ocl-icd-opencl-dev ocl-icd-libopencl1 tar wget make libopencl-clang-dev tmux build-essential git jq  libgomp1 -y && sudo apt install wget -y && cd $HOME && tmux new-session -t gensyn
```
NOT: Tmux ekranında çıkmak için ctrl+b sonra d'ye basıyoruz. Tekrar tmux ekranına girmek için ```tmux attach -t gensyn``` yazıyoruz

2-) Python Kurulumu
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

6-) Run Swarm (İlk soruda Y'ye ikinci soruda N'ye basın ve gelen ekranlarda Enter'a basın geçin)
```
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

7-) Giriş
- Bilgisayarımızda tarayıcıya ```http://VPSIP:3000/``` yazıp aşağıdaki görselde olduğu gibi ekranın gelmesini bekliyoruz.

- Daha sonra Login'e tıkladığımızda bize seçenekler sunuyor. Mail adresi girebilir ya da direkt gmail ile bağlanabilirsiniz. Eğer sorun çıkmazsa 9. adımdan devam edin. Kod gelmiyor ya da bağlanamıyorsanız 8. adımı uygulayın.

8-) Kod gelmediği için işlemleri ngrok aracılıpyla tamamlayacağız. Öncelikle aşağıdaki kodları girelim.
x86;
```
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz && tar -xvzf ngrok-v3-stable-linux-amd64.tgz && sudo mv ngrok /usr/local/bin/
```

aarch64;
```
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm64.tgz && tar -xvzf ngrok-stable-linux-arm64.tgz && sudo mv ngrok /usr/local/bin/
```
- ```https://ngrok.com/``` girip üyelik oluşturuyoruz.
- Daha sonra sol üst taraftan ```Your Authtoken```'a tıklıyoruz.
- Açılan ekranda ```Show Authtoken```'a tıklayıp çıkan satırı Vps'de 2. bir tmux ekranı açarak o ekranda yapıştırıyoruz.
- Daha sonra ```ngrok http 3000``` yazıp enterlayınca bize aşağıdaki ss'de ki gibi ekranda verdiği adresi tarayıcımızda yapıştırıp giriş işlemlerini yapıyoruz.

9-) Kod geldikten ve giriş ekranı onayımızı gördükten sonra logları izlemeye devam ediyoruz. Buradaki işlemler vakit alabilir. SS'de ki ilk kutucuk bizim ismimizi 2. kutucuk ise işlemlerin sorunsuz bittiğini ve node'un çalıştığını gösteriyor.
![gsyn](https://github.com/user-attachments/assets/892ea3c5-9930-4b01-9bfc-388360d9b78e)

10-) Yedek Alma
- Başlarken size verdiği node ismini ve vps'in içinde root kullanıcısında olan ```swarm.pem``` (/root/rl-swarm/swarm.pem) isimli dosyayı mutlaka yedekliyorsunuz. 

## Güncelleme Adımları - 28.09.2025
- Arkadaşlar iki yol var. Birincisini denedikten sonra hata verirse ikinci yolu deneyin. Öncesinde kesinlikle yükleme adımlarında 10. sırada bahsettiğim swaprm.pen dosyasının yediğini alın. İlk olarak ```ctrl+c``` yaparak node mutlaka durdurun. Kodları girdikten sonra en alttaki işlemleri yapın.

1-) Repo Güncelleyerek Başlatmak
```
cd
deactivate
cd rl-swarm
git fetch
git reset --hard origin/main
python3 -m venv .venv
source .venv/bin/activate
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 22
node -v
pip install trl
pip uninstall trl -y
pip install git+https://github.com/huggingface/trl.git
pip install torch --index-url https://download.pytorch.org/whl/cpu
pip install hf_xet
./run_rl_swarm.sh
```

2-) Bütün Dosyaları Kaldırdıktan Sonra Tekrar Klonlayarak Başlatmak
```
cd
deactivate
mv /root/rl-swarm/swarm.pem /root/
rm -rf rl-swarm
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
mv /root/swarm.pem /root/rl-swarm/
chmod +x swarm.pem
python3 -m venv .venv
source .venv/bin/activate
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 22
node -v
pip install protobuf==3.12.2
pip install transformers==4.51.3 --force-reinstall
git describe --tags
sed -i -E 's/(num_train_samples:\s*)2/\1 1/' rgym_exp/config/rg-swarm.yaml
sed -i '1i # ~/.bashrc: executed by bash(1) for non-login shells.\n\n# If not running interactively, don'\''t do anything\ncase $- in\n    *i*) ;;\n    *) return;;\nesac\n' ~/.bashrc
pip install hf_xet
pip install trl
pip uninstall trl -y
pip install git+https://github.com/huggingface/trl.git
pip install torch --index-url https://download.pytorch.org/whl/cpu
./run_rl_swarm.sh
```

- Bu adımlardan sonra ngrok ekranında da giriş yapıp node başlatıyoruz. Bundan sonra ilk gelen ekranda ``N``, daha sonra gelen soruya da ``Enter`` A basıyoruz sonra gelen AI Prediction Market sorusuna ``Y`` yapıp geçiyoruz. Logları biraz izleyin çalıştığından emin olun.

### ```ValueError: Your setup doesn't support bf16/gpu.``` Hatasının Çözümü
- Sadece CPU üzerinde çalıştıracak olanlar, yükleme ya da güncelleme sonucunda yukarıdaki hata ile karşılaşıyorlar. Aşağıdaki kodlarla çözülüyor. İlk önce CTRL+C yaparak node durduruyoruz. Son kodlardan devam.
```
rm -rf /root/rl-swarm/rgym_exp/config/rg-swarm.yaml
wget -q -O /root/rl-swarm/rgym_exp/config/rg-swarm.yaml https://raw.githubusercontent.com/okannako/gensyn/refs/heads/main/rg-swarm.yaml && chmod +x /root/rl-swarm/rgym_exp/config/rg-swarm.yaml
```
- Bu kodları girdikten sonra normal bir şekilde node tekrar başlatıyoruz.


- Kontrol için aşağıdaki siteyi kullanabilirsiniz.
> https://dashboard.gensyn.ai/

