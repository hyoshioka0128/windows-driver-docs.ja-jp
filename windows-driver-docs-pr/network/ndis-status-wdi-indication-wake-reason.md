---
title: NDIS_STATUS_WDI_INDICATION_WAKE_REASON
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_WAKE_REASON を使用して NIC は、ホストをスリープ解除時に、ウェイクの理由を示します。 ウェイク アップの理由は、デバッグ目的で使用され、機能の影響を与えません。
ms.assetid: 5f2eb569-be1e-4f24-92f5-8405ffc7b061
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_WAKE_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 48459164e04bdfdfe304b7da4b506acd624ec82a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560888"
---
# <a name="ndisstatuswdiindicationwakereason"></a>NDIS\_状態\_WDI\_INDICATION\_WAKE\_理由


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_WAKE\_NIC は、ホストをスリープ解除時に、ウェイクの理由を示す理由。 ウェイク アップの理由は、デバッグ目的で使用され、機能の影響を与えません。

| オブジェクト |
|--------|
| ポート   |

 

低電力状態になると、ホスト、ときに、NIC にいくつかの関数の負荷を軽減し、ウェイク アップの NIC を準備します。 ウェイク イベントが発生したときに、NIC は、ホストをウェイクするためウェイク割り込み行をアサートします。 ホストは、し (電源の状態を実行している) D0 に NIC を表示します。 NIC は、D0 に入った、ウェイク アップの理由を示す必要があります。

ウェイク アップの理由がウェイク アップ パケットの場合は、NIC は、ウェイク アップ パケットと、パケットに一致するウェイク パターン ID に含めるも必要があります。 パケットとしてカプセル化[ **WDI\_TLV\_INDICATION\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/dn897833)します。 ウェイク アップの理由を含める必要がありますも[ **WDI\_TLV\_INDICATION\_WAKE\_パケット\_パターン\_ID** ](https://msdn.microsoft.com/library/windows/hardware/dn897832)にパケットに一致するパターンの ID を指定します。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/dn897834)                         |                                |          | ウェイク アップの理由です。                                                                                            |
| [**WDI\_TLV\_INDICATION\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/dn897833)                         |                                | X        | ウェイク アップ パケットです。                                                                                            |
| [**WDI\_TLV\_INDICATION\_WAKE\_パケット\_パターン\_ID**](https://msdn.microsoft.com/library/windows/hardware/dn897832) |                                | X        | ウェイク アップ パケットに一致するパターンの ID。 ID は、パターンの追加 コマンドから取得されます。 |

 

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

 

 




