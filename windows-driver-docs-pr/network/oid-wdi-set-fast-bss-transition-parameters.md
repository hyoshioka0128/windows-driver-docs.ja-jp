---
title: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS
description: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS は NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED への応答で送信されます。 (Re) を送信するために必要なパラメーターを持つアソシエーション要求。 コマンドは、直接 OID としてドライバーに送信されます。
ms.assetid: D769E49D-C565-41CD-9C91-195B1223AE66
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a0a4099a4aec594c70bebeaca39582a1cfb8e9a7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903610"
---
# <a name="oidwdisetfastbsstransitionparameters"></a>OID\_WDI\_設定\_高速\_BSS\_遷移\_パラメーター


OID\_WDI\_設定\_高速\_BSS\_遷移\_パラメーターへの応答で送信[NDIS\_状態\_WDI\_INDICATION\_FT\_ASSOC\_PARAMS\_必要](ndis-status-wdi-indication-ft-assoc-params-needed.md)します。 (Re) を送信するために必要なパラメーターを持つアソシエーション要求。 コマンドは、直接 OID としてドライバーに送信されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                    |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/dn898068)      |                                |          | この状態が成功である場合、残りのフィールド (RSNIE、MDE、FTE) は存在します。 これは、問題またはエラー (たとえば、MIC チェック失敗) 認証の応答がないと、IHV の再関連付け要求を続行することを示します。 |
| [**WDI\_TLV\_FT\_RSNIE**](https://msdn.microsoft.com/library/windows/hardware/mt269125) |                                | x        | RSN IE バイト blob。                                                                                                                                                                                                                                          |
| [**WDI\_TLV\_FT\_MDE**](https://msdn.microsoft.com/library/windows/hardware/mt269120)     |                                | x        | MDE バイト blob。                                                                                                                                                                                                                                             |
| [**WDI\_TLV\_FT\_FTE**](https://msdn.microsoft.com/library/windows/hardware/mt269118)     |                                | x        | FTE バイト blob。                                                                                                                                                                                                                                             |

 

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

 

 




