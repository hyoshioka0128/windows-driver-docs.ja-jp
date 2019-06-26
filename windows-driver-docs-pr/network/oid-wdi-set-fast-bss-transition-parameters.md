---
title: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS
description: OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS は NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED への応答で送信されます。 (Re) を送信するために必要なパラメーターを持つアソシエーション要求。 コマンドは、直接 OID としてドライバーに送信されます。
ms.assetid: D769E49D-C565-41CD-9C91-195B1223AE66
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_FAST_BSS_TRANSITION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0b10d48664ad432f0f0c7255df77f57400389836
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381206"
---
# <a name="oidwdisetfastbsstransitionparameters"></a>OID\_WDI\_設定\_高速\_BSS\_遷移\_パラメーター


OID\_WDI\_設定\_高速\_BSS\_遷移\_パラメーターへの応答で送信[NDIS\_状態\_WDI\_INDICATION\_FT\_ASSOC\_PARAMS\_必要](ndis-status-wdi-indication-ft-assoc-params-needed.md)します。 (Re) を送信するために必要なパラメーターを持つアソシエーション要求。 コマンドは、直接 OID としてドライバーに送信されます。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                    |
|------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-status)      |                                |          | この状態が成功である場合、残りのフィールド (RSNIE、MDE、FTE) は存在します。 これは、問題またはエラー (たとえば、MIC チェック失敗) 認証の応答がないと、IHV の再関連付け要求を続行することを示します。 |
| [**WDI\_TLV\_FT\_RSNIE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-rsnie) |                                | x        | RSN IE バイト blob。                                                                                                                                                                                                                                          |
| [**WDI\_TLV\_FT\_MDE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-mde)     |                                | x        | MDE バイト blob。                                                                                                                                                                                                                                             |
| [**WDI\_TLV\_FT\_FTE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-fte)     |                                | x        | FTE バイト blob。                                                                                                                                                                                                                                             |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。

<a name="requirements"></a>必要条件
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

 

 




