---
title: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN
description: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN では、次のアクションのフレームで使用される DialogToken を要求します。
ms.assetid: EB5F6077-1566-41AE-B414-9ECF24BAE982
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fceb6564af7d2c38478f110bbcfa06182524adbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353672"
---
# <a name="oidwdigetnextactionframedialogtoken"></a>OID\_WDI\_取得\_次\_アクション\_フレーム\_ダイアログ\_トークン


OID\_WDI\_取得\_次\_アクション\_フレーム\_ダイアログ\_トークンは、次のアクションのフレームで使用される DialogToken を要求します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


| TLV                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明     |
|-------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI\_TLV\_次\_ダイアログ\_トークン**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-next-dialog-token) |                                |          | ダイアログ トークンです。 |

 

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

 

 




