---
title: OID_WDI_SET_DELETE_CIPHER_KEYS
description: OID_WDI_SET_DELETE_CIPHER_KEYS では、デバイスの暗号化キーのテーブルから暗号キーを削除します。
ms.assetid: 0a8d4625-382b-4976-aa3f-a8fea0976a00
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_DELETE_CIPHER_KEYS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 26c506035d61731c2aa5d75b87cf23761e52d60a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387253"
---
# <a name="oidwdisetdeletecipherkeys"></a>OID\_WDI\_設定\_削除\_暗号\_キー


OID\_WDI\_設定\_削除\_暗号\_キーの削除、デバイスの暗号化キーのテーブルからキーの暗号です。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI\_TLV\_削除\_暗号\_キー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-delete-cipher-key-info) | x                              |          | デバイスのキー テーブルから削除する暗号キー。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_追加\_暗号\_キー](oid-wdi-set-add-cipher-keys.md)

 

 




