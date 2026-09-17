# Power ⚡

> **An advanced Flutter application for managing and tracking MikroTik networks, monitoring modem status, and drawing network topology on an interactive map.**

## 📌 About The Project
**Power** is a professional networking tool designed for network administrators and service providers. The app enables automatic local discovery of connected network devices, plots their geographical locations on a map, and monitors link statuses between towers and equipment in real-time. With a modern and intuitive interface, it simplifies infrastructure management and ensures rapid fault detection.

## 🚀 Key Features
* **🗺️ Interactive Network Topology Map:** Draw links between towers and equipment directly on the map. Links change color dynamically (green for online, red for offline) based on endpoint connection statuses.
* **📡 Auto-Discovery:** Automatically capture new, unplaced devices via the MNDP (MikroTik Neighbor Discovery Protocol) and display them in a floating window.
* **📍 Drag & Drop:** A smart feature that allows you to drag any unplaced device from the list and drop it onto a specific point on the map to instantly register its geographical coordinates.
* **⚡ Real-time Monitoring & Filtering:** Quick filters to view Online, Offline, or Maintenance devices, paired with a periodic 10-second cleanup timer to continuously evaluate device connection states.
* **📱 Modern UI:** Built with `Material 3` design principles, featuring bottom sheets that display precise details for towers and equipment (Address, IP, Coordinates, Connected Devices).

## 🛠️ Tech Stack

**Frontend & State Management:**
* **Framework:** Flutter (Dart SDK ^3.13.2)
* **State Management:** Riverpod (`flutter_riverpod`)
* **Routing:** `go_router`
* **Storage & Security:** `shared_preferences` & `flutter_secure_storage`
* **Localization:** `flutter_localizations` & `intl`

**Backend & Database:**
* **Firebase Core & Cloud Firestore:** For storing network tower/equipment data and link statuses.
* **Firebase Auth:** For user authentication and access management.

**Maps & Location:**
* **Map Engine:** `flutter_map` with support for switching between standard mode (OpenStreetMap) and satellite mode (ArcGIS World Imagery).
* **Coordinate Processing:** `latlong2`

**Networking & MikroTik Protocols:**
* **MNDP Service:** A custom service listening to the MikroTik Neighbor Discovery Protocol via `UDP port 5678` to fetch local devices.
* **MikroTik API:** Direct connection with RouterOS via `MikrotikApiService` to control devices and fetch neighbor data.

## ⚙️ Getting Started

To run the project on your local environment, follow these steps:

**1. Clone the repository:**
Clone the repo to your local machine and navigate into the project directory.

**2. Install dependencies:**
```bash
flutter clean
flutter pub get
