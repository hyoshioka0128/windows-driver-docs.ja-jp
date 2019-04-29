---
title: NDIS_STATUS_WDI_INDICATION_IHV_EVENT
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_IHV_EVENT を使用して、IHV 機能拡張のモジュールを IHV 固有の情報を渡します。
ms.assetid: 767f15cd-456f-4d91-9b78-58f8f8b7a465
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_IHV_EVENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e938600e5c196788fd8831bb9c086b754df27e3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390724"
---
# <a name="ndisstatuswdiindicationihvevent"></a>NDIS\_状態\_WDI\_INDICATION\_IHV\_イベント


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_IHV\_IHV 固有の情報を IHV 機能拡張のモジュールに渡すイベント。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                           |
|------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_IHV\_データ**](https://msdn.microsoft.com/library/windows/hardware/dn926312) |                                | x        | IHV 機能拡張のモジュールに送信するイベントです。 |

 

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

 

 




