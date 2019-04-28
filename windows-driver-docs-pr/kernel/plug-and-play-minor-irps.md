---
title: プラグ アンド プレイのマイナー IRP
description: プラグ アンド プレイのマイナー IRP
ms.date: 08/12/2017
ms.assetid: eeb7dafd-fb44-4fb7-b5f0-314059ee0093
ms.localizationpriority: medium
ms.openlocfilehash: 9f596962a85f29ddcb1986da40e37d011316bd78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369250"
---
# <a name="plug-and-play-minor-irps"></a>プラグ アンド プレイのマイナー IRP





このセクションには、ドライバーに送信される PnP Irp がについて説明します。 コードが主な機能であるすべての PnP Irp [ **IRP\_MJ\_PNP** ](irp-mj-pnp.md)とマイナー関数を特定の PnP 要求を示すコード。

このセクションでは、個々 の Irp のリファレンス情報を提供します。 参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)Irp が送信される、Irp を処理する方法については、順序の説明については[DispatchPnP ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff543348)、PnP の概念と用語の一般的なディスカッションとします。

各 IRP とドライバーの種類ごとでは、ドライバーとは、IRP を必要に応じて処理できる、IRP を処理するために必要なのか、または IRP を処理する必要があります。 ドライバーは処理し、個々 の Irp については、リファレンス ページを参照する Irp を識別するために次の表を参照してください。 Irp は IRP のリファレンス ページでアルファベット順にテーブルの機能の順序で表示されます。

IRP が"No"テーブルには、特定のドライバーをマークされている場合そのドライバーは IRP を処理する必要があります。 ドライバーは IRP のリファレンス ページの説明に従って、デバイス スタックでは、次のドライバーに IRP を渡す必要があります。

Irp これら PnP マネージャーに送信します。 PnP ドライバーには、だけのこのセクションではそのように記載されますが、これらの Irp の一部を送信できます。

次に、PnP Irp、およびその処理を行うドライバーの種類のマイナー関数コードを示します。


|                              PnP IRP マイナー関数コード                              | Nonbus デバイス用の関数またはフィルター ドライバー | バスのデバイス (バス FDO) 用のドライバーを関数 | バス ドライバーまたは (子 Pdo) 用のバス フィルター ドライバー |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|
|                 [**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)                  |                  必須                   |                   必須                   |                     必須                     |
|            [**IRP\_MN\_クエリ\_停止\_デバイス**](irp-mn-query-stop-device.md)            |                  必須                   |                   必須                   |                     必須                     |
|                  [**IRP\_MN\_停止\_デバイス**](irp-mn-stop-device.md)                   |                  必須                   |                   必須                   |                     必須                     |
|           [**IRP\_MN\_CANCEL\_STOP\_DEVICE**](irp-mn-cancel-stop-device.md)           |                  必須                   |                   必須                   |                     必須                     |
|          [**IRP\_MN\_クエリ\_削除\_デバイス**](irp-mn-query-remove-device.md)          |                  必須                   |                   必須                   |                     必須                     |
|                [**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)                 |                  必須                   |                   必須                   |                     必須                     |
|         [**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)         |                  必須                   |                   必須                   |                     必須                     |
|             [**IRP\_MN\_SURPRISE\_REMOVAL**](irp-mn-surprise-removal.md)              |                  必須                   |                   必須                   |                     必須                     |
|           [**IRP\_MN\_クエリ\_機能**](irp-mn-query-capabilities.md)            |                  省略可能                   |              省略可能なために必要な               |                                                  |
|      [**IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)       |                  省略可能                   |                   省略可能                   |                     省略可能                     |
| [**IRP\_MN\_フィルター\_リソース\_要件**](irp-mn-filter-resource-requirements.md) |                省略可能 (1)                 |                 省略可能 (1)                 |                        X                        |
|    [**IRP\_MN\_デバイス\_使用状況\_通知**](irp-mn-device-usage-notification.md)    |                必要な (1)                 |                 必要な (1)                 |                   必要な (1)                   |
|       [**IRP\_MN\_クエリ\_デバイス\_リレーション**](irp-mn-query-device-relations.md)       |                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |                省略可能 (1)                 |                   必須                   |                      いいえ (2)                      |
|                               -   **EjectionRelations**                               |                     X                      |                      X                      |                     省略可能                     |
|                               -   **RemovalRelations**                                |                  省略可能                   |                   省略可能                   |                        X                        |
|                             -   **TargetDeviceRelation**                              |                     X                      |                      X                      |                     必須                     |
|              [**IRP\_MN\_クエリ\_リソース**](irp-mn-query-resources.md)               |                     X                      |                      X                      |                   必要な (1)                   |
|  [**IRP\_MN\_クエリ\_リソース\_要件**](irp-mn-query-resource-requirements.md)  |                     X                      |                      X                      |                   必要な (1)                   |
|                     [**IRP\_MN\_QUERY\_ID**](irp-mn-query-id.md)                      |                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |                     X                      |                      X                      |                     必須                     |
|                              -   **BusQueryHardwareIDs**                              |                     X                      |                      X                      |                     省略可能                     |
|                             -   **BusQueryCompatibleIDs**                             |                     X                      |                  NoOptional                  |                                                  |
|                              -   **BusQueryInstanceID**                               |                     X                      |                      X                      |                     省略可能                     |
|                              -   **BusQueryContainerID**                              |                     X                      |                      X                      |                   必要な (3)                   |
|            [**IRP\_MN\_QUERY\_DEVICE\_TEXT**](irp-mn-query-device-text.md)            |                     X                      |                      X                      |                   必要な (1)                   |
|        [**IRP\_MN\_クエリ\_BUS\_情報**](irp-mn-query-bus-information.md)        |                     X                      |                      X                      |                   必要な (1)                   |
|              [**IRP\_MN\_クエリ\_インターフェイス**](irp-mn-query-interface.md)               |                  省略可能                   |                   省略可能                   |                   必要な (1)                   |
|                  [**IRP\_MN\_READ\_CONFIG**](irp-mn-read-config.md)                   |                     X                      |                      X                      |                   必要な (1)                   |
|                 [**IRP\_MN\_WRITE\_CONFIG**](irp-mn-write-config.md)                  |                     X                      |                      X                      |                   必要な (1)                   |
|            [**IRP\_MN\_デバイス\_列挙**](irp-mn-device-enumerated.md)             |                     X                      |                      X                      |                   必要な (1)                   |
|                     [**IRP\_MN\_SET\_LOCK**](irp-mn-set-lock.md)                      |                     X                      |                      X                      |                   必要な (1)                   |

(1) は、必須または特定の状況では省略可能。 詳細については IRP のリファレンス ページを参照してください。

(バス 2) フィルター ドライバーでのクエリが処理**BusRelations**します。

(3) Windows 7 および Windows の以降のバージョンでサポートされています。










