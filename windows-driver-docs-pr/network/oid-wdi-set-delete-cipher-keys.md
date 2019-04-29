---
title: OID_WDI_SET_DELETE_CIPHER_KEYS
description: OID_WDI_SET_DELETE_CIPHER_KEYS では、デバイスの暗号化キーのテーブルから暗号キーを削除します。
ms.assetid: 0a8d4625-382b-4976-aa3f-a8fea0976a00
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_DELETE_CIPHER_KEYS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 58390ab614bca413053e178fe572dd29ce95a39c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365773"
---
# <a name="oidwdisetdeletecipherkeys"></a>OID\_WDI\_設定\_削除\_暗号\_キー


OID\_WDI\_設定\_削除\_暗号\_キーの削除、デバイスの暗号化キーのテーブルからキーの暗号です。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI\_TLV\_削除\_暗号\_キー\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn926283) | x                              |          | デバイスのキー テーブルから削除する暗号キー。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_追加\_暗号\_キー](oid-wdi-set-add-cipher-keys.md)

 

 




