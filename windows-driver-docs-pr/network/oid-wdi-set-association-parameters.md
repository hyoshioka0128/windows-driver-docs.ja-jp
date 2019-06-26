---
title: OID_WDI_SET_ASSOCIATION_PARAMETERS
description: OID_WDI_SET_ASSOCIATION_PARAMETERS には、アダプターは、一連の Bssid に関連付けの際に使用できるパラメーターを指定します。
ms.assetid: 86a6cc62-eaa4-435c-af6c-b76591d92c00
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ASSOCIATION_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 681cc68754495e492b7593b3f862a0aa331811d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353653"
---
# <a name="oidwdisetassociationparameters"></a>OID\_WDI\_設定\_アソシエーション\_パラメーター


OID\_WDI\_設定\_アソシエーション\_パラメーターが、アダプターは、一連の Bssid に関連付けの際に使用できるパラメーターを指定します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | X                       | 1                               |

 

このコマンドは、以前に構成された BSSID 固有の関連付けパラメーターの一覧を置き換えます。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                     |
|-------------------------------------------------------------------------|--------------------------------|----------|---------------------------------|
| [**WDI\_TLV\_CONNECT\_BSS\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-bss-entry) | x                              |          | BSS エントリとパラメーター。 |

 

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

 

 




