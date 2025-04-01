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
  
Ya da aşağıda verilmiş 4 ekran kartında birinin olduğu bir sistem

- RTX 3090, RTX 4090, A100, H100
- RAM: 16+ GB

## Yükleme Adımları
- Aşğıdaki adımları sırayla uygulayarak testente katılabilirsiniz.

1-) Sistemn Güncellemeleri
```
sudo apt update && sudo apt install lz4 ocl-icd-opencl-dev ocl-icd-libopencl1 tar wget make libopencl-clang-dev tmux build-essential git jq  libgomp1 -y && sudo apt install wget -y && cd $HOME
```
