1. I installed VMware Fusion and I am using it with "ubuntu-24.04.4-live-server-arm64.iso".
2. I launched the VM and ssh'd into it using VSCode. I cloned my repo in the VM under "/home/pravella/projects/ebpf-firewall". I pasted an image of my current repo structure.
3. The VM has 4 vCPU, 8GB RAM, and 40GB Disk. It is connected using NAT from my personal Mac.
4. uname -r prints "6.8.0-101-generic".
5. uname -m prints "aarch64".
6. I installed all of the packaged with no issues
7. I did not install BCC from the source, I simply used apt and everything seems to be working. There was no mention of outdated builds on their new docs.
8. Mount bpffs worked properly.
9. Kernel features are fine.
10. ip link is "ens160" and ip addr is "inet 192.168.125.128/24"
11. sudo bpftool feature probe dev ens160 results in:
Scanning system call availability...
bpf() syscall is available
Scanning eBPF program types...
eBPF program_type sched_cls is NOT available
eBPF program_type xdp is NOT available
Scanning eBPF map types...
eBPF map_type hash is NOT available
eBPF map_type array is NOT available
Scanning eBPF helper functions...
eBPF helpers supported for program type sched_cls:
        Program type not supported
eBPF helpers supported for program type xdp:
        Program type not supported
Scanning miscellaneous eBPF features...
Large program size limit is NOT available
Bounded loop support is NOT available
ISA extension v2 is NOT available
ISA extension v3 is NOT available

12. ip route results in:
ip route
default via 192.168.125.2 dev ens160 proto dhcp src 192.168.125.128 metric 100 
192.168.125.0/24 dev ens160 proto kernel scope link src 192.168.125.128 metric 100 
192.168.125.2 dev ens160 proto dhcp scope link src 192.168.125.128 metric 100 

13. Created python venv with no issue 

14. ethtool -i ens160
driver: e1000e
version: 6.8.0-101-generic
firmware-version: 1.8-0
expansion-rom-version: 
bus-info: 0000:02:00.0
supports-statistics: yes
supports-test: yes
supports-eeprom-access: yes
supports-register-dump: yes
supports-priv-flags: yes

15. BCC works correctly, the python command worked. bpftool is using version v7.4.0, python3 is using version 3.12.3, and clang is using version 18.1.3