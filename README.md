# smart-secure-edge-esp32
# IoT-Security-Gadget-ESP32

An enterprise-grade, hardware-resilient IoT smart security ecosystem featuring a decentralized ESP32 sensing edge node, custom Tasmota operational profiles, and a real-time cross-platform Ionic/JavaScript mobile application client.

---

## System Architecture & Data Flow

The physical and digital ecosystem of this project operates through a decoupled, asynchronous Publish/Subscribe model utilizing an on-premise hardware edge node, an isolated MQTT cloud broker, and a mobile client dashboard.

```text
  +--------------------------------------------------------------+
  |                      HARDWARE EDGE NODE                      |
  |                                                              |
  |  [PIR Motion Sensor]                                         |
  |         |                                                    |
  |         v (Hardware Interrupt Trigger on GPIO Pin)           |
  |  [ESP32 Microcontroller (Running Custom Tasmota Firmware)]   |
  |         |                                                    |
  |         +---> [Auxiliary 5V USB Rail] ---> (Powers Router)   |
  |         |                                                    |
  |         +---> [Internal Rechargeable Battery] (Failover Power)|
  +---------|----------------------------------------------------+
            |
            v (Asynchronous Publish Payload over Wi-Fi/WebSockets)
  +--------------------------------------------------------------+
  |               EXTERNAL MQTT CLOUD BROKER LAYER               |
  |                                                              |
  |   Topic Base: tele/security_node/ALARM                       |
  |   Payload JSON: {"status": "unauthorized_entry"}            |
  +---------|----------------------------------------------------+
            |
            +---------------------------+
            |                           |
            v (MQTT Subscription)       v (Upstream Event Webhook)
  +-----------------------+   +----------------------------------+
  |  CROSS-PLATFORM APP   |   |     ALERT SERVER PLATFORM        |
  |                       |   |                                  |
  | [Ionic App Interface] |   | [Automated Voice Call Execution] |
  | [Real-Time Alerts]    |   | [Emergency SMS Broadcast Layer]  |
  +-----------------------+   +----------------------------------+
