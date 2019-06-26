---
title: WDI_TLV_INDICATION_WAKE_REASON
description: WDI_TLV_INDICATION_WAKE_REASON は、NDIS_STATUS_WDI_INDICATION_WAKE_REASON のウェイク アップの理由を含む TLV です。
ms.assetid: 3D3F93EA-4733-44FC-9CB3-721F0552F3E2
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_WAKE_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 154a4eac601e9f9f76413f040664ed61afb3526f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380780"
---
# <a name="wditlvindicationwakereason"></a>WDI\_TLV\_INDICATION\_WAKE\_理由


WDI\_TLV\_を示す値\_WAKE\_理由は、ウェイク アップの理由を含む TLV [NDIS\_状態\_WDI\_INDICATION\_WAKE\_理由](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-wake-reason)します。

## <a name="tlv-type"></a>TLV 型


0x9C

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                |
|--------|----------------------------|
| UINT32 | ウェイク アップの理由を指定します。 |

 

有効なスリープ解除理由の値は次のとおりです。

| ウェイク アップの理由                                       | Value  | 説明                                                                                                          |
|---------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------|
| WDI\_WAKE\_理由\_コード\_パケット                   | 0x0001 | 受信したパケットでは、ウェイク アップのパターンと一致します。                                                                          |
| WDI\_WAKE\_理由\_コード\_メディア\_切断        | 0x0002 | メディア切断します。                                                                                                 |
| WDI\_WAKE\_理由\_コード\_メディア\_接続           | 0x0003 | メディア接続します。                                                                                                    |
| WDI\_WAKE\_理由\_コード\_NLO\_検出           | 0x1000 | NLO 検出します。                                                                                                       |
| WDI\_WAKE\_理由\_コード\_AP\_アソシエーション\_LOST    | 0x1001 | アクセス ポイントの関連付けが失われました。                                                                                       |
| WDI\_WAKE\_理由\_コード\_GTK\_ハンドシェイク\_エラー    | 0x1002 | GTK ハンドシェイク エラーです。                                                                                                 |
| WDI\_WAKE\_理由\_コード\_4 WAY\_ハンドシェイク\_要求 | 0x1003 | 4 ウェイ ハンドシェイク要求。                                                                                             |
| WDI\_WAKE\_理由\_コード\_高速\_要求           | 0x1004 | 将来使用するために予約されています。                                                                                             |
| WDI\_WAKE\_理由\_コード\_受信\_M1           | 0x1005 | WDI を使用して、\_WAKE\_理由\_コード\_4 way\_ハンドシェイク\_代わりに要求します。                                                       |
| WDI\_WAKE\_理由\_コード\_ファームウェア\_STALLED        | 0x1010 | ファームウェアのハングが (たとえば、ウォッチドッグ タイマー) によって検出され、ウェイク ロジックがまだホストをスリープ解除する機能します。 |
| WDI\_WAKE\_理由\_コード\_GTK\_ハンドシェイク\_要求  | 0x1020 | キーのキー更新要求をグループ化します。                                                                                             |

 

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

 

 




