---
title: OID_WDI_SET_CONNECTION_QUALITY
description: OID_WDI_SET_CONNECTION_QUALITY は、特定の仮想ポートに対して接続品質を適用するためのヒントを IHV コンポーネントに提供します。 このヒントを使用すると、ポートはさまざまなシナリオでチャネルの使用を最適化できます。
ms.assetid: 753e25c5-44b5-4afa-8769-49f693472aa9
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_CONNECTION_QUALITY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 55b26e6ee5a8045d395845570bb6eb9af8f82bf4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843875"
---
# <a name="oid_wdi_set_connection_quality"></a>OID\_WDI\_設定\_接続\_品質


OID\_WDI\_SET\_CONNECTION\_QUALITY は、特定の仮想ポートの接続品質を適用するために、IHV コンポーネントにヒントを提供します。 このヒントを使用すると、ポートはさまざまなシナリオでチャネルの使用を最適化できます。

| 適用範囲 | タスクでシリアル化された設定 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | [はい]                      | 1                               |

 

この**プロパティ  、** サービスヒントのデータパスの品質を指定します。これにより、アダプターに発行された他のプロパティやタスクとの競合が発生する可能性があります。

 

## <a name="set-property-parameters"></a>プロパティパラメーターの設定


| TLV                                                                                                                       | 複数の TLV インスタンスを使用できます | オプション | 説明                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_接続\_品質\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-quality-parameters)                           |                                |          | 必要な Wi-fi 接続品質ヒント。                                                                                                                                                     |
| [**WDI\_TLV\_低\_待機時間\_接続\_品質\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters) |                                | X        | 低待機時間の接続品質の動作。 これは、接続の品質が WDI に設定されている場合にのみ必要です。 [ **\_接続\_品質\_低\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)です。 |

 

## <a name="set-property-results"></a>プロパティの結果の設定


その他のデータはありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

 




