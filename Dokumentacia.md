# LEPSIE SA CITA V CODE PREVIEW #
DOKUMENTACIA : VPN A

Cieľom projektu je vytvoriť VPN sieť, ktorá prepája dve geograficky oddelené lokality cez GRE 
(Generic Routing Encapsulation) tunel v Cisco Packet Tracer. Tento tunel umožní prístup z 
vzdialenej siete k tlačiarni v lokálnej sieti.

Požitý hardware:

•	Lokálna sieť:
o	1x Router (Cisco 2811)
o	1x Switch (Cisco 2960)
o	3x PC (PC0, PC1, PC2)
o	1x Tlačiareň (Printer0)

•	Vzdialená sieť:
o	1x Router (Cisco 2811)
o	1x Switch (Cisco 2960)
o	2x PC (PC3, PC4)

Kroky konfigurácie:

1. Fyzická topológia
Najprv som vytvoril topológiu v Cisco Packet Tracer:
•	Počítače a tlačiareň sú pripojené k switchom cez copper straight-through káble.
•	Switch a router sú prepojené cez copper cross-over káble.
•	Routery medzi sebou spojené cez sériové rozhrania (Serial0/3/0) pomocou serial DCE kábla.

2. Nastavenie IP adries
Na routeroch som nastavil nasledovné IP adresy:
•	Router R1 (lokálna sieť):
o	FastEthernet0/0: 192.168.1.1/24
o	Serial0/3/0: 10.1.1.1
o	Nastavil som DHCP pre sieť 192.168.1.0 na automatické pripojenie zariadení.
•	Router R2 (vzdialená sieť):
o	FastEthernet0/0: 192.168.2.1/24
o	Serial0/3/0: 10.1.1.2
o	DHCP pre sieť 192.168.2.0 na automatické pripojenie zariadení.

4. Konfigurácia GRE tunela
GRE tunel sa vytvoril na oboch routeroch:

•	Na R1:
o	Rozhranie Tunnel0: 172.16.1.1
o	Tunnel source: Serial0/3/0
o	Tunnel destination: 10.1.1.2

•	Na R2:
o	Rozhranie Tunnel0: 172.16.1.2
o	Tunnel source: Serial0/3/0
o	Tunnel destination: 10.1.1.1

Tento tunel umožní prenos dát medzi lokálnou a vzdialenou sieťou cez špeciálny kanál.

6. Konfigurácia switchov
Na switchoch v oboch sieťach som nastavil porty na režim "access", aby zariadenia pripojené k switchom mohli komunikovať so sieťou.

Problémy a riešenia
•	Nešifrovaný prenos: GRE tunel v Cisco Packet Tracer neposkytuje šifrovanie. Preto sú dáta prenášané nešifrovane, čo môže byť bezpečnostné riziko.
•	IPsec: V reálnom prostredí by sa mal použiť IPsec pre šifrovanie a autentifikáciu, no mne sa v projekte túto technológiu nepodarilo nakonfigurovať.

Bezpečnostné riziká:
•	Nešifrovaný prenos: Dátové prenosy cez GRE tunel nie sú šifrované, čo umožňuje riziko odpočúvania a zneužitia informácií.
•	Útoky typu Man-in-the-Middle: Útočník môže zachytiť a upravit komunikáciu, ak neexistuje adekvátne zabezpečenie.

Odporúčania:
•	Použiť IPsec pre šifrovanie a autentifikáciu v reálnych aplikáciách.
•	Zabezpečiť autentifikáciu zariadení pomocou digitálnych certifikátov.

Záver
Projekt preukázal, ako nastaviť VPN sieť medzi dvoma sieťami pomocou GRE tunelu v Cisco Packet Traceri. 
Aj keď GRE umožňuje jednoduchú komunikáciu medzi sieťami, v reálnom prostredí je dôležité implementovať 
šifrovanie a autentifikáciu, aby sa zabezpečila bezpečnosť prenosu dát. Vypracovanie tohto projektu 
pre mňa poskytlo základy pre pochopenie VPN technológie a tunelovania dát cez nešifrované kanály.
