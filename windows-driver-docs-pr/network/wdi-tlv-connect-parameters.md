---
title: WDI_TLV_CONNECT_PARAMETERS
description: WDI_TLV_CONNECT_PARAMETERS は、OID_WDI_TASK_CONNECT と OID_WDI_TASK_ROAM パラメーターを含む TLV です。
ms.assetid: 6B2B4E5D-4BF9-4803-A373-FDF64AD3C99B
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4e3f2119db4c760ac4c1c13c99cf40ee81927439
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570640"
---
# <a name="wditlvconnectparameters"></a>WDI\_TLV\_CONNECT\_パラメーター


WDI\_TLV\_CONNECT\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/dn925948)と[OID\_WDI\_タスク\_ローミング](https://msdn.microsoft.com/library/windows/hardware/dn925958)します。

## <a name="tlv-type"></a>TLV 型


0x33

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値

| 型 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_接続\_設定**](wdi-tlv-connection-settings.md) |   |   | 接続の設定。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md) | x |   | 接続にポートが許可されている Ssid の一覧です。 |
| [**WDI\_TLV\_HESSID**](wdi-tlv-hessid.md) |   | x | 接続にポートが許可されている HESSIDs の一覧です。 これは、SSID の一覧に追加の要件です。 |
| [**WDI\_TLV\_AUTH\_ALGO\_一覧**](wdi-tlv-auth-algo-list.md) |   |   | 接続に使用できる認証アルゴリズムの一覧。 |
| [**WDI\_TLV\_マルチキャスト\_暗号\_ALGO\_一覧**](wdi-tlv-multicast-cipher-algo-list.md) |   |   | 接続を使用するマルチキャストの暗号アルゴリズムの一覧。 |
| [**WDI\_TLV\_ユニキャスト\_暗号\_ALGO\_一覧**](wdi-tlv-unicast-cipher-algo-list.md) |   |   | 接続に使用できるユニキャスト暗号アルゴリズムの一覧。 |
| [**WDI\_TLV\_余分な\_アソシエーション\_要求\_IES**](wdi-tlv-extra-association-request-ies.md) |   | x | ポートによって送信されたアソシエーションの要求に含める必要がある IE blob。 これは、すべて BSSID をデバイスに関連付ける場合に適用されます。 これは、BSSID 特定 IEs に加えて使用する必要があります。 |
| [**WDI\_TLV\_PHY\_型\_一覧**](wdi-tlv-phy-type-list.md) |   | x | 関連付けの使用を許可する物理サイズの一覧。 指定しない場合、サポートされている任意 PHY を使用できます。 指定すると、デバイスに表示されている物理サイズする必要がありますしか使用できません。 |
| [**WDI\_TLV\_許可しない\_BSSID\_一覧**](wdi-tlv-disallowed-bssids-list.md) |   | x | 関連付けに使用するのには許可されていない Bssid の一覧。 指定した場合、アダプターいないこのリストである任意の AP に関連付ける必要があります。 |
| [**WDI\_TLV\_許可\_BSSID\_一覧**](wdi-tlv-allowed-bssids-list.md) |   | x | 関連付けに使用することができる Bssid の一覧。 WDI 255.255.255.255 を指定する場合は、すべて Bssid が許可されます。 | 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>
