---
title: OID_WDI_SET_ADD_WOL_PATTERN
description: OID_WDI_SET_ADD_WOL_PATTERN では、ファームウェアに wake on LAN (WOL) パターンを追加します。
ms.assetid: 96fb71fd-412b-4013-b3bc-c31a43516f55
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_ADD_WOL_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5f1cec01cc2d6baa379f72e732375453519ba19e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557461"
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
| [**WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン**](https://msdn.microsoft.com/library/windows/hardware/dn898084)                       | X                              | X        | WOL パターン情報。                      |
| [**WDI\_TLV\_WAKE\_パケット\_マジック\_パケット**](https://msdn.microsoft.com/library/windows/hardware/dn898185)                           |                                | X        | マジック パケットのパターンの ID。               |
| [**WDI\_TLV\_WAKE\_PACKET\_IPv4\_TCP\_SYNC**](https://msdn.microsoft.com/library/windows/hardware/dn898089)                        | X                              | X        | WOL IPv4 TCP 同期パケット情報。         |
| [**WDI\_TLV\_WAKE\_パケット\_IPv6\_TCP\_同期**](https://msdn.microsoft.com/library/windows/hardware/dn898091)                        | X                              | X        | WOL IPv4 TCP 同期パケット情報。         |
| [**WDI\_TLV\_WAKE\_パケット\_EAPOL\_要求\_ID\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/dn898087) |                                | X        | WOL EAPOL 要求の ID のメッセージの ID をパターンです。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_削除\_WOL\_パターン](oid-wdi-set-remove-wol-pattern.md)

 

 




