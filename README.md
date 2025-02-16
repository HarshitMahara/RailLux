# RailLux

## 📌 Project Overview

This project is designed to monitor light levels on railway tracks using sensors. Each pit contains multiple sections, and each section is equipped with 10 sensors. The system stores real-time sensor data in **InfluxDB** and provides a frontend interface to visualize and analyze light conditions.

### 🚧 Problem Statement

Railway maintenance requires sufficient lighting. If light levels fall below **100 lux**, work cannot proceed. This system helps railway operators monitor light conditions in real-time to ensure safety and efficiency.

## 🔧 Technology Stack

- **Backend**: Node.js, Express.js
- **Database**: InfluxDB (for real-time time-series data)
- **Frontend**: React.js with Tailwind CSS
- **Containerization**: Docker (optional)

## 🏗 Project Structure

```
├── backend
│   ├── server.js  # Express server fetching data from InfluxDB
│   ├── influx.js  # InfluxDB connection and query functions
│   ├── routes
│   │   ├── sensorRoutes.js  # API endpoints for retrieving sensor data
│   ├── package.json  # Node.js dependencies
├── frontend
│   ├── src
│   │   ├── components
│   │   ├── pages
│   │   ├── App.js  # Main React component
│   │   ├── index.js  # React entry point
│   ├── tailwind.config.js  # Tailwind CSS config
├── influxdb
│   ├── data.lp  # Line protocol file for sensor data
├── docker-compose.yml  # Optional for running InfluxDB via Docker
├── README.md  # Project documentation
```

## 🗄 InfluxDB Data Structure

### **Measurement**: `sensor_data`

| Field       | Type    | Description                     |
| ----------- | ------- | ------------------------------- |
| `lux_value` | Integer | Measured light intensity in lux |

### **Tags**

| Tag Key      | Description                           |
| ------------ | ------------------------------------- |
| `pit_id`     | Identifies the pit                    |
| `section_id` | Identifies the section within the pit |
| `sensor_id`  | Unique sensor identifier              |

### **Example Data Entry (Line Protocol Format)**

```plaintext
sensor_data,pit_id=1,section_id=A,sensor_id=101 lux_value=95
sensor_data,pit_id=2,section_id=B,sensor_id=205 lux_value=110
```

## 🚀 Installation Guide

### *1️⃣ Install InfluxDB**

#### **Using Docker (Recommended)**

```bash
docker run -p 8086:8086 -v $PWD:/var/lib/influxdb influxdb
```

#### **Manual Installation**

- Download and install InfluxDB from [InfluxData](https://portal.influxdata.com/downloads/)
- Start the InfluxDB service

### **2️⃣ Set Up InfluxDB**

```bash
influx setup --bucket railway_data --org railway_org --username admin --password admin123 --retention 30d
```

### **3️⃣ Insert Sample Data**

Run the following command to insert sensor data:

```bash
influx write --bucket railway_data --precision s --org railway_org --token YOUR_TOKEN -f influxdb/data.lp
```

### **4️⃣ Run Backend**

```bash
cd backend
npm install
node server.js
```

### **5️⃣ Run Frontend**

```bash
cd frontend
npm install
npm start
```

## 🎨 Frontend Features

- **Dashboard**: Displays real-time light data for all pits and sections
- **Alerts**: Highlights areas where lux levels drop below 100
- **Historical Data**: Allows users to view light intensity trends over time

## 📜 API Endpoints

| Method | Endpoint                           | Description                     |
| ------ | ---------------------------------- | ------------------------------- |
| `GET`  | `/api/sensors`                     | Get all sensor data             |
| `GET`  | `/api/sensors/:pit_id`             | Get data for a specific pit     |
| `GET`  | `/api/sensors/:pit_id/:section_id` | Get data for a specific section |

## 🛠 Future Enhancements

- **User Authentication**
- **Graphical Visualizations**
- **SMS/Email Alerts for Low Lux Levels**


