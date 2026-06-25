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

<img width="751" height="522" alt="Active Directory" src="https://github.com/user-attachments/assets/03132a86-e44a-4cc7-832d-b08cfb8d61a9" />

### 2. Konfiguracja Obiektów Zasad Grupy (GPO)
* **Mapowanie dysków sieciowych (User Configuration):** Automatyczne podłączanie zasobów udostępnionych (Dysk Z: "Dane") podczas logowania użytkownika.
* **Branding Firmowy:** Wymuszenie ujednoliconej tapety na stacjach roboczych bez możliwości zmiany przez pracownika.
* **Restrykcje Bezpieczeństwa:** Blokada dostępu do Panelu Sterowania i Ustawień systemu Windows dla kont nieuprzywilejowanych.

<img width="749" height="524" alt="Group Polisy Object" src="https://github.com/user-attachments/assets/18c9e98f-c7ac-4457-b4de-4ac04c6c9b14" />


### 3. Weryfikacja i Troubleshooting
* Testowanie wdrożonych polityk z poziomu klienta i serwera.
* Biegłe wykorzystanie narzędzi wiersza poleceń do diagnostyki: `gpupdate /force`, `gpresult`, `whoami`.
* Symulacja resetowania uprawnień i rozwiązywania konfliktów logowania.

<p align="center">
  <img width="45%" alt="gpresult" src="https://github.com/user-attachments/assets/efb6fc71-f2d1-4d3f-969c-ada418d98a3d" />
  <img width="45%" alt="zmapowany dysk Z" src="https://github.com/user-attachments/assets/53361cab-7103-42d1-9441-955e4d3c98eb" />
</p>


### 4. Zdalne Zarządzanie i Monitoring (Action1 RMM)
* **Automatyczne wdrażanie oprogramowania:** Skonfigurowanie polityki GPO (`Software Installation`) w sekcji komputerowej, co pozwoliło na w pełni automatyczną instalację agenta Action1 na stacjach roboczych w tle, bez konieczności ręcznego klikania instalatora na każdym komputerze.
* **Centralny nadzór:** Przygotowanie infrastruktury pod zdalne zarządzanie aplikacjami oraz monitorowanie stanu technicznego maszyn z poziomu jednego panelu w chmurze.

<p align="center">
  <img width="45%"  alt="GPO" src="https://github.com/user-attachments/assets/39d57c86-5e20-47fe-9c29-cb52db9dcfef" />
  <img width="45%"  alt="Panel Action1" src="https://github.com/user-attachments/assets/da54cc8a-5bb5-46de-a816-13d2d7513eae" />
</p>


### 5. Obsługa Zgłoszeń i Procesy ITSM (Jira Service Desk)
* **Zarządzanie cyklem życia incydentów:** Konfiguracja tablicy Kanban w systemie Jira (projekt *HomeLab*) w celu kategoryzacji, przypisywania i mapowania zgłoszeń użytkowników końcowych zgodnie z praktykami Help Desk.
* **Symulacja zgłoszeń L1/L2:** Praktyczne procesowanie codziennych incydentów wsparcia technicznego, takich jak procedury resetowania haseł (*Reset password*), odblokowywanie kont w Active Directory (*Unlock account*) oraz pełna dokumentacja techniczna rozwiązanych awarii.

<img width="100%" alt="Paneel Jira" src="https://github.com/user-attachments/assets/5b42f4b5-97bc-40d8-948c-3d333d931528" />



### 6. Case Study: Diagnoza i Rozwiązanie Problemu z Dostępem Sieciowym
Podczas automatycznego wdrażania agenta Action1 przez GPO, system Windows 11 zaraportował błąd: *"The installation source for this product is not available"*. Proces udanego troubleshootingu objął:
* **Analizę uprawnień maszynowych:** Identyfikację, że instalator GPO uruchamia się na prawach konta systemowego komputera, a nie zalogowanego użytkownika.
* **Konfigurację zabezpieczeń folderu:** Rozdzielenie uprawnień na poziomie sieciowym (**Share Permissions:** dodano grupę `Everyone` z prawem odczytu) oraz lokalnym (**NTFS Security:** przypisano dedykowane prawa odczytu i wykonania dla grupy `Domain Computers`).
* **Optymalizację ścieżki UNC:** Zmianę mapowania pakietu `.msi` w GPO z nazwy hosta na bezpośredni adres IP (`\\192.168.10.10\deploy`), co wyeliminowało błędy komunikacji z serwerem DNS podczas wczesnej fazy rozruchu systemu operacyjnego.

<img width="100%" alt="Raport błędu" src="https://github.com/user-attachments/assets/50d43d86-8317-4945-bb03-a48133f307e6" />






