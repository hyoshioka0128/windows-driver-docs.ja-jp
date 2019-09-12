---
title: プラグ アンド プレイのマイナー IRP
description: プラグ アンド プレイのマイナー IRP
ms.date: 08/12/2017
ms.assetid: eeb7dafd-fb44-4fb7-b5f0-314059ee0093
ms.localizationpriority: medium
ms.openlocfilehash: 356aa08a1c06571a401545050b93de0caa87721c
ms.sourcegitcommit: 9b0ddcdba8c56987b45e538948b2ac8c60ef1287
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70876930"
---
# <a name="plug-and-play-minor-irps"></a>プラグ アンド プレイのマイナー IRP





このセクションでは、ドライバーに送信される PnP Irp について説明します。 すべての pnp irp には、主要な関数コードの[ **\_IRP MJ\_PnP**](irp-mj-pnp.md)と、特定の pnp 要求を示すマイナー関数コードがあります。

ここでは、個々の Irp に関するリファレンス情報を提供します。 Irp が送信される順序の説明、 [DispatchPnP ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines)での irp の処理方法の説明、PnP の概念と用語に関する一般的な説明については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

各 IRP および各種類のドライバーについて、IRP を処理するためにドライバーが必要であるか、必要に応じて IRP を処理するか、または IRP を処理しないようにする必要があります。 次の表を参照して、ドライバーが処理する Irp を特定し、各 Irp の詳細についてリファレンスページを参照してください。 Irp は、テーブル内の機能順と、IRP 参照ページのアルファベット順で一覧表示されます。

特定のドライバーのテーブルで IRP が "No" とマークされている場合、そのドライバーは IRP を処理できません。 IRP の参照ページで説明されているように、ドライバーは IRP をデバイススタックの次のドライバーに渡す必要があります。

これらの Irp は、PnP マネージャーによって送信されます。 PnP ドライバーはこれらの Irp の一部を送信できますが、このセクションに記載されているもののみを送信できます。

PnP Irp のマイナー関数コードとそれらを処理するドライバーの種類を次に示します。


|                              PnP IRP minor 関数コード                              | 非バスデバイス用の関数またはフィルタードライバー | バスデバイス用の関数ドライバー (bus FDO 用) | バスドライバーまたはバスフィルタードライバー (子 PDOs 用) |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|
|                 [**IRP\_の全\_開始デバイス\_** ](irp-mn-start-device.md)                  |                  必須                   |                   必須                   |                     必須                     |
|            [**IRP\_の全クエリ\_の停止\_デバイス\_** ](irp-mn-query-stop-device.md)            |                  必須                   |                   必須                   |                     必須                     |
|                  [**IRP\_の全\_停止デバイス\_** ](irp-mn-stop-device.md)                   |                  必須                   |                   必須                   |                     必須                     |
|           [**IRP が終了し\_たときにデバイスを停止する\_\_\_** ](irp-mn-cancel-stop-device.md)           |                  必須                   |                   必須                   |                     必須                     |
|          [**IRP\_を実行\_する\_クエリデバイスの削除\_** ](irp-mn-query-remove-device.md)          |                  必須                   |                   必須                   |                     必須                     |
|                [**IRP\_のすべてのデバイスの削除\_\_** ](irp-mn-remove-device.md)                 |                  必須                   |                   必須                   |                     必須                     |
|         [**IRP を終了する\_デバイスの削除\_\_\_** ](irp-mn-cancel-remove-device.md)         |                  必須                   |                   必須                   |                     必須                     |
|             [**IRP\_の突然\_の削除\_** ](irp-mn-surprise-removal.md)              |                  必須                   |                   必須                   |                     必須                     |
|           [**IRP\_の全\_クエリ機能\_** ](irp-mn-query-capabilities.md)            |                  省略可                   |              省略可 | 必須               |                                                  |
|      [ **\_IRPの全クエリ\_のPNP\_デバイス\_の状態\_** ](irp-mn-query-pnp-device-state.md)       |                  省略可                   |                   省略可能                   |                     省略可                     |
| [**IRP\_の全フィルター\_のリソース\_要件\_** ](irp-mn-filter-resource-requirements.md) |                省略可能 (1)                 |                 省略可能 (1)                 |                        いいえ                        |
|    [**IRP\_デバイス使用量\_の通知\_\_** ](irp-mn-device-usage-notification.md)    |                必須 (1)                 |                 必須 (1)                 |                   必須 (1)                   |
|       [**IRP\_の全クエリ\_のデバイス\_の関係\_** ](irp-mn-query-device-relations.md)       |                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |                省略可能 (1)                 |                   必須                   |                      いいえ (2)                      |
|                               -   **EjectionRelations**                               |                     いいえ                      |                      X                      |                     省略可                     |
|                               -   **RemovalRelations**                                |                  省略可                   |                   オプション                   |                        いいえ                        |
|                             -   **TargetDeviceRelation**                              |                     いいえ                      |                      X                      |                     必須                     |
|              [**IRP\_の全\_クエリリソース\_** ](irp-mn-query-resources.md)               |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|  [**IRP\_の全クエリ\_のリソース\_要件\_** ](irp-mn-query-resource-requirements.md)  |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                     [**IRP\_の全\_クエリ ID\_** ](irp-mn-query-id.md)                      |                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |                     いいえ                      |                      X                      |                     必須                     |
|                              -   **Busqueryハードウェア Id**                              |                     いいえ                      |                      X                      |                     省略可                     |
|                             -   **Busquery互換 Id**                             |                     いいえ                      |                  X  |  省略可                  |                                                  |
|                              -   **BusQueryInstanceID**                               |                     いいえ                      |                      X                      |                     省略可                     |
|                              -   **BusQueryContainerID**                              |                     いいえ                      |                      いいえ                      |                   必須 (3)                   |
|            [**IRP\_の全クエリ\_のデバイス\_テキスト\_** ](irp-mn-query-device-text.md)            |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|        [**IRP\_の全クエリ\_バス情報\_\_** ](irp-mn-query-bus-information.md)        |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|              [**IRP\_の全\_クエリインターフェイス\_** ](irp-mn-query-interface.md)               |                  省略可                   |                   省略可                   |                   必須 (1)                   |
|                  [**IRP\_の読み取り\_の構成\_** ](irp-mn-read-config.md)                   |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                 [**IRP\_の全書き込み\_の構成\_** ](irp-mn-write-config.md)                  |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|            [**IRP\_全デバイス\_列挙型\_** ](irp-mn-device-enumerated.md)             |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                     [**IRP\_の全セット\_のロック\_** ](irp-mn-set-lock.md)                      |                     いいえ                      |                      いいえ                      |                   必須 (1)                   |

(1) 特定の状況では必須または省略可能。 詳細については、IRP のリファレンスページを参照してください。

(2) バスフィルタードライバーが**Busrelations**のクエリを処理する場合があります。

(3) Windows 7 以降のバージョンの Windows でサポートされています。










