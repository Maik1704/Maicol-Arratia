# 🔥 Configuración Avanzada de DHCP y DNS en Cisco Packet Tracer

Este documento explica cómo configurar **DHCP y DNS en Cisco Packet Tracer** utilizando **3 PCs, 1 switch, 1 router y 2 servidores** (uno para DHCP y otro para DNS). Además, cada PC tendrá su propio nombre DNS.

---

## 📌 Dispositivos y Conexiones
### 🛠 **Dispositivos utilizados:**
- **1 Router**
- **1 Switch**
- **2 Servidores** (uno para DHCP y otro para DNS)
- **3 PCs**

### 🔌 **Conexiones (Cable "Copper Straight-Through")**
- **Router (GigabitEthernet0/0) → Switch (FastEthernet0/1)**
- **Servidor DHCP (FastEthernet0) → Switch (FastEthernet0/2)**
- **Servidor DNS (FastEthernet0) → Switch (FastEthernet0/3)**
- **PC1 (FastEthernet0) → Switch (FastEthernet0/4)**
- **PC2 (FastEthernet0) → Switch (FastEthernet0/5)**
- **PC3 (FastEthernet0) → Switch (FastEthernet0/6)**

---

## 🌐 **Configuración de Direcciones IP**
### **Esquema de Red**
- **Router:** `192.168.1.1`
- **Servidor DHCP:** `192.168.1.2`
- **Servidor DNS:** `192.168.1.3`
- **PCs:** Recibirán IP dinámica desde el servidor DHCP

---

## 🚀 **Paso 1: Configurar el Router**
```bash
enable
configure terminal
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
write memory
```

---

## 🔑 **Paso 2: Configurar el Servidor DHCP**
1. Ir a **Config → FastEthernet0**
2. **Asignar IP estática:**
   - **IP Address:** `192.168.1.2`
   - **Subnet Mask:** `255.255.255.0`
   - **Gateway:** `192.168.1.1`
3. Ir a **Services → DHCP**
4. Activar servicio DHCP (`ON`)
5. Completar los datos:
   - **Pool Name:** `Red1`
   - **Default Gateway:** `192.168.1.1`
   - **DNS Server:** `192.168.1.3`
   - **Start IP Address:** `192.168.1.10`
   - **Subnet Mask:** `255.255.255.0`
   - **Max Users:** `100`
6. Guardar configuración (`Save`)

---

## 🌍 **Paso 3: Configurar el Servidor DNS**
1. Ir a **Config → FastEthernet0**
2. **Asignar IP estática:**
   - **IP Address:** `192.168.1.3`
   - **Subnet Mask:** `255.255.255.0`
   - **Gateway:** `192.168.1.1`
3. Ir a **Services → DNS**
4. Activar servicio DNS (`ON`)
5. Agregar registros:
   - **PC1:** `pc1.miempresa.com` → `192.168.1.10`
   - **PC2:** `pc2.miempresa.com` → `192.168.1.11`
   - **PC3:** `pc3.miempresa.com` → `192.168.1.12`
6. Guardar configuración (`Add`)

---

## 💻 **Paso 4: Configurar las PCs (IP Automática)**
1. Ir a **Desktop → IP Configuration** en cada PC
2. Seleccionar **DHCP**
3. Revisar que haya recibido una **IP en el rango 192.168.1.10+** con `ipconfig`

---

## 🔍 **Paso 5: Pruebas Finales**
📌 **Verificar conectividad (PING)**
```bash
ping 192.168.1.3  # Ping al servidor DNS
ping 192.168.1.2  # Ping al servidor DHCP
```
📌 **Probar resolución DNS (NSLOOKUP)**
```bash
nslookup pc2.miempresa.com
```

---

## 🎯 **Resumen**
✔ **DHCP funciona:** PCs reciben IP automáticamente.
✔ **DNS funciona:** Cada PC tiene su propio nombre (`pc1.miempresa.com`, `pc2.miempresa.com`, etc.).
✔ **Conexión establecida:** Ping entre dispositivos exitoso.

🚀 **¡Configuración completa en Packet Tracer!**
