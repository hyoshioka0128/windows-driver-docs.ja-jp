---
title: OID_WDI_SET_P2P_WPS_ENABLED
description: OID_WDI_SET_P2P_WPS_ENABLED 要求アダプターが有効にしたり、NIC で、Wi-fi Protected セットアップ (WPS) を無効にします。
ms.assetid: 96F21807-464F-4B50-AF7E-779F6BF6FE37
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_P2P_WPS_ENABLED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6e4d7b3e46fb0c3cfdbbcb80bafa022b6413b7f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359191"
---
# <a name="oidwdisetp2pwpsenabled"></a>OID\_WDI\_設定\_P2P\_WPS\_有効


OID\_WDI\_設定\_P2P\_WPS\_有効要求アダプターが有効にしたり、NIC で、Wi-fi Protected セットアップ (WPS) を無効にします。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                 |
|---------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_P2P\_WPS\_有効**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-wps-enabled) |                                |          | 有効または WPS を無効にするかどうかを指定します。 |

 

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

 

 




