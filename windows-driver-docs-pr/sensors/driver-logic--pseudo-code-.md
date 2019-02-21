---
title: センサー ドライバー ロジック
description: このセクションでは、擬似コードとして重要な推進ロジック、またはタスクについて説明します。
ms.assetid: 4B14C515-1B79-4B67-BA9A-365B2D6C0F07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c36e299afa4e7d9480b7eee9c16e795ad3543e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530669"
---
# <a name="sensor-driver-logic"></a>センサー ドライバー ロジック


このセクションでは、擬似コードとして重要な推進ロジック、またはタスクについて説明します。 これらのタスクには、次のクライアント操作に対するドライバーのサポートが含まれます。

-   クライアントが接続します。
-   クライアントがイベントをサブスクライブします。
-   クライアント イベントからをアンサブスク ライブします。
-   クライアントが切断します。

クライアントが接続するデスクトップ アプリケーションを呼び出すとき、 **ISensorCollection::GetAt**メソッド。 このメソッドが戻る、 **ISensor**目的のセンサーのインターフェイス。 アプリケーションでは、このインターフェイスをリリースするときに、クライアントを切断します。

クライアントは、デスクトップ アプリケーションを呼び出すときのイベントにサブスクライブして、 **ISensorManager:SetEventSink**メソッド。 アプリケーションでは、このメソッドによって返されるイベント シンクをリリースするとき、クライアントがイベントをアンサブスク ライブします。

## <a name="abbreviations-and-variables"></a>省略形と変数


このセクションでは擬似コードでは、次の省略形を使用します。

| 省略形 | 説明                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------|
| CRI          | 現在のレポート間隔 (ミリ秒単位で指定)                                                       |
| CS           | (値は、センサーの種類に依存) と小文字の区別を変更します。                                                  |
| CS\[\]       | すべてのデータ フィールドの変更の感度の配列 (たとえば、3 軸加速度計、3 つのエントリ) |
| LDA          | 必要な場所の精度 (場所のみに適用されます)                                                      |
| RS           | (イベントを有効または無効になっているかどうかを示す) の状態を報告                                       |
| PS           | 電源の状態 (off、低、または高で指定できます)                                                                    |



擬似コードには、次の変数が含まれています。

| 変数    | 説明                                                                          |
|-------------|--------------------------------------------------------------------------------------|
| sensorID    | 特定のセンサーの一意識別子                                                 |
| クライアント Id    | 特定のクライアントの一意の識別子                                                 |
| flagCRI     | 少なくとも 1 つのクライアントが現在のレポート間隔を指定した場合に True に設定します。         |
| flagCS      | 少なくとも 1 つのクライアントがデバイスの変更の区別を指定した場合に True に設定します。 |
| flagLDA     | 少なくとも 1 つのクライアントが必要な場所の精度を指定した場合に True に設定します。       |
| deviceState | ドライバーがデバイスに接続されていることを示します。                                      |



## <a name="driver-methods"></a>ドライバー メソッド


センサー ドライバーでは、クライアントとデバイスの両方の初期化をサポートする必要があります。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverClientInitialize
-   DeviceSensorInitialize

センサー ドライバーでは、プラットフォームのデバイス ドライバー インターフェイス (DDI) をサポートします。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DDIOnClientConnect
-   DDIOnClientDisconnect
-   DDIOnClientSubscribeToEvents
-   DDIOnClientUnsubscribeFromEvents
-   DDIOnSetCRI
-   DDIOnSetCS
-   DDIOnSetLDA
-   DDIOnGetProperties
-   DDIOnGetDatafields
-   DDIHandleAsyncDataEvent

センサー ドライバーには、現在のレポート間隔の更新を処理する、秘密度を変更および具合内部メソッドがサポートしています。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverUpdateCRI
-   DriverUpdateCS
-   DriverUpdateLDA
-   DriverUpdateSensorState
-   DriverUpdateDatafields

センサー ドライバーでは、センサー デバイスを更新するメソッドをサポートします。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverUpdateDeviceCRI
-   DriverUpdateDeviceCS
-   DriverUpdateDeviceLDA
-   DriverUpdateDeviceRS
-   DriverUpdateDevicePS

センサー ドライバーでは、複数のセンサーを格納しているデバイスとのインターフェイス メソッドをサポートします。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverUpdateDeviceState

センサー ドライバーは HID センサーをサポートする場合は、次のメソッドをサポートして可能性があります。

-   HIDSensorPollData
-   HIDSensorDeviceEvent
-   HIDSensorSetProperties
-   HIDSensorGetProperties

センサー ドライバーは HID センサーをサポートする場合は、複数のセンサーを含むデバイスの次のメソッドをサポートして可能性があります。

-   HIDDeviceManagePower

センサー ドライバーでは、単純なセンサー (たとえば、I2C または SPI) をサポートする場合は、次のメソッドをサポートして可能性があります。

-   SpbSensorPollData
-   SpbSensorDeviceEvent

## <a name="driver-structures-and-enumerations"></a>ドライバーの構造および列挙体


HID ドライバーでは、入力のレポートをサポートします。 擬似コードでは、次のデータ構造を使用して、レポートを表します。

```cpp
struct _inputReport
{
    reportID
    senstate
    eventType
    sensorData //this varies from sensor to sensor

} buffer, pbuffer
```

センサー ドライバーは、クライアント データを保存します。 擬似コードでは、次のデータ構造を使用して、クライアント データを保存します。

```cpp
struct clientEntry
{
    clientCRI
    clientCS[]
    clientLDA
    clientSubscribed
}
```

センサー ドライバーは、デバイスの状態を表す必要があります。 擬似コードでは、次の列挙を使用して、デバイスの状態を表します。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

センサー ドライバーは、デバイスの状態を表す必要があります。 擬似コードでは、次の列挙を使用して、デバイスの状態を表します。

```cpp
enum deviceState
{
    deviceStateDisconnected // driver is disconnected from the device
    deviceStateConnected //driver is connected to the device
}
```

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)



