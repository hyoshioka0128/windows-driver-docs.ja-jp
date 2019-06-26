---
title: OID_WDI_SET_ADD_WOL_PATTERN
description: OID_WDI_SET_ADD_WOL_PATTERN では、ファームウェアに wake on LAN (WOL) パターンを追加します。
ms.assetid: 96fb71fd-412b-4013-b3bc-c31a43516f55
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADD_WOL_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a195f4555e5b1be337b586a84521ebba5f5d2535
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387251"
---
# <a name="oidwdisetaddwolpattern"></a>OID\_WDI\_設定\_追加\_WOL\_パターン


OID\_WDI\_設定\_追加\_WOL\_パターンのファームウェアに wake on LAN (WOL) パターンを追加します。

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|-------|--------------------------|---------------------------------|
| ポート  | 〇                      | 1                               |

 

ホストは、ファームウェアに追加するパケットのパターンの種類を定義します。 ファームウェアでは、Dx で到着する一致するパケットを検出します。 検出された場合、ファームウェアはウェイク割り込みをアサートします。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-bitmap-pattern)                       | x                              | x        | WOL パターン情報。                      |
| [**WDI\_TLV\_WAKE\_パケット\_マジック\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-magic-packet)                           |                                | x        | マジック パケットのパターンの ID。               |
| [**WDI\_TLV\_WAKE\_PACKET\_IPv4\_TCP\_SYNC**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-ipv4-tcp-sync)                        | x                              | x        | WOL IPv4 TCP 同期パケット情報。         |
| [**WDI\_TLV\_WAKE\_パケット\_IPv6\_TCP\_同期**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-ipv6-tcp-sync)                        | x                              | x        | WOL IPv4 TCP 同期パケット情報。         |
| [**WDI\_TLV\_WAKE\_パケット\_EAPOL\_要求\_ID\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-wake-packet-eapol-request-id-message) |                                | x        | WOL EAPOL 要求の ID のメッセージの ID をパターンです。 |

 

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


[OID\_WDI\_設定\_削除\_WOL\_パターン](oid-wdi-set-remove-wol-pattern.md)

 

 




