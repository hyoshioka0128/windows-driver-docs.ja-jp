---
title: OID_WDI_SET_ASSOCIATION_PARAMETERS
description: OID_WDI_SET_ASSOCIATION_PARAMETERS には、アダプターは、一連の Bssid に関連付けの際に使用できるパラメーターを指定します。
ms.assetid: 86a6cc62-eaa4-435c-af6c-b76591d92c00
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ASSOCIATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6bc9dadde9fbe77dcb0152a1e569c8689c495661
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574584"
---
# <a name="oidwdisetassociationparameters"></a>OID\_WDI\_設定\_アソシエーション\_パラメーター


OID\_WDI\_設定\_アソシエーション\_パラメーターが、アダプターは、一連の Bssid に関連付けの際に使用できるパラメーターを指定します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | いいえ                       | 1                               |

 

このコマンドは、以前に構成された BSSID 固有の関連付けパラメーターの一覧を置き換えます。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                     |
|-------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI\_TLV\_CONNECT\_BSS\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/dn926264) | x                              |          | BSS エントリとパラメーター。 |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
必要条件
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

 

 




