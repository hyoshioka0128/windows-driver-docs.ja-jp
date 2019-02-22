---
title: OID_WDI_SET_DEFAULT_KEY_ID
description: OID_WDI_SET_DEFAULT_KEY_ID パケットの送信ポートでの ID を既定のキーを設定します。
ms.assetid: 5112a661-3560-4070-b74a-0027e3adfac1
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_DEFAULT_KEY_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 04cb39057f3f85898eebab6b0892fd0d511be404
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537907"
---
# <a name="oidwdisetdefaultkeyid"></a>OID\_WDI\_設定\_既定\_キー\_ID


OID\_WDI\_設定\_既定\_キー\_パケットの送信ポートでの ID を既定のキー ID を設定します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                             |
|-------------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------|
| [**WDI\_TLV\_既定\_TX\_キー\_ID\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn926281) |                                |          | 既定値は、パケットの送信ポートでの ID をキーします。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
要件
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

 

 




