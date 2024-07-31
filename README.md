# Mapeo

This project is designed to facilitate mapping and data visualization for the Universidad Centroamericana (UCA) routing data using OpenStreetMap. It includes a backend service for routing using the OSRM (Open Source Routing Machine) and integrates with a mobile app for route planning and navigation.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Endpoint](#endpoint)

## Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://www.docker.com/products/docker-desktop) (for containerization)
- [Git](https://git-scm.com/downloads) (for cloning the repository)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Vive-la-UCA/mapeo.git
cd mapeo
```

2. Pull the OSRM Docker image:

```bash
docker pull osrm/osrm-backend
```

3. Run the OSRM backend service:

```bash
sudo docker run -d --restart unless-stopped --name osrm-routing --network webservices -v /docker/routing_uca/MapeoUCA:/data osrm/osrm-backend osrm-routed --algorithm mld /data/mapaUCA.osrm
```

This command runs the OSRM routing service in a Docker container, using the Multi-Level Dijkstra (MLD) algorithm and the provided OpenStreetMap data for UCA.

## Usage

Once the OSRM backend service is running, it can be used by the mobile app to provide routing services. The backend service exposes endpoints for route calculation, which the mobile app can call to get directions.

## Endpoint

The endpoint that we are using in our application requires the `start` and `end` points as coordinates `longitude,latitude`. So we can use the following endpoint as example.

Here is the start point `-89.21819,13.69294` and here the end point `end = -89.20309,13.69337`.

And to make a request it's like that:

```
{{url}}/route/v1/foot/{start};{end}?geometries=geojson
```

Now using the values on the query

```
{{url}}/route/v1/foot/-89.21819,13.69294;-89.20309,13.69337?geometries=geojson
```
