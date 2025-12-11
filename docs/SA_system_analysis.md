# sbar_pos 系統分析文件 (System Analysis Document)

---

## 目錄

1. [專案概述 (Project Overview)](#1-專案概述-project-overview)
2. [系統架構設計 (System Architecture)](#2-系統架構設計-system-architecture)
3. [功能需求與邏輯 (Functional Requirements)](#3-功能需求與邏輯-functional-requirements)
4. [使用者介面與體驗設計 (UI/UX Design Specifications)](#4-使用者介面與體驗設計-uiux-design-specifications)
5. [資料處理與 API 整合 (Data & API Integration)](#5-資料處理與-api-整合-data--api-integration)
6. [非功能性需求 (Non-Functional Requirements)](#6-非功能性需求-non-functional-requirements)
7. [測試計畫 (Test Plan)](#7-測試計畫-test-plan)

---

## 1. 專案概述 (Project Overview)

### 1.1 專案背景與目標 (Background & Objectives)

**專案背景**

sbar_pos 是一套專為餐飲零售業設計的 POS 銷售點管理系統。因應現代商業營運需求，本系統整合了商品銷售、會員管理、課程預約、業績分配等核心功能，旨在提供一站式的店舖營運解決方案。

**開發目標**

| 目標 | 說明 |
|------|------|
| 提升營運效率 | 透過條碼掃描、快速結帳等功能，縮短交易時間 |
| 整合會員管理 | 建立完整的會員資料庫，支援儲值金、課程購買等服務 |
| 支援課程預約 | 提供視覺化日曆系統，方便管理預約課程及排程 |
| 業績追蹤分析 | 即時追蹤銷售業績，支援員工業績分配 |
| 離線作業支援 | 本地資料庫確保網路不穩時仍可持續營運 |

**預期解決的問題**

- 傳統 POS 系統功能分散，需整合多套系統
- 會員資料管理不便，缺乏統一介面
- 課程預約流程繁瑣，缺乏視覺化排程工具
- 業績分配計算複雜，容易出錯

### 1.2 適用範圍 (Scope)

**包含功能 (In-Scope)**

| 模組 | 功能描述 |
|------|----------|
| 商品銷售 | 商品搜尋、條碼掃描、購物車管理、結帳支付 |
| 會員管理 | 會員搜尋、資料維護、歷史訂單查詢、儲值金管理 |
| 課程預約 | 課程瀏覽、預約排程、日曆管理、課程確認 |
| 業績分配 | 銷售業績追蹤、員工業績分配、報表查詢 |
| 訂單管理 | 歷史訂單查詢、退貨處理、訂單取消 |
| 庫存管理 | 商品庫存查詢與管理 |

**不包含功能 (Out-of-Scope)**

| 項目 | 說明 |
|------|------|
| 進銷存完整系統 | 僅提供基礎庫存查詢，不含採購、進貨功能 |
| 財務報表 | 不含完整財務會計報表功能 |
| 人事薪資 | 不含員工排班、薪資計算功能 |
| 電子商務 | 不支援線上購物、物流配送 |

### 1.3 目標受眾 (Target Audience)

| 角色 | 使用情境 | 主要功能 |
|------|----------|----------|
| 店員/收銀員 | 日常銷售作業 | 商品掃描、結帳、會員查詢 |
| 店長/主管 | 營運管理 | 業績查詢、訂單管理、庫存盤點 |
| 美容師/服務人員 | 課程服務 | 預約查詢、課程確認、會員服務 |

### 1.4 技術堆疊 (Tech Stack)

**核心框架**

| 項目 | 版本/規格 |
|------|-----------|
| Flutter SDK | ^3.8.1 |
| Dart SDK | ^3.8.1 |
| 支援平台 | iOS、Android |
| 設計解析度 | 1920 x 1200 (橫向) |

**狀態管理與資料層**

| 套件 | 用途 | 版本 |
|------|------|------|
| provider | 狀態管理 | ^6.0.5 |
| hive / hive_flutter | 本地 KV 儲存 | ^2.2.3 / ^1.1.0 |
| sqflite | SQLite 資料庫 | ^2.3.1 |

**網路與 API**

| 套件 | 用途 | 版本 |
|------|------|------|
| chopper | HTTP 客戶端 | ^8.0.3 |
| dio | HTTP 請求 (輔助) | ^5.7.0 |
| http | HTTP 請求 (輔助) | ^1.2.2 |
| connectivity_plus | 網路狀態監聽 | ^4.0.1 |

**UI 元件**

| 套件 | 用途 | 版本 |
|------|------|------|
| flutter_screenutil | 螢幕適配 | ^5.9.3 |
| table_calendar | 日曆元件 | ^3.0.9 |
| flutter_svg | SVG 圖片 | ^2.2.0 |
| cached_network_image | 網路圖片快取 | ^3.2.3 |
| flutter_slidable | 滑動操作 | ^3.0.0 |
| carousel_slider | 輪播元件 | ^5.0.0 |
| fluttertoast | Toast 提示 | ^8.2.8 |

**硬體整合**

| 套件 | 用途 | 版本 |
|------|------|------|
| barcode_scan2 | 條碼掃描 | ^4.5.1 |
| local_auth | 本地身份驗證 | ^2.3.0 |
| permission_handler | 權限管理 | ^11.4.0 |
| device_info_plus | 裝置資訊 | ^10.0.0 |

**分析與監控**

| 套件 | 用途 | 版本 |
|------|------|------|
| firebase_analytics | 使用分析 | ^11.5.1 |

**開發工具**

| 套件 | 用途 | 版本 |
|------|------|------|
| build_runner | 代碼生成 | ^2.4.13 |
| flutter_gen / flutter_gen_runner | 資源生成 | 5.8.0 |
| chopper_generator | API 代碼生成 | ^8.0.3 |
| hive_generator | Hive 代碼生成 | 2.0.1 |
| patrol | E2E 測試框架 | ^3.0.0 |

---

## 2. 系統架構設計 (System Architecture)

### 2.1 系[]()統架構圖 (System Architecture Diagram)

```
┌─────────────────────────────────────────────────────────────────┐
│                        sbar_pos App                             │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │                    Presentation Layer                     │  │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────────────┐ │  │
│  │  │ Screens │ │ Widgets │ │ Dialogs │ │ ViewModels      │ │  │
│  │  └────┬────┘ └────┬────┘ └────┬────┘ │(ChangeNotifier) │ │  │
│  │       │           │           │       └────────┬────────┘ │  │
│  └───────┴───────────┴───────────┴────────────────┴──────────┘  │
│                              │                                   │
│  ┌───────────────────────────▼──────────────────────────────┐  │
│  │                     State Management                      │  │
│  │  ┌───────────────────┐  ┌───────────────────────────┐   │  │
│  │  │  Global Providers │  │   Local ViewModels        │   │  │
│  │  │  - ShoppingCar    │  │   (per screen)            │   │  │
│  │  │  - ReserveCalendar│  │                           │   │  │
│  │  │  - Main           │  │                           │   │  │
│  │  │  - Loading        │  │                           │   │  │
│  │  │  - Version        │  │                           │   │  │
│  │  └─────────┬─────────┘  └─────────────┬─────────────┘   │  │
│  └────────────┴─────────────────────────┬┴─────────────────┘  │
│                                         │                       │
│  ┌──────────────────────────────────────▼───────────────────┐  │
│  │                      Data Layer                           │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐  │  │
│  │  │  API Layer  │  │ Local DB    │  │  Cache Layer    │  │  │
│  │  │  (Chopper)  │  │ (SQLite)    │  │  (Hive)         │  │  │
│  │  └──────┬──────┘  └──────┬──────┘  └───────┬─────────┘  │  │
│  └─────────┴────────────────┴─────────────────┴────────────┘  │
└────────────┬────────────────┬─────────────────────────────────┘
             │                │
             ▼                ▼
┌────────────────────┐  ┌─────────────────┐
│   Backend Server   │  │  Local Storage  │
│   (RESTful API)    │  │  (Device)       │
│   - Auth           │  │  - SQLite DB    │
│   - Products       │  │  - Hive Boxes   │
│   - Orders         │  │                 │
│   - Members        │  │                 │
│   - Reservations   │  │                 │
└────────────────────┘  └─────────────────┘
```

**外部服務整合**

```
┌─────────────────────────────────────────────────────────────┐
│                     External Services                        │
├─────────────────┬─────────────────┬─────────────────────────┤
│ Firebase        │ Backend API     │ Hardware                │
│ - Analytics     │ - Auth Service  │ - Barcode Scanner       │
│                 │ - SignalR       │ - Camera                │
│                 │ - REST API      │                         │
└─────────────────┴─────────────────┴─────────────────────────┘
```

### 2.2 軟體架構模式 (Software Architecture Pattern)

**架構模式：MVVM (Model-View-ViewModel)**

本專案採用 MVVM 架構，資料流向如下：

```
┌─────────────────────────────────────────────────────────────┐
│                      Data Flow                               │
│                                                              │
│  View (Screen)                                               │
│      │                                                       │
│      │ Provider.of / Consumer / Selector                     │
│      ▼                                                       │
│  ViewModel (ChangeNotifier)                                  │
│      │                                                       │
│      │ 呼叫 API / 存取本地資料庫                              │
│      ▼                                                       │
│  Model + API Layer                                           │
│      │                                                       │
│      │ 回傳資料                                               │
│      ▼                                                       │
│  ViewModel (notifyListeners)                                 │
│      │                                                       │
│      │ 監聽更新                                               │
│      ▼                                                       │
│  View (重建 UI)                                              │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**目錄結構說明**

```
lib/
├── api/                    # API 層
│   ├── api_service.dart    # Chopper HTTP 客戶端定義
│   ├── api_service.chopper.dart  # 自動生成的代碼
│   ├── my_authenticator.dart     # 認證器
│   ├── auth_interceptor.dart     # 請求攔截器
│   └── error_tracker/      # API 錯誤追蹤
│
├── extension/              # Dart 擴展方法
│   ├── datetime_extension.dart
│   ├── string_extension.dart
│   ├── list_extension.dart
│   └── ...
│
├── flavor/                 # 環境配置 (Flavor)
│   └── flavor.dart         # 6 種環境配置
│
├── gen/                    # 自動生成資源
│   └── r.dart              # Flutter Gen 生成
│
├── hive/                   # Hive 本地儲存
│   ├── entity/             # Hive 實體類
│   ├── helper/             # Hive 輔助類
│   └── hive_provider/      # Hive 資料提供器
│
├── logger/                 # 日誌系統
│   └── my_print.dart
│
├── model/                  # 資料模型
│   ├── api_model/          # API 相關模型
│   │   ├── req_model/      # 請求模型
│   │   └── res_model/      # 回應模型
│   ├── product/            # 商品模型
│   ├── member/             # 會員模型
│   ├── class/              # 課程模型
│   ├── performance/        # 業績模型
│   └── reserve_calendar_model/  # 預約日曆模型
│
├── provider/               # 全局狀態管理
│   ├── shopping_car_provider.dart     # 購物車 (核心)
│   ├── reserve_calendar_provider.dart # 預約日曆
│   ├── main_provider.dart             # 主應用狀態
│   ├── loading_provider.dart          # 載入狀態
│   └── version_provider.dart          # 版本管理
│
├── route_observer/         # 路由觀察
│   ├── my_route_observer.dart
│   └── page_info.dart      # 頁面資訊單例
│
├── screen/                 # 畫面 (View + ViewModel)
│   ├── start/              # 應用入口
│   ├── login/              # 登入
│   ├── main/               # 主畫面
│   ├── scan/               # 掃描
│   ├── search_product/     # 搜尋商品
│   ├── shopping_car/       # 購物車
│   ├── payment/            # 支付
│   ├── member/             # 會員管理
│   ├── brand_member/       # 品牌會員
│   ├── search_member/      # 搜尋會員
│   ├── reserve_calendar/   # 預約日曆
│   ├── reserve_class/      # 預約課程
│   ├── reserve_manage/     # 預約管理
│   ├── class/              # 課程
│   ├── class_confirm/      # 課程確認
│   ├── history_order/      # 歷史訂單
│   ├── performance_distribution/  # 業績分配
│   ├── product/            # 商品
│   ├── buy_cash/           # 儲值金購買
│   └── product_inventory_management/  # 庫存管理
│
├── sqlite/                 # SQLite 本地資料庫
│   ├── DatabaseHelper.dart
│   ├── sales_record.dart
│   ├── product_shopping_car_record.dart
│   └── provider/
│
├── static/                 # 靜態工具
│   └── net_work_listener.dart
│
├── util/                   # 工具函數
│   ├── MyRoutes.dart       # 路由定義
│   ├── error_decode.dart   # 錯誤解析
│   ├── StringUtils.dart    # 字串工具
│   └── validation_mixin.dart
│
└── widget/                 # 共用元件 (35+ 類別)
    ├── app_bar/
    ├── btn/
    ├── dialog/
    ├── scanner/
    ├── reserve_calender_widget/
    └── ...
```

**模組命名規範**

```
功能名_screen.dart           → View
功能名_screen_view_model.dart → ViewModel

範例：
screen/payment/
├── payment_screen.dart              # View
├── payment_screen_view_model.dart   # ViewModel
├── payment_details/                 # 子功能 View
├── payment_list/                    # 子功能 View
└── payment_tape_switch_area/        # 子功能 View
```

### 2.3 狀態管理策略 (State Management Strategy)

**使用套件**：`provider` (^6.0.5)

**狀態分類與處理規則**

| 狀態類型 | 位置 | 說明 | 範例 |
|----------|------|------|------|
| 全局狀態 | `lib/provider/` | 跨頁面共享的資料 | 購物車、會員資訊 |
| 區域狀態 | `lib/screen/*/view_model.dart` | 單一頁面的資料 | 表單輸入、列表篩選 |

**全局 Provider 列表**

| Provider | 檔案 | 職責 |
|----------|------|------|
| ShoppingCarProvider | `shopping_car_provider.dart` | 購物車管理、折扣計算、業績分配、支付處理 |
| ReserveCalendarScreenProvider | `reserve_calendar_provider.dart` | 預約日曆資料、日/週/月視圖切換 |
| MainProvider | `main_provider.dart` | 主畫面狀態、應用連結 |
| LoadingProvider | `loading_provider.dart` | 全局載入遮罩控制 |
| VersionProvider | `version_provider.dart` | 版本檢查與更新 |

**ShoppingCarProvider 核心功能**

```
ShoppingCarProvider
├── 商品管理
│   ├── addProductDirectlyToCart()    # 直接添加商品
│   ├── apiGetProductByBarcode()      # 條碼查詢商品
│   ├── removeProduct()               # 移除商品
│   └── updateQuantity()              # 更新數量
│
├── 折扣系統
│   ├── toggleCampaignSelect()        # 折扣活動選擇
│   └── calculateDiscount()           # 折扣計算
│
├── 業績分配
│   └── distributePerformance()       # 員工業績分配
│
├── 支付處理
│   ├── processPayment()              # 支付處理
│   └── handlePrepaid()               # 儲值金處理
│
└── 本地儲存
    └── SQLite 購物車持久化
```

### 2.4 路由與導航 (Routing & Navigation)

**導航方式**：Navigator 1.0 + 自訂路由管理

**路由定義** (`lib/util/MyRoutes.dart`)

```dart
enum PageName {
  login,           // 登入頁
  main,            // 主畫面
  payment,         // 支付
  memberInfo,      // 會員資訊
  historyOrder,    // 歷史訂單
  reserveCalendar, // 預約日曆
  reserveClass,    // 預約課程
  reserveManage,   // 預約管理
  classConfirm,    // 課程確認
  performanceDistribution,  // 業績分配
  productInventory,         // 庫存管理
  // ... 共 18 個主要頁面
}
```

**導航機制**

| 元件 | 檔案 | 功能 |
|------|------|------|
| Global Navigator Key | `my_app.dart` | 全局導航控制 |
| MyRouteObserver | `my_route_observer.dart` | 路由事件監聽 |
| PageInfo | `page_info.dart` | 當前頁面追蹤 (單例) |

**導航方法**

```dart
// 推入新頁面
pushTo(context, PageName.payment);

// 推入並移除所有舊頁面
pushAndRemoveUntil(context, PageName.main);
```

**注意事項**

- Dialog 不會更新 `PageInfo().pageName`
- 從 Dialog 導航時需手動處理頁面追蹤

---

## 3. 功能需求與邏輯 (Functional Requirements)

### 3.1 使用者案例圖 (Use Case Diagram)

```
                    ┌─────────────────────────────────────────┐
                    │              sbar_pos 系統              │
                    └─────────────────────────────────────────┘
                                       │
        ┌──────────────────────────────┼──────────────────────────────┐
        │                              │                              │
        ▼                              ▼                              ▼
   ┌─────────┐                   ┌─────────┐                   ┌─────────┐
   │  店員   │                   │  店長   │                   │ 美容師  │
   └────┬────┘                   └────┬────┘                   └────┬────┘
        │                              │                              │
        │  ┌───────────────────────────┴───────────────────────────┐ │
        │  │                                                        │ │
        ├──┼── 登入系統 ──────────────────────────────────────────┼─┤
        │  │                                                        │ │
        ├──┼── 搜尋/掃描商品 ─────────────────────────────────────┼─┤
        │  │                                                        │ │
        ├──┼── 管理購物車 ────────────────────────────────────────┼─┤
        │  │                                                        │ │
        ├──┼── 結帳支付 ──────────────────────────────────────────┼─┤
        │  │                                                        │ │
        ├──┼── 查詢會員 ──────────────────────────────────────────┼─┤
        │  │                                                        │ │
        │  ├── 查看業績分配 ────────────────────────────────────────┤ │
        │  │                                                        │ │
        │  ├── 管理歷史訂單 ────────────────────────────────────────┤ │
        │  │                                                        │ │
        │  ├── 庫存管理 ────────────────────────────────────────────┤ │
        │  │                                                        │ │
        │  │                                               ┌────────┤ │
        │  │                                               │        │ │
        │  └───────────────────────────────────────────────┼────────┘ │
        │                                                  │          │
        │                                                  ├── 查看預約日曆
        │                                                  │
        │                                                  ├── 預約課程
        │                                                  │
        │                                                  ├── 課程確認
        │                                                  │
        │                                                  └── 預約管理
        │
        ├── 查詢課程
        │
        └── 購買儲值金
```

### 3.2 功能詳細規格 (Detailed Functional Specifications)

#### 3.2.1 登入模組 (Login)

**前置條件**
- 使用者已取得系統帳號密碼
- 裝置已連接網路

**主要流程**
1. 使用者開啟 App
2. 系統顯示登入畫面
3. 使用者輸入帳號與密碼
4. 使用者點擊登入按鈕
5. 系統驗證帳號密碼
6. 驗證成功，導向主畫面
7. 系統儲存使用者 Token 至 Hive

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 帳號密碼錯誤 | 顯示錯誤訊息，停留登入頁 |
| 網路斷線 | 顯示網路錯誤提示 |
| Token 過期 | 自動刷新 Token 或重新登入 |

**後置條件**
- 使用者狀態更新為已登入
- 本地儲存使用者資訊與 Token

---

#### 3.2.2 商品掃描/搜尋模組 (Scan / Search Product)

**前置條件**
- 使用者已登入系統
- 裝置具備相機權限 (掃描功能)

**主要流程 - 條碼掃描**
1. 使用者點擊掃描按鈕
2. 系統開啟相機掃描介面
3. 使用者對準商品條碼
4. 系統辨識條碼
5. 系統呼叫 API 查詢商品
6. 查詢成功，商品加入購物車
7. 返回主畫面

**主要流程 - 商品搜尋**
1. 使用者進入搜尋商品頁面
2. 使用者輸入關鍵字或選擇分類
3. 系統顯示符合條件的商品列表
4. 使用者選擇商品
5. 使用者設定數量
6. 商品加入購物車

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 無法辨識條碼 | 提示使用者重新掃描或手動輸入 |
| 商品不存在 | 顯示查無商品訊息 |
| 商品已下架 | 顯示商品已下架訊息 |
| API 呼叫失敗 | 顯示網路錯誤，支援重試 |

**後置條件**
- 商品已加入購物車
- 購物車數量更新

---

#### 3.2.3 購物車模組 (Shopping Cart)

**前置條件**
- 使用者已登入系統
- 購物車至少有一項商品

**主要流程**
1. 使用者查看購物車內容
2. 系統顯示所有商品項目
3. 使用者可執行以下操作：
   - 調整商品數量
   - 移除商品
   - 選擇折扣活動
   - 設定業績分配
4. 系統即時計算總金額
5. 使用者點擊結帳
6. 導向支付頁面

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 商品庫存不足 | 提示庫存數量，限制最大購買量 |
| 折扣活動衝突 | 互斥選擇，只能選一個折扣 |
| 購物車為空 | 禁用結帳按鈕 |

**後置條件**
- 購物車狀態更新
- 本地資料庫同步 (SQLite)

---

#### 3.2.4 支付模組 (Payment)

**前置條件**
- 購物車有商品
- 已設定業績分配 (若需要)

**主要流程**
1. 使用者進入支付頁面
2. 系統顯示訂單明細
3. 使用者選擇支付方式：
   - 現金
   - 信用卡
   - 儲值金
   - 其他
4. 使用者確認金額
5. 使用者點擊結帳
6. 系統建立訂單
7. 系統處理支付
8. 支付成功，顯示收據
9. 清空購物車

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 儲值金不足 | 提示餘額不足，建議其他付款方式 |
| 支付失敗 | 顯示錯誤訊息，保留訂單資料 |
| 網路中斷 | 訂單儲存至本地，待網路恢復後同步 |

**後置條件**
- 訂單建立完成
- 購物車清空
- 會員儲值金/點數更新 (若使用)

---

#### 3.2.5 會員管理模組 (Member)

**前置條件**
- 使用者已登入系統

**功能子模組**

| 子模組 | 功能描述 |
|--------|----------|
| 會員搜尋 | 透過姓名、電話、會員編號搜尋 |
| 會員資訊 | 查看/編輯會員基本資料 |
| 歷史訂單 | 查看會員消費紀錄 |
| 儲值金管理 | 查看餘額、儲值紀錄、退款 |
| 會員課程 | 查看已購買課程 |
| 會員預約 | 查看預約紀錄 |

**主要流程 - 會員搜尋**
1. 使用者進入會員搜尋頁面
2. 使用者輸入搜尋條件
3. 系統查詢符合條件的會員
4. 顯示會員列表
5. 使用者選擇會員
6. 導向會員詳細資訊頁

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 查無會員 | 顯示「查無資料」訊息 |
| 搜尋條件不足 | 提示輸入至少一個條件 |

**後置條件**
- 選定會員可用於後續交易

---

#### 3.2.6 預約日曆模組 (Reserve Calendar)

**前置條件**
- 使用者已登入系統
- 具備預約管理權限

**視圖模式**

| 模式 | 說明 |
|------|------|
| 日視圖 | 顯示單日所有預約時段 |
| 週視圖 | 顯示一週預約概覽 |
| 月視圖 | 顯示整月預約狀態 |

**主要流程**
1. 使用者進入預約日曆頁面
2. 系統載入當前日期的預約資料
3. 使用者可切換視圖模式
4. 使用者可左右滑動切換日期
5. 使用者點擊預約事件
6. 顯示預約詳細資訊
7. 可執行：修改、取消預約

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 載入逾時 | 顯示重試按鈕 |
| 無預約資料 | 顯示「今日無預約」 |

**後置條件**
- 預約資料快取更新

---

#### 3.2.7 課程預約模組 (Reserve Class)

**前置條件**
- 使用者已登入系統
- 已選擇會員 (會員課程預約)

**主要流程**
1. 使用者進入課程預約頁面
2. 使用者選擇課程類型
3. 系統顯示可預約課程列表
4. 使用者選擇課程
5. 使用者選擇日期
6. 系統顯示可用時段與服務人員
7. 使用者選擇時段與服務人員
8. 使用者確認預約
9. 系統建立預約記錄

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 時段已被預約 | 顯示「時段已滿」，建議其他時段 |
| 服務人員無空檔 | 顯示「該人員已有安排」 |
| 課程已過期 | 顯示「課程已過期」 |

**後置條件**
- 預約記錄建立
- 日曆資料更新
- 會員課程扣除一次

---

#### 3.2.8 歷史訂單模組 (History Order)

**前置條件**
- 使用者已登入系統

**功能子模組**

| 子模組 | 功能描述 |
|--------|----------|
| 訂單列表 | 依日期、會員、狀態篩選訂單 |
| 訂單詳情 | 查看完整訂單資訊 |
| 付款紀錄 | 查看訂單付款明細 |
| 銷售退貨 | 處理商品退貨 |
| 訂單取消 | 取消訂單 |

**主要流程 - 查詢訂單**
1. 使用者進入歷史訂單頁面
2. 使用者設定篩選條件
3. 系統查詢符合條件的訂單
4. 顯示訂單列表
5. 使用者選擇訂單
6. 顯示訂單詳細資訊

**例外流程**
| 情境 | 處理方式 |
|------|----------|
| 查無訂單 | 顯示「查無資料」 |
| 無法退貨 | 顯示「該訂單不可退貨」並說明原因 |

**後置條件**
- 訂單資料載入完成

---

#### 3.2.9 業績分配模組 (Performance Distribution)

**前置條件**
- 使用者已登入系統
- 具備業績查看權限

**主要流程**
1. 使用者進入業績分配頁面
2. 使用者選擇日期範圍
3. 系統查詢業績資料
4. 顯示員工業績列表
5. 使用者可查看詳細分配

**業務規則**
- 每筆訂單可分配給多位員工
- 業績比例總和必須為 100%
- 預設業績 100% 分配給單一員工

**後置條件**
- 業績資料載入完成

---

### 3.3 業務邏輯規則 (Business Rules)

#### 折扣計算規則

```
1. 折扣活動為互斥選擇，一次只能使用一個折扣
2. 折扣計算優先順序：
   - 會員等級折扣
   - 活動折扣
   - 優惠券折扣
3. 折扣不可疊加 (除非系統設定允許)
```

#### 業績分配規則

```
1. 每筆訂單須指定業績歸屬員工
2. 可多人分配，比例合計 100%
3. 預設為 100% 分配給操作員工
4. 課程預約業績歸服務人員
```

#### 儲值金使用規則

```
1. 儲值金可部分使用
2. 儲值金可與其他付款方式併用
3. 退款時儲值金退回原帳戶
4. 儲值金有效期限依系統設定
```

#### 課程預約規則

```
1. 預約需提前 24 小時
2. 取消需提前 24 小時
3. 會員課程有效期限
4. 同一時段不可重複預約
```

---

## 4. 使用者介面與體驗設計 (UI/UX Design Specifications)

### 4.1 畫面流程圖 (Screen Flow)

```
┌─────────┐
│  啟動   │
└────┬────┘
     │
     ▼
┌─────────┐     登入失敗      ┌─────────┐
│  登入   │ ◄─────────────── │ 錯誤提示 │
└────┬────┘                   └─────────┘
     │ 登入成功
     ▼
┌─────────────────────────────────────────────────────────────┐
│                        主畫面 (6 個標籤頁)                   │
├─────────┬─────────┬─────────┬─────────┬─────────┬─────────┤
│ 預約日曆 │  課程   │  商品   │ 品牌會員 │ 歷史訂單 │ 儲值購買 │
└────┬────┴────┬────┴────┬────┴────┬────┴────┬────┴────┬────┘
     │         │         │         │         │         │
     ▼         ▼         ▼         ▼         ▼         ▼
┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐
│日曆視圖 │ │課程列表 │ │商品列表 │ │會員搜尋 │ │訂單列表 │ │儲值金   │
│日/週/月 │ │         │ │         │ │         │ │         │ │購買     │
└────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘
     │         │         │         │         │         │
     ▼         ▼         ▼         ▼         ▼         ▼
┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐
│預約詳情 │ │課程預約 │ │商品詳情 │ │會員詳情 │ │訂單詳情 │ │購物車   │
└────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘
     │         │         │         │         │         │
     └─────────┴─────────┴─────────┴─────────┴─────────┘
                              │
                              ▼
                       ┌─────────────┐
                       │   購物車    │
                       └──────┬──────┘
                              │
                              ▼
                       ┌─────────────┐
                       │    支付     │
                       └──────┬──────┘
                              │
                              ▼
                       ┌─────────────┐
                       │  完成結帳   │
                       └─────────────┘
```

**側邊欄 (Drawer) 功能**

```
┌─────────────────────────┐
│        側邊欄           │
├─────────────────────────┤
│ • POS 收款             │
│ • 預約管理             │
│ • 業績分配             │
│ • 庫存管理             │
│ • 開錢箱               │
│ • 登出                 │
└─────────────────────────┘
```

### 4.2 UI 規範 (UI Guidelines)

#### 螢幕配置

| 項目 | 規格 |
|------|------|
| 設計解析度 | 1920 x 1200 |
| 螢幕方向 | 僅橫向 (Landscape) |
| 適配工具 | flutter_screenutil |

#### 色彩系統 (Color Scheme)

```dart
// 主要色系
class MyColor {
  static const Color primary = Color(0xFF...);     // 主色
  static const Color secondary = Color(0xFF...);   // 次色
  static const Color accent = Color(0xFF...);      // 強調色

  // 語義色彩
  static const Color success = Color(0xFF...);     // 成功
  static const Color error = Color(0xFF...);       // 錯誤
  static const Color warning = Color(0xFF...);     // 警告
  static const Color info = Color(0xFF...);        // 資訊

  // 背景色
  static const Color background = Color(0xFF...);  // 背景
  static const Color surface = Color(0xFF...);     // 表面
}
```

#### 字型系統 (Typography)

| 等級 | 用途 | 大小 | 粗細 |
|------|------|------|------|
| H1 | 頁面標題 | 24sp | Bold |
| H2 | 區塊標題 | 20sp | SemiBold |
| H3 | 列表標題 | 18sp | Medium |
| Body1 | 內文 | 16sp | Regular |
| Body2 | 次要內文 | 14sp | Regular |
| Caption | 說明文字 | 12sp | Regular |

#### 間距系統 (Spacing)

| 尺寸 | 數值 | 用途 |
|------|------|------|
| xs | 4dp | 最小間距 |
| sm | 8dp | 小間距 |
| md | 16dp | 中間距 |
| lg | 24dp | 大間距 |
| xl | 32dp | 超大間距 |

### 4.3 共用元件庫 (Common Widgets)

**按鈕元件 (lib/widget/btn/)**

| 元件名稱 | 用途 | 狀態 |
|----------|------|------|
| PrimaryButton | 主要操作按鈕 | 正常、禁用、載入中 |
| SecondaryButton | 次要操作按鈕 | 正常、禁用 |
| TextButton | 文字按鈕 | 正常、禁用 |
| IconButton | 圖示按鈕 | 正常、選中 |

**對話框元件 (lib/widget/dialog/)**

| 元件名稱 | 用途 |
|----------|------|
| ConfirmDialog | 確認對話框 |
| AlertDialog | 警告對話框 |
| InputDialog | 輸入對話框 |
| LoadingDialog | 載入中對話框 |
| DatePickerDialog | 日期選擇對話框 |

**列表元件 (lib/widget/base_title_list_bar/)**

| 元件名稱 | 用途 |
|----------|------|
| BaseTitleListBar | 基礎標題列表 |
| ProductListItem | 商品列表項 |
| MemberListItem | 會員列表項 |
| OrderListItem | 訂單列表項 |

**日曆元件 (lib/widget/reserve_calender_widget/)**

| 元件名稱 | 用途 |
|----------|------|
| DayViewCalendar | 日視圖日曆 |
| WeekViewCalendar | 週視圖日曆 |
| MonthViewCalendar | 月視圖日曆 |
| EventCard | 事件卡片 |
| TimeSlotPicker | 時段選擇器 |

### 4.4 互動與動畫 (Interactions & Animations)

#### 轉場效果

| 場景 | 動畫類型 |
|------|----------|
| 頁面推入 | SlideTransition (右進) |
| 頁面彈出 | SlideTransition (右出) |
| Modal 對話框 | FadeTransition + ScaleTransition |
| 底部工作表 | SlideTransition (下進上出) |

#### Loading 狀態

| 場景 | 呈現方式 |
|------|----------|
| 全域載入 | 半透明遮罩 + 載入指示器 |
| 按鈕載入 | 按鈕內載入指示器 |
| 列表載入 | Skeleton 骨架屏 |
| 下拉刷新 | PullToRefresh 指示器 |

#### 錯誤訊息呈現

| 類型 | 呈現方式 | 持續時間 |
|------|----------|----------|
| 輕微錯誤 | Toast | 2 秒 |
| 一般錯誤 | SnackBar | 4 秒 |
| 嚴重錯誤 | AlertDialog | 手動關閉 |
| 表單錯誤 | Inline Error | 持續顯示 |

---

## 5. 資料處理與 API 整合 (Data & API Integration)

### 5.1 資料模型 (Data Models)

#### 核心商品模型

```dart
// lib/model/product/product_model.dart
class ProductModel {
  final String id;
  final String name;
  final int type;           // 1: 商品, 2: 預約課程, 3: 儲值金
  final double price;
  final int quantity;
  final String? imageUrl;

  // 預約相關 (type == 2)
  final DateTime? reserveDate;
  final String? reserveTime;
  final String? beauticianId;
  final String? beauticianName;
}
```

#### 會員模型

```dart
// lib/model/member/member_data.dart
class MemberData {
  final String id;
  final String name;
  final String phone;
  final String? email;
  final String? memberNo;
  final double prepaidBalance;   // 儲值金餘額
  final int levelId;             // 會員等級
}
```

#### 訂單模型

```dart
// lib/model/api_model/res_model/res_get_order_detail.dart
class OrderDetail {
  final String orderId;
  final String orderNo;
  final DateTime orderDate;
  final String status;
  final double totalAmount;
  final double discountAmount;
  final double paidAmount;
  final List<OrderItem> items;
  final List<PaymentRecord> payments;
}
```

#### 預約事件模型

```dart
// lib/model/reserve_calendar_model/models/event.dart
class ReserveEvent {
  final String id;
  final String title;
  final DateTime startTime;
  final DateTime endTime;
  final String? memberId;
  final String? memberName;
  final String? employeeId;
  final String? employeeName;
  final String status;
}
```

#### JSON 序列化

專案使用手動 JSON 序列化 (factory fromJson, Map toJson)：

```dart
factory ProductModel.fromJson(Map<String, dynamic> json) {
  return ProductModel(
    id: json['id'],
    name: json['name'],
    // ...
  );
}

Map<String, dynamic> toJson() {
  return {
    'id': id,
    'name': name,
    // ...
  };
}
```

### 5.2 本地儲存 (Local Storage)

#### Hive (輕量 KV 儲存)

**用途**: 使用者資訊、Token、設定

```dart
// lib/hive/entity/user.dart
@HiveType(typeId: 0)
class User extends HiveObject {
  @HiveField(0)
  String? id;

  @HiveField(1)
  String? name;

  @HiveField(2)
  String? token;

  @HiveField(3)
  String? refreshToken;
}
```

**Box 定義**:
- `userBox` - 使用者資料

#### SQLite (結構化資料)

**資料庫**: `sbar_database.db`

**資料表**

| 資料表 | 用途 |
|--------|------|
| salesRecord | 銷售記錄 (離線備份) |
| productShoppingCarRecord | 購物車記錄 (持久化) |

```dart
// lib/sqlite/DatabaseHelper.dart
class DatabaseHelper {
  static const String _databaseName = 'sbar_database.db';

  Future<Database> initDatabase() async {
    return openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute('''
          CREATE TABLE salesRecord (
            id INTEGER PRIMARY KEY,
            orderId TEXT,
            // ...
          )
        ''');

        await db.execute('''
          CREATE TABLE productShoppingCarRecord (
            id INTEGER PRIMARY KEY,
            productId TEXT,
            quantity INTEGER,
            // ...
          )
        ''');
      },
    );
  }
}
```

### 5.3 API 介面規格 (API Specifications)

#### API 服務定義

```dart
// lib/api/api_service.dart
@ChopperApi()
abstract class ApiService extends ChopperService {
  // 登入
  @Post(path: '/login')
  Future<Response> login(@Body() Map<String, dynamic> body);

  // 取得商品類型
  @Get(path: '/products-types')
  Future<Response> getProductTypes();

  // 取得課程類型
  @Get(path: '/programs-course-types')
  Future<Response> getProgramsCourseTypes();

  // 取得我的資料
  @Get(path: '/my-profile')
  Future<Response> getMyProfile();

  // 取得員工列表
  @Get(path: '/employees')
  Future<Response> getEmployees();

  // 會員搜尋
  @Get(path: '/members/search')
  Future<Response> searchMembers(@Query('keyword') String keyword);

  // 訂單報價
  @Post(path: '/orders/quote')
  Future<Response> orderQuote(@Body() Map<String, dynamic> body);

  // ... 更多 API
}
```

#### 認證機制

```dart
// lib/api/my_authenticator.dart
class MyAuthenticator extends Authenticator {
  @override
  FutureOr<Request?> authenticate(
    Request request,
    Response response, [
    Request? originalRequest,
  ]) async {
    if (response.statusCode == 401) {
      // Token 過期，嘗試刷新
      final newToken = await refreshToken();
      if (newToken != null) {
        return request.copyWith(
          headers: {'Authorization': 'Bearer $newToken'},
        );
      }
    }
    return null;
  }
}
```

#### 錯誤處理策略

| 狀態碼 | 處理方式 |
|--------|----------|
| 200 | 成功，解析回應資料 |
| 400 | 請求錯誤，顯示錯誤訊息 |
| 401 | Token 過期，自動刷新或重新登入 |
| 403 | 權限不足，顯示錯誤訊息 |
| 404 | 資源不存在，顯示錯誤訊息 |
| 500 | 伺服器錯誤，顯示通用錯誤訊息 |
| Network Error | 網路錯誤，提示檢查網路 |

```dart
// lib/util/error_decode.dart
String decodeApiError(Response response) {
  switch (response.statusCode) {
    case 400:
      return parseErrorMessage(response.body);
    case 401:
      return '登入已過期，請重新登入';
    case 403:
      return '權限不足';
    case 404:
      return '資料不存在';
    case 500:
      return '伺服器錯誤，請稍後再試';
    default:
      return '發生未知錯誤';
  }
}
```

#### API 回應模型對照表

| API 端點 | 回應模型 |
|----------|----------|
| /products-types | ResGetProductsTypes |
| /programs-course-types | ResGetProgramsCourseTypes |
| /my-profile | ResMyProfile |
| /employees | ResGetEmployees |
| /members/search | ResMemberProfile |
| /orders/quote | ResOrderQuote |
| /orders | ResGetOrders |
| /orders/{id} | ResGetOrderDetail |
| /reservations/day | ResGetReservationDay |
| /reservations/week | ResGetReservationWeek |
| /reservations/month | ResGetReservationMonth |
| /checkout | ResCheckout |
| /pay-methods | ResGetPayMethods |
| /prepaid | ResGetPrepaid |

---

## 6. 非功能性需求 (Non-Functional Requirements)

### 6.1 效能需求 (Performance)

| 指標 | 目標 | 說明 |
|------|------|------|
| App 啟動時間 | < 3 秒 | 冷啟動至首頁可操作 |
| 頁面切換 | < 500ms | 頁面轉場動畫完成 |
| 列表滑動 | 60 FPS | 不掉幀、無卡頓 |
| API 回應 | < 2 秒 | 一般操作的 API 回應 |
| 條碼掃描 | < 1 秒 | 掃描至結果顯示 |

### 6.2 安全性 (Security)

| 項目 | 措施 |
|------|------|
| 代碼混淆 | Release 版本啟用 ProGuard/R8 (Android) |
| 通訊加密 | 強制 HTTPS，所有 API 請求加密傳輸 |
| Token 儲存 | Hive 加密儲存 |
| 敏感資料 | 不在日誌中印出敏感資訊 |
| Session 管理 | Token 過期自動刷新機制 |

### 6.3 相容性 (Compatibility)

| 平台 | 最低版本 | 說明 |
|------|----------|------|
| iOS | 12.0 | 支援 iPhone 6s 及以上 |
| Android | API 21 (5.0) | 支援 Android 5.0 及以上 |

#### 螢幕適配策略

```dart
// 使用 flutter_screenutil 進行適配
// 設計稿基準: 1920 x 1200

ScreenUtil.init(
  context,
  designSize: const Size(1920, 1200),
);

// 使用方式
Container(
  width: 100.w,   // 寬度
  height: 50.h,   // 高度
  padding: EdgeInsets.all(16.r),  // 間距
)

Text(
  'Hello',
  style: TextStyle(fontSize: 16.sp),  // 字體大小
)
```

### 6.4 國際化與在地化 (i18n & l10n)

**目前支援語言**: 繁體中文

**實作框架**: Flutter intl

```yaml
# pubspec.yaml
dependencies:
  intl: ^0.20.2
  flutter_localizations:
    sdk: flutter
```

**語言檔案結構**

```
lib/l10n/
├── intl_zh_TW.arb    # 繁體中文
└── intl_en.arb       # 英文 (預留)
```

**使用方式**

```dart
// 取得本地化文字
S.of(context).loginButton
S.of(context).orderTotal
```

---

## 7. 測試計畫 (Test Plan)

### 7.1 單元測試 (Unit Test)

**測試範圍**

| 類型 | 測試對象 | 優先級 |
|------|----------|--------|
| 業務邏輯 | ShoppingCarProvider | 高 |
| 業務邏輯 | ReserveCalendarProvider | 高 |
| 資料轉換 | Model fromJson/toJson | 中 |
| 工具函數 | Extension methods | 中 |
| 驗證規則 | ValidationMixin | 中 |

**執行命令**

```bash
# 執行所有單元測試
flutter test

# 執行特定測試檔案
flutter test test/unit/shopping_car_provider_test.dart
```

### 7.2 Widget 測試 (Widget Test)

**測試範圍**

| 類型 | 測試對象 | 優先級 |
|------|----------|--------|
| 共用元件 | PrimaryButton | 中 |
| 共用元件 | Dialog 系列 | 中 |
| 列表元件 | ProductListItem | 中 |
| 表單元件 | TextField 系列 | 中 |

**測試重點**

- 元件正確渲染
- 點擊事件觸發
- 狀態變化顯示
- 輸入驗證回饋

### 7.3 整合測試 (Integration Test)

**測試框架**: Patrol (^3.0.0)

**測試範圍**

| 流程 | 測試案例 | 優先級 |
|------|----------|--------|
| 登入流程 | 正常登入、錯誤登入 | 高 |
| 購物流程 | 掃描 → 購物車 → 結帳 | 高 |
| 會員流程 | 搜尋 → 查看資料 | 中 |
| 預約流程 | 選課 → 選時段 → 確認 | 中 |

**執行命令**

```bash
# 執行整合測試
flutter test integration_test/
```

### 7.4 測試覆蓋率目標

| 測試類型 | 目標覆蓋率 |
|----------|------------|
| 單元測試 | >= 70% |
| Widget 測試 | >= 50% |
| 整合測試 | 主要流程 100% |

---

## 附錄

### A. 環境配置 (Flavor Configuration)

| 環境 | 識別碼 | 用途 |
|------|--------|------|
| kidTest | Kid 測試環境 | 開發測試 |
| kidStag | Kid 預發佈環境 | UAT 測試 |
| kidProd | Kid 正式環境 | 正式上線 |
| cusTest | Customer 測試環境 | 開發測試 |
| cusStag | Customer 預發佈環境 | UAT 測試 |
| cusProd | Customer 正式環境 | 正式上線 |

### B. 建置命令 (Build Commands)

```bash
# 測試環境 APK
flutter build apk --flavor kidTest -t lib/screen/start/main_kid_test.dart

# 測試環境 App Bundle
flutter build appbundle --flavor kidTest -t lib/screen/start/main_kid_test.dart

# 測試環境 IPA
flutter build ipa --flavor kidTest -t lib/screen/start/main_kid_test.dart

# 正式環境 App Bundle
flutter build appbundle --flavor cusProd -t lib/screen/start/main_cus_prod.dart
```

### C. 程式碼生成 (Code Generation)

```bash
# 資源生成 (圖片、字型)
dart run build_runner build

# API 代碼生成 (清除衝突)
dart run build_runner build --delete-conflicting-outputs

# 多語系生成
flutter pub run intl_utils:generate
```

---

**文件修改時間**: 2025-12-11

**文件版本**: 1.0.0
