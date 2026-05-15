# DC-1 CTF (VulnHub)

## Əvvəlcə Məlumat

Mərhələ 1: İnformasiya Toplanması və Şəbəkə Analizi (Reconnaissance)
Hücumun ilk mərhələsində hədəf maşını müəyyən etmək və onun üzərindəki xidmətləri analiz etmək üçün sistemli bir yol izlədim.

1.1 Hədəf IP-nin Müəyyən Edilməsi
Şəbəkədəki canlı hostları tapmaq üçün netdiscover alətindən istifadə etdim. Skan nəticəsində hədəf maşının 192.168.100.85 IP ünvanında olduğunu müəyyən etdim.

1.2 Port Skanlama və Xidmət Analizi (Nmap)
Hədəf üzərindəki açıq portları və servisləri müəyyən etmək üçün nmap ilə dərin analiz apardım:
Servis versiyaları və OS təyini üçün

 $\color{red}{\text{nmap -sS -sV -O 192.168.100.85}}$

Nəticələr:
*Port 22: OpenSSH 6.0p1 (Debian)
*Port 80: Apache httpd 2.2.22 (Drupal CMS işləyir)
*Port 111: rpcbind

Bundan əlavə, SSH servisinin hansı alqoritmləri dəstəklədiyini və potensial zəifliklərini görmək üçün xüsusi Nmap script-ini işə saldım:

$\color{red}{\text{nmap --script ssh2-enum-algos -p22 192.168.100.85}}$

1.3 Web İnterfeys və Directory Enumeration
80-ci portu brauzerdə açdıqda bizi standart bir Drupal Site giriş paneli qarşıladı.
Sistemin arxa tərəfindəki gizli qovluqları və faylları aşkar etmək üçün gobuster aləti ilə common.txt wordlist-indən istifadə edərək skan apardım:

$$\color{red}{\text{gobuster \ dir \ -u \ [http://192.168.100.85](http://192.168.100.85) \ -w \ /usr/share/wordlists/dirb/common.txt}}$$

Tapıntılar:
/includes, /misc, /modules, /themes (Standart Drupal qovluqları)
robots.txt və CHANGELOG.txt kimi informasiya sızdıra biləcək fayllar.

1.4 Zəiflik Araşdırması (Research)
OpenSSH 6.0p1 versiyası üçün apardığım araşdırma nəticəsində bu versiyanın CVE-2018-15473 (User Enumeration) zəifliyinə qarşı həssas ola biləcəyini qeyd etdim. Bu, sistemdəki [...]


<img width="647" height="151" alt="1" src="https://github.com/user-attachments/assets/6a61fc8a-08f0-49ea-a8a2-682d0b1d83ef" />
<img width="866" height="318" alt="2" src="https://github.com/user-attachments/assets/7db1d48b-6d39-4142-bf34-88268591ae35" />
<img width="1366" height="596" alt="3" src="https://github.com/user-attachments/assets/5242147e-56d5-4d5d-952d-17fe821e94d2" />
<img width="859" height="416" alt="4" src="https://github.com/user-attachments/assets/b4931189-ff6e-40bd-baff-4198a396b508" />
<img width="866" height="318" alt="5" src="https://github.com/user-attachments/assets/[IMAGE5-SSH-ALGORITHMS]" />
<img width="1366" height="596" alt="6" src="https://github.com/user-attachments/assets/[IMAGE6-GOBUSTER-OUTPUT]" />
<img width="859" height="416" alt="7" src="https://github.com/user-attachments/assets/[IMAGE7-GOBUSTER-RESULTS]" />
<img width="647" height="151" alt="8" src="https://github.com/user-attachments/assets/[IMAGE8-NMAP-MAC]" />


## Zəiflik Analizi

[Buraya zəiflik analizi mətnini yazın. Hanı zəifliklər tapıldı, necə tapıldı, etc.]

![Screenshot 2](screenshots/screenshot2.jpg)

## Exploitation Prosesi

[Buraya exploitation prosesini detallarından yazın. Hansı toollar istifadə etdiniz, hansı komandalar çalışdırdınız, etc.]

![Screenshot 3](screenshots/screenshot3.jpg)

## Hücum Nəticəsi

[Buraya hücumun nəticəsini yazın. Nə əldə etdiniz, hanı flagları tapdınız, etc.]

![Screenshot 4](screenshots/screenshot4.jpg)

## Dərslərin Çıxarılması

[Buraya öyrəndiyiniz dərsləri və tövsiyələri yazın.]

![Screenshot 5](screenshots/screenshot5.jpg)

## Kaynaklar

[Buraya istifadə etdiyiniz kaynakları, linkləri yazın.]
