<p align="center">
  <h1 align="center">Kafka distributed message middleware</h1>
  <p align="center">
    <a href="README_ZH.md"><strong>简体中文</strong></a> | <strong>English</strong>
  </p>

## Table of Contents

- [Repository Introduction](#repository-introduction)  
- [Prerequisites](#prerequisites)  
- [Image Specifications](#image-specifications)
- [Getting Help](#getting-help)
- [How to Contribute](#how-to-contribute)

## Repository Introduction  
[Apache Kafka](https://github.com/apache/kafka) is a distributed message system that supports partitions and multiple replicas based on ZooKeeper coordination.

**Core Features:**
1. Log collection: Kafka can collect logs of various services and open them to various consumers through Kafka as a unified interface service, such as Hadoop, Hbase, Solr, etc.  
2. Metrics: Kafka is also frequently used to record operational monitoring data. Including collecting data from various distributed applications, producing centralized feedback for various operations such as alarms and reports.  
3. Streaming processing: can be integrated with Spark streaming and Flink for use.  
4. Flow limiting and peak clipping: Kafka can be used to write requests to Kafka when there are too many requests at a certain time in the Internet field, so as to avoid the service crash caused by directly requesting the back-end program.  

**Architecture Design:**

![](./images/img001.png)

This project offers pre-configured [**Kafka distributed message middleware**](https://marketplace.huaweicloud.com/intl/hidden/contents/3b8c28c7-295e-493d-82ed-6c0e94a3fc8c) images with Kafka and its runtime environment pre-installed, along with deployment templates. Follow the guide to enjoy an "out-of-the-box" experience.

> **System Requirements:**
> - CPU: 2GHz or higher  
> - RAM: 4GB or more  
> - Disk: At least 40GB  

## Prerequisites  
[Register a Huawei account and activate Huawei Cloud](https://support.huaweicloud.com/usermanual-account/account_id_001.html)

## Image Specifications  

| Image Version                                                                                                      | Description                                                    | Notes |  
|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|-------|  
| [kafka3.8_HCE2.0](https://marketplace.huaweicloud.com/intl/hidden/contents/3b8c28c7-295e-493d-82ed-6c0e94a3fc8c) | Deployed on Kunpeng servers with Huawei Cloud EulerOS 2.0 64bit |  | 
| [kafka3.8_Ubuntu24.04](https://marketplace.huaweicloud.com/intl/hidden/contents/3b8c28c7-295e-493d-82ed-6c0e94a3fc8c)  | Deployed on Kunpeng servers with Ubuntu24.04 64bit        |  |  

## Getting Help
- Submit an [issue](https://github.com/HuaweiCloudDeveloper/kafka-image/issues)
- Contact Huawei Cloud Marketplace product support

## How to Contribute
- Fork this repository and submit a merge request.
- Update README.md synchronously based on your open-source mirror information.
