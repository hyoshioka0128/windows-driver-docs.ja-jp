---
title: NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG
description: ミニポート ドライバー使用 NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG を TCP での変更がある場合を示すためには、ハードウェアの機能をオフロードします。
ms.assetid: 4E73F09A-965F-4F32-AFF7-FDF1E3B2853C
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: edb3daf1f6b4702232ef103d70b08c18df8b844d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372866"
---
# <a name="ndisstatuswdiindicationtaskoffloadcurrentconfig"></a>NDIS\_状態\_WDI\_INDICATION\_タスク\_オフロード\_現在\_構成


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_タスク\_オフロード\_現在\_を TCP での変更がある場合を示すために構成のオフロード機能ハードウェア。

| オブジェクト |
|--------|
| ポート   |

 

TCP の変更、ハードウェアの機能をオフロードする場合は、LE は新しい TCP チェックサム/LSO 機能を備えた、UE に要請されていないこの通知を送信します。 値を使用して**NDIS\_オフロード\_設定\_OFF**と**NDIS\_オフロード\_設定\_ON** 内のメンバーについて[**WDI\_TLV\_TCP\_オフロード\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn898069)変更オフロード機能を示すためです。 UE を送信すると、 [OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](oid-wdi-set-tcp-offload-parameters.md)、LE がオフロード機能を更新する必要があり、し、この通知を送信できるようにOS は、最新のオフロード機能情報で更新されます。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_TCP\_オフロード\_機能**](https://msdn.microsoft.com/library/windows/hardware/dn898069) |                                | x        | TCP/IP のチェックサムと Large Send Offload 機能。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](oid-wdi-set-tcp-offload-parameters.md)

 

 




