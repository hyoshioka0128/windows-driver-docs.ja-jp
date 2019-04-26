---
title: OID_WDI_SET_ADD_CIPHER_KEYS
description: OID_WDI_SET_ADD_CIPHER_KEYS を追加またはポートのキー テーブル内の暗号キーを上書きします。 これは、設定専用のプロパティです。
ms.assetid: d10fc976-9e51-4bbb-8f29-caf8c600618a
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADD_CIPHER_KEYS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 31e580b6e77cf8d353184c625690ec9782b7cc2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342968"
---
# <a name="oidwdisetaddcipherkeys"></a>OID\_WDI\_設定\_追加\_暗号\_キー


OID\_WDI\_設定\_追加\_暗号\_キーを追加またはポートのキー テーブル内の暗号キーを上書きします。 これは、設定専用のプロパティです。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

静的な必要があります、ローミングをクリアできませんとしてマークされている暗号キー。 クリアすることができますのみ、 [OID\_WDI\_タスク\_DOT11\_リセット](oid-wdi-task-dot11-reset.md)新しい OID で上書きされる場合または\_WDI\_設定\_追加\_暗号\_キー。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                          | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                              |
|------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------|
| [**WDI\_TLV\_設定\_暗号\_キー\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn898056) | x                              |          | 追加またはポートのキーのテーブルを上書きする暗号キー。 |

 

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


[OID\_WDI\_設定\_削除\_暗号\_キー](oid-wdi-set-delete-cipher-keys.md)

 

 




