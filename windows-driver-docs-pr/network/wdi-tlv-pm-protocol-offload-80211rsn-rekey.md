---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY では、キーを再入力 RSN プロトコル オフロード パラメーターを含む TLV です。
ms.assetid: 4FDB56EA-444B-4EA2-B8D1-5E740734EEED
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 72033a9acd362cc10e77814e659e3b8ef8a92d8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553558"
---
# <a name="wditlvpmprotocoloffload80211rsnrekey"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_キー更新


WDI\_TLV\_PM\_プロトコル\_オフロード\_80211RSN\_RSN キーを再入力プロトコル オフロード パラメーターを含む TLV キー更新ができます。 ドライバーがでクエリを実行するときに返す必要があります TCK/iGTK キー情報が構成されている場合[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)この TLV を使用しています。

## <a name="tlv-type"></a>TLV 型


など

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類 | 説明  |
| --- | --- |
| [WDI_TLV_RSN_KEY_INFO](wdi-tlv-rsn-key-info.md) | Rsn Eapol キー パラメーター。 |
| LIST<[WDI_TLV_CONFIGURED_CIPHER_KEY](wdi-tlv-configured-cipher-key.md)> | 設定する構成済みの暗号のリスト[OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)します。 ドライバーは、現在構成されている GTK または iGTK キーを返す必要があります。 |

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




