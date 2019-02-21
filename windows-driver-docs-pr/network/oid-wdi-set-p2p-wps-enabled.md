---
title: OID_WDI_SET_P2P_WPS_ENABLED
description: OID_WDI_SET_P2P_WPS_ENABLED 要求アダプターが有効にしたり、NIC で、Wi-fi Protected セットアップ (WPS) を無効にします。
ms.assetid: 96F21807-464F-4B50-AF7E-779F6BF6FE37
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_P2P_WPS_ENABLED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8c2a7dd1decd9ba925f1bc0fb9ed427e354d0865
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560207"
---
# <a name="oidwdisetp2pwpsenabled"></a>OID\_WDI\_設定\_P2P\_WPS\_有効


OID\_WDI\_設定\_P2P\_WPS\_有効要求アダプターが有効にしたり、NIC で、Wi-fi Protected セットアップ (WPS) を無効にします。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                 |
|---------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------|
| [**WDI\_TLV\_P2P\_WPS\_有効**](https://msdn.microsoft.com/library/windows/hardware/dn898018) |                                |          | 有効または WPS を無効にするかどうかを指定します。 |

 

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

 

 




