# Wirtualne Środowisko Korporacyjne - Active Directory & Windows Server 2022

## 📌 Opis Projektu
Projekt polega na zaprojektowaniu, wdrożeniu i konfiguracji wirtualnego środowiska domenowego. Symuluje on realną infrastrukturę IT w celu testowania polityk bezpieczeństwa (GPO), zarządzania tożsamością oraz administracji siecią. 

## 🏗️ Architektura i Technologie
* **Hypervisor:** Oracle VirtualBox
* **Serwer (Kontroler Domeny):** Windows Server 2022 (IP: 192.168.10.10)
* **Stacja Robocza (Klient):** Windows 11 Pro (IP: 192.168.10.11)
* **Sieć:** Sieć wewnętrzna (Internal Network) oraz przełącznik w trybie Bridged, własny serwer DNS.
* **Systemy Zarządzania:** Action1 RMM (Patch Management), Jira Service Desk.

## ⚙️ Zrealizowane Zadania

### 1. Zarządzanie Tożsamością (Active Directory)
* Promocja serwera do roli Kontrolera Domeny (domena: `lab.local`).
* Utworzenie struktury jednostek organizacyjnych (OU) – m.in. dział `Ksiegowosc`.
* Wdrożenie kont użytkowników (np. `jkowalski`) i przygotowanie środowiska pod nadawanie uprawnień (RBAC).

<img width="751" height="522" alt="obraz" src="https://github.com/user-attachments/assets/03132a86-e44a-4cc7-832d-b08cfb8d61a9" />

### 2. Konfiguracja Obiektów Zasad Grupy (GPO)
* **Mapowanie dysków sieciowych (User Configuration):** Automatyczne podłączanie zasobów udostępnionych (Dysk Z: "Tajne Dokumenty") podczas logowania użytkownika.
* **Branding Firmowy:** Wymuszenie ujednoliconej tapety na stacjach roboczych bez możliwości zmiany przez pracownika.
* **Restrykcje Bezpieczeństwa:** Blokada dostępu do Panelu Sterowania i Ustawień systemu Windows dla kont nieuprzywilejowanych.

<img width="749" height="524" alt="obraz" src="https://github.com/user-attachments/assets/18c9e98f-c7ac-4457-b4de-4ac04c6c9b14" />


### 3. Weryfikacja i Troubleshooting
* Testowanie wdrożonych polityk z poziomu klienta i serwera.
* Biegłe wykorzystanie narzędzi wiersza poleceń do diagnostyki: `gpupdate /force`, `gpresult`, `whoami`.
* Symulacja resetowania uprawnień i rozwiązywania konfliktów logowania.

<p align="center">
  <img width="45%" alt="obraz" src="https://github.com/user-attachments/assets/efb6fc71-f2d1-4d3f-969c-ada418d98a3d" />
  <img width="45%" alt="obraz" src="https://github.com/user-attachments/assets/53361cab-7103-42d1-9441-955e4d3c98eb" />
</p>



