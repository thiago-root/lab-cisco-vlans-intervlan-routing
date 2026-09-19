# Laboratório Prático: VLANs, Enlaces Trunk e Roteamento Inter-VLAN (Router-on-a-Stick)

## 📌 Descrição do Projeto
Este projeto foi desenvolvido no Cisco Packet Tracer para demonstrar e comparar duas arquiteturas de segmentação de redes locais:
1. **Cenário A:** Segmentação por VLANs utilizando enlaces de acesso dedicados por porta (sem enlace Trunk e sem roteamento entre VLANs).
2. **Cenário B:** Segmentação avançada por VLANs com tronco IEEE 802.1Q, Roteamento Inter-VLAN (*Router-on-a-Stick*) e distribuição dinâmica de IP via **Servidor DHCP** integrado no roteador Cisco.

---

## 🛠️ Tecnologias e Conceitos Utilizados
* **Cisco Packet Tracer 8.x**
* **Switches e Roteadores Cisco IOS**
* **VLANs (Virtual Local Area Networks):** Isolamento de domínios de broadcast (VLAN 10 - Vendas e VLAN 20 - RH).
* **Trunking (IEEE 802.1Q):** Encapsulamento e sinalização de tags em enlaces tronco.
* **Router-on-a-Stick (ROAS):** Configuração de subinterfaces e gateways padrão para comunicação entre sub-redes.
* **DHCP Service:** Configuração de múltiplos pools de IP dinâmicos em roteador Cisco.

---

## 📐 Topologia e Arquitetura

### Cenário A (Acesso Dedicado / Sem Roteamento)
* **VLAN 10 (Rede 192.168.10.0/24):** PC-A1 e PC-A3
* **VLAN 20 (Rede 192.168.20.0/24):** PC-A2 e PC-A4
* **Comportamento:** Comunicação limitada exclusivamente à mesma VLAN através de cabos de acesso dedicados entre os switches `S1A` e `S2A`. Comunicação entre VLAN 10 e VLAN 20 inexistente por ausência de gateway/roteador.

### Cenário B (Trunk + Router-on-a-Stick + DHCP)
* **Subinterface g0/0/0.10:** Gateway `192.168.10.1` (VLAN 10)
* **Subinterface g0/0/0.20:** Gateway `192.168.20.1` (VLAN 20)
* **Comportamento:** Enlace tronco 802.1Q entre os switches `S1B` e `S2B` consolidando todo o tráfego. O `Router1` provê os IPs via DHCP para as duas sub-redes e realiza o roteamento de pacotes entre VLANs distintas.

---

## 🧪 Validação dos Testes de Conectividade

### 1. Comunicação Intra-VLAN - Cenário A (Mesma VLAN)
Sucesso no disparo de requisições `ping` entre hosts da mesma VLAN no Cenário A (VLAN 10).

![Teste Mesma VLAN](cenario-a-ping-sucesso.png)

### 2. Isolamento Inter-VLAN - Cenário A (Sem Roteador)
Falha/Timeout esperada ao tentar pingar entre a VLAN 10 e a VLAN 20 no Cenário A devido à ausência de dispositivo de Camada 3.

![Teste VLANs Diferentes Sem Roteador](cenario-a-ping-falha.png)

### 3. Roteamento Inter-VLAN - Cenário B (Com Router-on-a-Stick)
Sucesso na comunicação entre dispositivos de VLANs distintas (VLAN 10 e VLAN 20) através do roteamento via subinterfaces no `Router1`. Nota-se a perda inicial do 1º pacote devido à resolução de endereço via protocolo **ARP**, seguida de 100% de êxito nos pacotes subsequentes.

![Teste Roteamento Inter-VLAN Cenário B](cenario-b-ping-sucesso.png)

---

## 📁 Como executar o projeto
1. Faça o download do arquivo `Lab_VLANs_InterVLAN_RouterOnAStick.pkt` localizado neste repositório.
2. Abra o arquivo no **Cisco Packet Tracer**.
3. Execute os testes no *Command Prompt* dos PCs ou acompanhe a passagem dos quadros no modo de simulação.
