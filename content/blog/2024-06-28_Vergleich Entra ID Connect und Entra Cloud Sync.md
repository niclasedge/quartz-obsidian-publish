---
title: Vergleich Entra ID
description: description
authors: niclasedge
images:
- default.png
tags:
- azure
toc_max_heading_level: 5
created: 28.06.2024
---

## Feature-Vergleich zwischen Microsoft Entra Connect und Entra Cloud Sync

### **Microsoft Entra Connect**

**Funktionen:**
- **Synchronisierung von Identitätsdaten:** Synchronisiert Benutzer, Gruppen und Kontakte zwischen der lokalen Umgebung und Microsoft Entra ID (ehemals Azure AD)[1].
- **Kennworthashsynchronisierung:** Synchronisiert Passwort-Hashes, sodass Benutzer sich mit denselben Anmeldedaten sowohl lokal als auch in der Cloud anmelden können[2].
- **Passthrough-Authentifizierung:** Ermöglicht Benutzern die Authentifizierung mit ihren lokalen Anmeldeinformationen, ohne dass Kennworthashes in die Cloud synchronisiert werden müssen[3].
- **Rückschreiben:** Unterstützt das Rückschreiben von Kennwörtern und Geräten in die lokale AD-Umgebung[3].
- **Erweiterte Filterung:** Ermöglicht die Anpassung der Synchronisierung durch Filtern von Objekten basierend auf bestimmten Kriterien[3].
- **Staging-Modus:** Ermöglicht das Testen von Änderungen, bevor sie in die Produktionsumgebung übernommen werden[4].

**Vorteile:**
- **Umfassende Funktionalität:** Bietet eine breite Palette an Synchronisierungs- und Authentifizierungsoptionen.
- **Flexibilität:** Unterstützt sowohl einfache als auch komplexe Umgebungen durch erweiterte Konfigurationsmöglichkeiten.
- **Bewährte Technologie:** Langjährig im Einsatz und gut dokumentiert.

**Nachteile:**
- **Komplexität:** Kann für kleinere Unternehmen oder weniger erfahrene Administratoren komplex und schwer zu verwalten sein.
- **Sicherheitsrisiken:** Erfordert die Einrichtung eines speziellen Kontos mit weitreichenden Rechten, was ein potenzielles Sicherheitsrisiko darstellt[2].
- **Wartung:** Erfordert regelmäßige Updates und Wartung, um sicherzustellen, dass die Synchronisierung reibungslos funktioniert.

### **Microsoft Entra Cloud Sync**

**Funktionen:**
- **Cloudbasierte Synchronisierung:** Synchronisiert Benutzer, Gruppen und Kontakte zwischen der lokalen Umgebung und Microsoft Entra ID mithilfe eines Cloudbereitstellungs-Agents[1].
- **Gruppenrückschreiben:** Unterstützt das Rückschreiben von Gruppen in die lokale AD-Umgebung[5].
- **Exchange-Hybrid-Unterstützung:** Unterstützt Exchange-Hybridszenarien, um eine nahtlose Integration von lokalen und Cloud-basierten Exchange-Diensten zu ermöglichen[6].
- **Einfache Installation und Konfiguration:** Erfordert keine dedizierte Serverinstallation und kann auf bestehenden Servern installiert werden[6].

**Vorteile:**
- **Einfachheit:** Einfachere Installation und Konfiguration im Vergleich zu Entra Connect.
- **Weniger Wartung:** Da die Synchronisierung cloudbasiert ist, erfordert sie weniger Wartung und Updates.
- **Sicherheit:** Reduziert potenzielle Sicherheitsrisiken, da keine speziellen Konten mit weitreichenden Rechten erforderlich sind.

**Nachteile:**
- **Eingeschränkte Funktionalität:** Unterstützt nicht alle Funktionen von Entra Connect, wie z.B. das Rückschreiben von „ms-ds-consistencyGUID“ für Objekte[6].
- **Keine Staging-Server-Unterstützung:** Unterstützt keine Staging-Server, was das Testen von Änderungen erschwert[6].
- **Eingeschränkte Filteroptionen:** Bietet weniger erweiterte Filtermöglichkeiten im Vergleich zu Entra Connect.

## Empfehlung: Sollten Kunden umsteigen?

**Wann ein Umstieg sinnvoll ist:**
- **Einfachheit und geringere Wartung:** Wenn ein Unternehmen eine einfachere Lösung mit weniger Wartungsaufwand sucht, könnte Entra Cloud Sync die bessere Wahl sein.
- **Sicherheitsbedenken:** Unternehmen, die Sicherheitsbedenken hinsichtlich der weitreichenden Rechte von Entra Connect haben, könnten von der sichereren Architektur von Cloud Sync profitieren.

**Wann ein Umstieg nicht sinnvoll ist:**
- **Erweiterte Anforderungen:** Wenn ein Unternehmen erweiterte Synchronisierungs- und Authentifizierungsfunktionen benötigt, die nur von Entra Connect unterstützt werden, sollte es bei Entra Connect bleiben.
- **Komplexe Umgebungen:** Für Unternehmen mit komplexen Umgebungen und spezifischen Anforderungen an die Synchronisierung und Authentifizierung bietet Entra Connect mehr Flexibilität und Anpassungsmöglichkeiten.

Insgesamt hängt die Entscheidung vom spezifischen Bedarf und den Ressourcen des Unternehmens ab. Unternehmen sollten die Vor- und Nachteile beider Lösungen sorgfältig abwägen, bevor sie eine Entscheidung treffen.

Citations:
[1] https://learn.microsoft.com/de-de/entra/identity/hybrid/connect/how-to-connect-sync-whatis
[2] https://www.prosec-networks.com/blog/microsoft-entra-connect-azure-ad-connect-vor-hackern-schuetzen/
[3] https://learn.microsoft.com/de-de/entra/identity/hybrid/connect/how-to-connect-install-roadmap
[4] https://learn.microsoft.com/de-de/entra/identity/hybrid/connect/concept-azure-ad-connect-sync-architecture
[5] https://learn.microsoft.com/de-de/entra/identity/hybrid/group-writeback-cloud-sync
[6] https://learn.microsoft.com/de-de/entra/identity/hybrid/cloud-sync/reference-cloud-sync-faq