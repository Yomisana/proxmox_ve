# CPU 建議採購方針指南
- 建議選擇持有 AVX2 指令集的



# PVE 下優化處理器
預設模式為: 效能模式
如果有 "ondemand" 建議選此項，在需要時提高時脈

## "可能"可以解決虛擬機凍結問題
> 在 proxmox 上安裝 intel/AMD microcode 軟體包可能可以解決
> 這可能可以"大幅降低"，但可能"無法完全解決"。
> 注意! 如果你有使用 CPU 漏洞，此處理器補丁包不要更新
1. ```echo "deb http://deb.debian.org/debian/ unstable non-free-firmware" > /etc/apt/sources.list.d/debian-unstable.list```
2. ```sudo nano /etc/apt/preferences.d/unstable-repo```
3. paste this to unstable-repo file.
```
# All unstable repo priority
Package: *
Pin: release o=Debian,a=unstable
Pin-Priority: 10

# Allow unstable repo update intel microcode
Package: intel-microcode
Pin: release o=Debian,a=unstable
Pin-Priority: 500
#
Package: amd64-microcode
Pin: release o=Debian,a=unstable
Pin-Priority: 500
```
4. Update proxmox repo
```apt update && apt list --upgradable```
```
5. install cpu microcode
```
# Intel CPU
apt install intel-microcode
# AMD CPU
apt install amd64-microcode
```
6. reboot
```reboot```
7. If restart finish check this command will know microcode is works
``journalctl -k --grep="microcode updated early to"``
> Nov 01 23:30:19 pve kernel: microcode: microcode updated early to revision 0x42e, date = 2019-03-14
Done!
