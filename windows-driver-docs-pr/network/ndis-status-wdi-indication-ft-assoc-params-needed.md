---
title: NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED
description: ミニポート ドライバーでは、ローミング 802.11r の要求パラメーターを NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED を使用します。ObjectPort します。
ms.assetid: AB745908-AA7B-416A-9C97-B376293F3DEE
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b636ac0f613a4f5b10e2e51338709e4708db3e90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354943"
---
# <a name="ndisstatuswdiindicationftassocparamsneeded"></a>NDIS\_状態\_WDI\_INDICATION\_FT\_ASSOC\_PARAMS\_が必要


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_FT\_ASSOC\_PARAMS\_にローミング 802.11r の要求パラメーターが必要です。

| オブジェクト |
|--------|
| ポート   |

 

中に[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)WDI、802.11 認証要求 (PmkR0Name、R0KH ID、SNonce、MDIE) を送信するパラメーターを提供します。 認証の応答を受信すると、LE が PMKR1Name と R1KH ID などの再関連付け要求は、必要な追加のパラメーターを要求します。 LE も (ANonce、SNonce、および R1KHID) 認証の応答で受信したパラメーターを送信します。

モビリティの初期のドメインが正常に完了の接続、LE する必要があります 11r ローミング (高速ローミング) のみを実行します。 LE では、オペレーティング システムによって提供される候補リストを使用したり、独自の使用、ローミングすることができます。 LE、独自の候補リストを使用する場合、オペレーティング システムで提案された候補のいずれかで指定したパラメーター (MDE、FTE、および PMKR0Name) を使用して、11r ローミングを行うがあります。 11r、接続が FIPS モードのときに無効です。 現在は 11r 高速ローミング FT 認証の種類 x 1 を超えるのみサポートします。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                            |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)                         |                                |          | AP の BSSID します。                   |
| [**WDI\_TLV\_FT\_AUTH\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-auth-request)   |                                |          | 認証要求のバイト blob。  |
| [**WDI\_TLV\_FT\_AUTH\_応答**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ft-auth-response) |                                |          | 認証応答バイト blob。 |

 

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


[OID\_WDI\_タスク\_ローミング](oid-wdi-task-roam.md)

 

 




