---
title: OID_WDI_SET_CONNECTION_QUALITY
description: OID_WDI_SET_CONNECTION_QUALITY では、特定の仮想化されたポートの接続の品質を強制する IHV コンポーネントにヒントを提供します。 このヒントは、さまざまなシナリオでのチャネルの使用を最適化するポートを許可します。
ms.assetid: 753e25c5-44b5-4afa-8769-49f693472aa9
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_CONNECTION_QUALITY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e96aabf2a7b13522639d042f016a5aab50852aff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353647"
---
# <a name="oidwdisetconnectionquality"></a>OID\_WDI\_設定\_接続\_品質


OID\_WDI\_設定\_接続\_品質は、特定の仮想化されたポートの接続の品質を強制する IHV コンポーネントにヒントを提供します。 このヒントは、さまざまなシナリオでのチャネルの使用を最適化するポートを許可します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

**注**  このプロパティは、他のプロパティまたはアダプターに発行されたタスクとの競合を引き起こす可能性のあるサービス ヒントのデータ パスの品質を指定します。

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                                       | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_接続\_品質\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connection-quality-parameters)                           |                                |          | 必要な Wi-fi 接続品質ヒント。                                                                                                                                                     |
| [**WDI\_TLV\_低\_待機時間\_接続\_品質\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters) |                                | x        | 接続品質の低待機時間の動作です。 これは、接続の品質は に設定されているかどうかに必要な[ **WDI\_接続\_品質\_低\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint)します。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




