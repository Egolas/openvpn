������ű���������Ի�ӭ������https://www.iewb.net/qg/4727.html

�ű��Ǹ����ҵ������д�ģ�ʹ�����ɺõ���Կ/֤�飬�����ʹ�ýű���װ��ɺ�����openvpn����/etc/openvpnĿ¼��client.zip������������ѹ����ڿͻ����޸ĳ���ķ����ip�Ϳ���ʹ�á�

����ķ�������ִ�У�

git clone https://github.com/qiguang0920/openvpn.git && cd openvpn &&chmod +x OpenVPN_centos7.sh &&./OpenVPN_centos7.sh
�Ϳ����Զ���װ��

���ű�˵����
1��ʹ�õ�Ĭ��1194/udp�˿�
2���ű�������centos7ϵͳ�����������redhatϵ�е�ϵͳ����Ҫ�ֶ��������ǽ�˿ڣ�debanϵ�в�֧��

�����ű��ʺ�����ٲ������ƫ����ͯЬ������԰�ȫҪ��ϸߣ��ڰ�װ��ɺ������������֤�飬��������server.confָ�������ɵ�֤��Ϳ����ˡ��ͻ���ͬ����

����OpenVPN֤���ǩ��
��������/etc/openvpn/easy-rsa/easyrsa3

�������ɷ�������������Կ

1��./easyrsa init-pki    //Ŀ¼��ʼ��
2��./easyrsa build-ca    //������֤��CA,����������ס����Ȼ�Ժ���Ϊ֤��ǩ��������Ҫ����common name ͨ������������Լ�������ã�һ������Ϊǩ������������������
3../easyrsa gen-req server_iewb.net nopass    //������������֤�飬�˴����������server_iewb.net��Ҳ�����Ǳ�����֣������������ļ�server_iewb.net.req��server_iewb.net.key
4��./easyrsa sign server server_iewb.net        //ǩԼ�����֤�飬��Ҫ�ṩCA���루�ڶ���ʱ�����룩��������server_iewb.net.crt
5��./easyrsa gen-dh    //����Diffie-Hellman��ȷ��key��Խ����ȫ���������

�������ɿͻ���������Կ

1��./easyrsa gen-req client_iewb.net    //clientΪ�Զ��壬�����Ǳ�ģ�������client_iewb.net.req��client_iewb.net.key����Ϊû�кͷ�����һ��ʹ��nopass��������������ʱ��������һ��֤�����롣

2��./easyrsa import-req  ./pki/reqs/client_iewb.net.req client1    //����req���˴�Ŀ¼���������ɵ����ֶ�Ҫ��ȷ��������Ǹ�client1�������Ϊע�ͣ���ʵ��һ�������ƣ�ǩԼ֤��ʱ����ʹ�ö�����ǩԼ��        
3��./easyrsa sign client client_iewb.net        //ǩԼ֤�� ,ͬǩԼ�����֤��һ������Ҫ����CA����

�������ɵ��ļ�����Ŀ¼�ֱ�Ϊ��

easy-rsa/easyrsa3/pki/ca.crt
easy-rsa/easyrsa3/pki/reqs/server_iewb.net.req
easy-rsa/easyrsa3/pki/reqs/client_iewb.net.req
easy-rsa/easyrsa3/pki/private/ca.key
easy-rsa/easyrsa3/pki/private/server_iewb.net.key
easy-rsa/easyrsa3/pki/private/client_iewb.net.key
easy-rsa/easyrsa3/pki/issued/server_iewb.net.crt
easy-rsa/easyrsa3/pki/issued/client_iewb.net.crt
easy-rsa/easyrsa3/pki/dh.pem

����.req��.keyΪ����֤��ʱ���ɣ�.crtΪǩԼ֤��ʱ���ɣ�ǩԼ֤��ʱ����Ҫ����CA���룬��ʵ����ʹ�õ���.crt��.key������ca.crt����˺Ϳͻ��˶����õ��������Ϊ���������֤�飬�����ٴ������������֤��(��ͬ����)�C����CǩԼ֤��

����һ������£����絥λ��ѧУ���ܸ���Ҫ������ʹ��һ��֤�飬Ȼ���������û����������½�����Ǵ�openvpn�������ļ�server.conf�����������е�ע��ȥ��

auth-user-pass-verify /etc/openvpn/checkpsw.sh via-env
username-as-common-name
script-security 3

�����ʹ��֤�飬ֻʹ���û�����������֤��������һ�е�ע��Ҳȥ��

client-cert-not-required 

�������ϼ������ùٷ�������Ĭ����û�еģ������ֶ�����openvpn��С�����԰��⼸�м��ϣ�ʹ�ýű���װ��С���ֻ��ȥ��ע�;Ϳ����ˡ�

����Ȼ�����Ǳ༭psw-file�������涨���û��������룬һ��һ�����û���������ʹ�ÿո�ֿ���
����ͬ����checkpsw.sh��psw-file�������ļ��ٷ���װ����װ��Ҳ��û�еģ�checkpsw.sh���ǿ��Դ��������أ�psw-file�Լ��½�һ�����С�
����checkpsw.sh�ٷ����ص�ַ�� http://openvpn.se/files/other/checkpsw.sh ��PS:�����ַ��ǽ�ˣ�
����Ҳ���Կ����https://github.com/qiguang0920/openvpn/blob/master/data/checkpsw.sh

����Ȼ��ͻ�������ҲҪ�����£���client.ovpn�м���һ�У�

auth-user-pass 

������������˺Ϳͻ������Ǿ���������Կ���û�������˫��֤�������û�ʹ��ͬһ����Կ��Ȼ����䲻ͬ���û��������롣