---
title: プラグ アンド プレイのマイナー IRP
description: プラグ アンド プレイのマイナー IRP
ms.date: 08/12/2017
ms.assetid: eeb7dafd-fb44-4fb7-b5f0-314059ee0093
ms.localizationpriority: medium
ms.openlocfilehash: 51bffcc98073f05a34b953fef13f8ef533b0980e
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922513"
---
# <a name="plug-and-play-minor-irps"></a>プラグ アンド プレイのマイナー IRP





このセクションでは、ドライバーに送信される PnP Irp について説明します。 すべての PnP Irp には、主要な関数コードの[**\_IRP MJ\_PnP**](irp-mj-pnp.md)と、特定の pnp 要求を示すマイナー関数コードがあります。

ここでは、個々の Irp に関するリファレンス情報を提供します。 Irp が送信される順序の説明、 [DispatchPnP ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines)での irp の処理方法の説明、PnP の概念と用語に関する一般的な説明については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

各 IRP および各種類のドライバーについて、IRP を処理するためにドライバーが必要であるか、必要に応じて IRP を処理するか、または IRP を処理しないようにする必要があります。 次の表を参照して、ドライバーが処理する Irp を特定し、各 Irp の詳細についてリファレンスページを参照してください。 Irp は、テーブル内の機能順と、IRP 参照ページのアルファベット順で一覧表示されます。

特定のドライバーのテーブルで IRP が "No" とマークされている場合、そのドライバーは IRP を処理できません。 IRP の参照ページで説明されているように、ドライバーは IRP をデバイススタックの次のドライバーに渡す必要があります。

これらの Irp は、PnP マネージャーによって送信されます。 PnP ドライバーはこれらの Irp の一部を送信できますが、このセクションに記載されているもののみを送信できます。

PnP Irp のマイナー関数コードとそれらを処理するドライバーの種類を次に示します。


|                              PnP IRP minor 関数コード                              | 値 | 非バスデバイス用の関数またはフィルタードライバー | バスデバイス用の関数ドライバー (bus FDO 用) | バスドライバーまたはバスフィルタードライバー (子 PDOs 用) |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|
|                 [**IRP\_の\_全\_開始デバイス**](irp-mn-start-device.md)                  |0x00|                  必須                   |                   必須                   |                     必須                     |
|          [**IRP\_を\_実行\_する\_クエリデバイスの削除**](irp-mn-query-remove-device.md)          |0x01|                  必須                   |                   必須                   |                     必須                     |
|                [**IRP\_の\_すべて\_のデバイスの削除**](irp-mn-remove-device.md)                 |0x02|                  必須                   |                   必須                   |                     必須                     |
|         [**\_IRP\_を終了\_する\_デバイスの削除**](irp-mn-cancel-remove-device.md)         |0x03|                  必須                   |                   必須                   |                     必須                     |
|                  [**IRP\_の\_全\_停止デバイス**](irp-mn-stop-device.md)                   |0x04|                  必須                   |                   必須                   |                     必須                     |
|            [**IRP\_の\_全\_クエリ\_の停止デバイス**](irp-mn-query-stop-device.md)            |0x05|                  必須                   |                   必須                   |                     必須                     |
|           [**\_IRP\_が\_終了し\_たときにデバイスを停止する**](irp-mn-cancel-stop-device.md)           |0x06|                  必須                   |                   必須                   |                     必須                     |
|       [**IRP\_の\_全\_クエリ\_のデバイスの関係**](irp-mn-query-device-relations.md)       |0x07                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |x|                省略可能 (1)                 |                   必須                   |                      いいえ (2)                      |
|                               -   **EjectionRelations**                               |x|                     いいえ                      |                      いいえ                      |                     省略可能                     |
|                               -   **RemovalRelations**                                |x|                  オプション                   |                   オプション                   |                        いいえ                        |
|                             -   **TargetDeviceRelation**                              |x|                     いいえ                      |                      いいえ                      |                     必須                     |
|              [**IRP\_の\_全\_クエリインターフェイス**](irp-mn-query-interface.md)               |0x08|                  オプション                   |                   オプション                   |                   必須 (1)                   |
|           [**IRP\_の\_全\_クエリ機能**](irp-mn-query-capabilities.md)            |0x09|                  オプション                   |              オプション | 必須               |                                                  |
|              [**IRP\_の\_全\_クエリリソース**](irp-mn-query-resources.md)               |0x0A|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|  [**IRP\_の\_全\_クエリ\_のリソース要件**](irp-mn-query-resource-requirements.md)  |0x0B|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|            [**IRP\_の\_全\_クエリ\_のデバイステキスト**](irp-mn-query-device-text.md)            |0x0C|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
| [**IRP\_の\_全\_フィルター\_のリソース要件**](irp-mn-filter-resource-requirements.md) |0x0D|                省略可能 (1)                 |                 省略可能 (1)                 |                        いいえ                        |
|                  [**IRP\_の\_読み取り\_の構成**](irp-mn-read-config.md)                   |0x0F|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                 [**IRP\_の\_全\_書き込みの構成**](irp-mn-write-config.md)                  |0x10|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                 [**IRP\_の\_全取り出し**](irp-mn-eject.md)                  |0x11|                     いいえ                      |                      いいえ                      |                   必須                   |
|                     [**IRP\_の\_全\_セットのロック**](irp-mn-set-lock.md)                      |0x12|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|                     [**IRP\_の\_全\_クエリ ID**](irp-mn-query-id.md)                      |0x13|                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |x|                     いいえ                      |                      いいえ                      |                     必須                     |
|                              -   **Busqueryハードウェア Id**                              |x|                     いいえ                      |                      いいえ                      |                     省略可能                     |
|                             -   **Busquery互換 Id**                             |x|                     いいえ                      |                  いいえ  |  省略可能                  |                                                  |
|                              -   **BusQueryInstanceID**                               |x|                     いいえ                      |                      いいえ                      |                     省略可能                     |
|                              -   **BusQueryContainerID**                              |x|                     いいえ                      |                      いいえ                      |                   必須 (3)                   |
|      [**IRP\_の\_全\_クエリ\_の\_PNP デバイスの状態**](irp-mn-query-pnp-device-state.md)       |0x14|                  オプション                   |                   オプション                   |                     オプション                     |
|        [**IRP\_の\_全\_クエリ\_バス情報**](irp-mn-query-bus-information.md)        |0x15|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |
|    [**IRP\_\_デバイス\_使用量\_の通知**](irp-mn-device-usage-notification.md)    |0x16|                必須 (1)                 |                 必須 (1)                 |                   必須 (1)                   |
|             [**IRP\_の\_突然\_の削除**](irp-mn-surprise-removal.md)              |0x17|                  必須                   |                   必須                   |                     必須                     |
|            [**IRP\_全\_デバイス\_列挙型**](irp-mn-device-enumerated.md)             |0x19|                     いいえ                      |                      いいえ                      |                   必須 (1)                   |

(1) 特定の状況では必須または省略可能。 詳細については、IRP のリファレンスページを参照してください。

(2) バスフィルタードライバーが**Busrelations**のクエリを処理する場合があります。

(3) Windows 7 以降のバージョンの Windows でサポートされています。










