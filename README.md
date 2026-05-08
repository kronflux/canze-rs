# 🚗 canze-rs

## How it works
![Hardware overview](images/canze-rs.webp)

## Description
This small linux tool is intended to connect to Renault Zoe's CAN bus via a Bluetooth ELM327 OBD2 adapter and push live battery telemetry data to a local REST endpoint (designed to integrate with `aa-proxy-rs`).<br>
The of the project is inspired by (and a tribute to) a great [CanZE](https://canze.fisch.lu/) project.<br>

#### Supported Vehicles:
- Hyundai Ioniq 5
- Kia EV6

#### This tool polls and transmits the following parameters:
- SOC (State of Charge)
- External Temperature

It is intended to be orchestrated by the `aa-proxy-rs` daemon. When an Android Auto session begins, it connects to the OBD dongle and transmits the collected battery data via HTTP POST to `http://localhost/ev-battery-data`, which fulfills the telemetry requirements needed for Android Auto EV Routing.

## Usage
```
canze-rs 0.1.0
Renault Zoe EV battery data telemetry logger

USAGE:
    canze-rs [OPTIONS]

OPTIONS:
    -c, --config <CONFIG>    Config file path [default: /etc/canze-rs.conf]
    -d, --debug              Enable debug info
    -h, --help               Print help information
    -V, --version            Print version information
```

## Config
The project uses a simple configuration file:<br>
`/etc/canze-rs.conf`<br>

A sample file should have the following contents:<br>
```
[general]
mac = 00:00:00:00:00:00  # Enter your Bluetooth OBD2 Dongle MAC here
car = ev6                # Options: 'ev6' or 'ioniq'
```