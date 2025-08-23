-  Atualizar lista de pacotes e pacotes do sistema
```bash
sudo apt update && sudo apt upgrade -y	
```

- Verificar nome da interface (normalmente enp0s3 na VM)
```bash
ip link
```
	Pegue o nome normalmente da segunda interface, ignorando lo (loopback)

- Instale o pacote do server dhcp (isc-dhcp-server)
```bash
sudo apt install isc-dhcp-server
```
-  Configure `/etc/dhcp/dhcpd.conf`
```bash
sudo nano /etc/dhcp/dhcpd.conf
```
- Adicione o seguinte no final do arquivo:
```
subnet 192.168.0.100 netmask 255.255.255.0 {
	range 192.168.0.100 192.168.0.200;
	option routers 192.168.0.1;
	option domain-name-servers: 8.8.8.8;
}
```
	Explicação:
		`subnet e netmask definem o ip da rede e máscara de subrede`
		 `range diz que o servidor irá distribuir ips entre 192.168.0.100 e *.200`
		 `routers diz o ip do roteador/gateway`
		 `domain-name-servers indica o ip do servidor dns (8.8.8.8 é o do google)`
- Configure `/etc/default/isc-dhcp-server`
```bash
sudo nano /etc/default/isc-dhcp-server
```
```
Coloque o nome da interface descoberta com ip link dentro das aspas de INTERFACESv4

Ex:
INTERFACESv4="enps0s3"
```
- Reinicie o servidor dhcp e verifique se está rodando
```bash
sudo systemctl restart isc-dhcp-server
```
```bash
sudo systemctl status isc-dhcp-server
```
	se aparecer running em verde o servidor está configurado corretamente e rodando