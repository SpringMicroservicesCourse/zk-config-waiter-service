# ZooKeeper 配置服務的咖啡廳服務員系統 ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.0.2-blue.svg)](https://spring.io/projects/spring-cloud)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

這是一個基於 Spring Boot 和 Spring Cloud 的微服務應用程式，展示如何使用 **ZooKeeper** 作為配置中心來管理服務配置。該系統模擬了一個咖啡廳的服務員系統，提供咖啡訂單管理功能，並整合了完整的微服務生態系統。

### 核心功能
- **咖啡管理**: 新增、查詢、批次匯入咖啡品項
- **訂單管理**: 建立、查詢、狀態更新咖啡訂單
- **配置管理**: 使用 ZooKeeper 進行動態配置管理
- **服務發現**: 整合 Consul 進行服務註冊與發現
- **韌性工程**: 整合 Resilience4j 提供熔斷器和限流功能
- **監控指標**: 整合 Prometheus 進行指標收集

### 解決的問題
- 微服務配置管理的複雜性
- 配置變更需要重啟服務的問題
- 服務間通訊的可靠性
- 系統監控和可觀測性

> 💡 **為什麼選擇 ZooKeeper 作為配置中心？**
> - **即時配置更新**: 透過 ZooKeeper 的監聽機制，配置變更可即時推送到應用程式
> - **高可用性**: ZooKeeper 提供分散式協調服務，確保配置服務的可靠性
> - **一致性保證**: 提供強一致性保證，避免配置不一致問題
> - **與服務發現整合**: 可與現有的 ZooKeeper 服務發現機制整合

### 🎯 專案特色

- **🔄 動態配置更新**: 無需重啟應用程式即可更新配置
- **🛡️ 韌性工程**: 整合熔斷器、限流器保護服務
- **📊 完整監控**: 提供健康檢查、指標收集等監控功能
- **⚡ 高效能**: 使用快取機制提升系統效能
- **🔧 易於維護**: 清晰的程式碼結構和詳細註解

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 應用程式框架，提供自動配置和內嵌伺服器
- **Spring Cloud 2024.0.2** - 微服務框架，提供服務發現、配置管理等功能
- **Spring Data JPA** - 資料存取層，簡化資料庫操作
- **Spring Cache** - 快取框架，提升系統效能

### 微服務組件
- **Spring Cloud Bootstrap** - 配置載入機制
- **Spring Cloud Consul Discovery** - 服務註冊與發現
- **Spring Cloud ZooKeeper Config** - ZooKeeper 配置中心整合

### 韌性工程
- **Resilience4j** - 熔斷器、限流器、重試機制
- **Micrometer** - 指標收集和監控

### 開發工具與輔助
- **Lombok** - 程式碼生成工具，減少樣板程式碼
- **Joda Money** - 金融數值處理套件
- **Apache Commons Lang3** - 工具類庫
- **H2 Database** - 記憶體資料庫（開發測試用）

## 專案結構

```
zk-config-waiter-service/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── tw/fengqing/spring/springbucks/waiter/
│   │   │       ├── controller/          # REST API 控制器
│   │   │       │   ├── CoffeeController.java
│   │   │       │   ├── CoffeeOrderController.java
│   │   │       │   ├── PerformanceInteceptor.java
│   │   │       │   └── request/         # 請求物件
│   │   │       ├── model/               # 資料模型
│   │   │       │   ├── BaseEntity.java
│   │   │       │   ├── Coffee.java
│   │   │       │   ├── CoffeeOrder.java
│   │   │       │   ├── OrderState.java
│   │   │       │   └── MoneyConverter.java
│   │   │       ├── repository/          # 資料存取層
│   │   │       │   ├── CoffeeRepository.java
│   │   │       │   └── CoffeeOrderRepository.java
│   │   │       ├── service/             # 業務邏輯層
│   │   │       │   ├── CoffeeService.java
│   │   │       │   └── CoffeeOrderService.java
│   │   │       └── support/             # 支援類別
│   │   │           ├── CoffeeIndicator.java
│   │   │           ├── OrderProperties.java
│   │   │           ├── MoneySerializer.java
│   │   │           ├── MoneyDeserializer.java
│   │   │           └── MoneyFormatter.java
│   │   └── resources/
│   │       ├── application.properties   # 應用程式配置
│   │       ├── bootstrap.properties     # Bootstrap 配置
│   │       ├── schema.sql              # 資料庫結構
│   │       ├── data.sql                # 初始資料
│   │       └── coffee.txt              # 咖啡資料檔案
│   └── test/
│       └── java/
│           └── tw/fengqing/spring/springbucks/waiter/
│               └── WaiterServiceApplicationTests.java
├── pom.xml
└── README.md
```

## 快速開始

### 前置需求
- **Java 21+** - 確保已安裝 JDK 21 或更高版本
- **Maven 3.6+** - 用於專案建置和依賴管理
- **ZooKeeper 3.8+** - 配置中心服務
- **Consul 1.15+** - 服務註冊與發現
- **Docker** - 可選，用於快速啟動服務

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/zk-config-waiter-service.git
```

2. **進入專案目錄：**
```bash
cd zk-config-waiter-service
```

3. **啟動 ZooKeeper 服務：**
```bash
# 使用 Docker 快速啟動
docker run -d --name zookeeper -p 2181:2181 zookeeper:3.8

# 或使用本地安裝的 ZooKeeper
zkServer.sh start
```

4. **啟動 Consul 服務：**
```bash
# 使用 Docker 快速啟動
docker run -d --name consul -p 8500:8500 consul:1.15

# 或使用本地安裝的 Consul
consul agent -dev
```

5. **配置 ZooKeeper 節點：**
```bash
# 連接到 ZooKeeper
zkCli.sh -server localhost:2181

# 建立配置節點
create /config/waiter-service/order.discount 60
create /config/waiter-service/order.waiter-prefix springbucks-

# 免刷新更新配置節點
set /config/waiter-service/order.discount 30

```

6. **編譯專案：**
```bash
mvn clean compile
```

7. **執行應用程式：**
```bash
mvn spring-boot:run
```

## 進階說明

### 環境變數
```properties
# ZooKeeper 配置
SPRING_CLOUD_ZOOKEEPER_CONNECT_STRING=localhost:2181
SPRING_CLOUD_ZOOKEEPER_CONFIG_ENABLED=true

# Consul 配置
SPRING_CLOUD_CONSUL_HOST=localhost
SPRING_CLOUD_CONSUL_PORT=8500

# 應用程式配置
SERVER_PORT=8080
ORDER_DISCOUNT=95
```

### 設定檔說明

#### bootstrap.properties
```properties
# 應用程式名稱
spring.application.name=waiter-service

# ZooKeeper 連接配置
spring.cloud.zookeeper.connect-string=localhost:2181
spring.cloud.zookeeper.config.enabled=true
spring.cloud.zookeeper.config.root=/config
spring.cloud.zookeeper.config.default-context=application
spring.cloud.zookeeper.config.profile-separator=,
```

#### application.properties
```properties
# 資料庫配置
spring.jpa.hibernate.ddl-auto=none
spring.jpa.properties.hibernate.show_sql=true
spring.jpa.properties.hibernate.format_sql=true

# 監控端點配置
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always

# 服務發現配置
spring.cloud.consul.host=localhost
spring.cloud.consul.port=8500
spring.cloud.consul.discovery.prefer-ip-address=true

# 韌性工程配置
resilience4j.ratelimiter.instances.coffee.limit-for-period=5
resilience4j.ratelimiter.instances.coffee.limit-refresh-period=30000
resilience4j.ratelimiter.instances.order.limit-for-period=3
resilience4j.ratelimiter.instances.order.limit-refresh-period=30000
```

### API 端點

#### 咖啡管理 API
```bash
# 取得所有咖啡
GET /coffee/

# 取得指定咖啡
GET /coffee/{id}

# 依名稱查詢咖啡
GET /coffee/?name={name}

# 新增咖啡 (JSON)
POST /coffee/
Content-Type: application/json
{
  "name": "espresso",
  "price": 100.00
}

# 批次新增咖啡 (Multipart)
POST /coffee/
Content-Type: multipart/form-data
file: coffee.txt
```

#### 訂單管理 API
```bash
# 取得訂單
GET /order/{id}

# 建立訂單
POST /order/
Content-Type: application/json
{
  "customer": "張三",
  "items": ["espresso", "latte"]
}
```

#### 監控端點
```bash
# 健康檢查
GET /actuator/health

# 指標資訊
GET /actuator/metrics

# Prometheus 指標
GET /actuator/prometheus

# 應用程式資訊
GET /actuator/info
```

## 韌性工程配置

### 限流器設定
```properties
# Coffee API 限流配置
resilience4j.ratelimiter.instances.coffee.limit-for-period=5
resilience4j.ratelimiter.instances.coffee.limit-refresh-period=30000
resilience4j.ratelimiter.instances.coffee.timeout-duration=5000

# Order API 限流配置
resilience4j.ratelimiter.instances.order.limit-for-period=3
resilience4j.ratelimiter.instances.order.limit-refresh-period=30000
resilience4j.ratelimiter.instances.order.timeout-duration=1000
```

### 熔斷器設定
```properties
# 熔斷器配置範例
resilience4j.circuitbreaker.instances.coffee-service.sliding-window-size=10
resilience4j.circuitbreaker.instances.coffee-service.failure-rate-threshold=50
resilience4j.circuitbreaker.instances.coffee-service.wait-duration-in-open-state=5000
```

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Spring Cloud 官方文件](https://spring.io/projects/spring-cloud)
- [ZooKeeper 官方文件](https://zookeeper.apache.org/)
- [Consul 官方文件](https://www.consul.io/)
- [Resilience4j 官方文件](https://resilience4j.readme.io/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 配置管理 | ZooKeeper 節點結構 | 使用 `/config/{application}/{profile}` 結構 |
| 服務發現 | Consul 註冊 | 確保服務名稱唯一性 |
| 資料庫連線 | H2 記憶體資料庫 | 生產環境使用正式資料庫 |
| 監控指標 | Prometheus 收集 | 定期檢查指標資料 |

### 🔒 最佳實踐指南

- **配置管理**: 使用 ZooKeeper 的監聽機制實現動態配置更新
- **服務保護**: 整合 Resilience4j 提供熔斷器、限流器保護
- **監控告警**: 設定適當的監控指標和告警閾值
- **程式碼品質**: 在重要程式碼區塊添加清楚註解，方便團隊成員理解與維護
- **錯誤處理**: 實作統一的錯誤處理機制
- **日誌記錄**: 使用結構化日誌記錄關鍵操作

### 🔧 開發注意事項

1. **確保 ZooKeeper 和 Consul 服務正常運行**
2. **配置檔案變更會自動重新載入**
3. **使用 `@RefreshScope` 註解支援配置熱更新**
4. **監控端點提供詳細的系統狀態資訊**
5. **使用台灣常用的專業用語，確保溝通順暢且符合本地習慣**

## 故障排除

### 常見問題

#### ZooKeeper 連接失敗
```bash
# 檢查 ZooKeeper 服務狀態
echo stat | nc localhost 2181

# 檢查連接字串配置
spring.cloud.zookeeper.connect-string=localhost:2181
```

#### Consul 註冊失敗
```bash
# 檢查 Consul 服務狀態
curl http://localhost:8500/v1/status/leader

# 檢查服務註冊
curl http://localhost:8500/v1/catalog/services
```

#### 配置載入失敗
```bash
# 檢查 ZooKeeper 節點結構
zkCli.sh -server localhost:2181
ls /config/waiter-service

# 檢查配置格式
get /config/waiter-service/order.discount
```

## 授權說明

本專案採用 MIT 授權條款，詳見 [LICENSE](LICENSE) 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025年8月31日**  
**👨‍💻 維護者：風清雲談團隊**  
**🏷️ 版本：0.0.1-SNAPSHOT**
