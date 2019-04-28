---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: ミニポート ドライバーでは、MB サービスに追加の PDP コンテキストの IP 構成の変更に関する通知 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知を使用します。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_IP_ADDRESS_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6986232ecebdc566ad5fc76afc9f61910f0e42e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377284"
---
# <a name="ndisstatuswwanipaddressstate"></a>NDIS\_STATUS\_WWAN\_IP\_ADDRESS\_STATE


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_IP\_アドレス\_MB サービスに追加の PDP コンテキストの IP 構成の変更に関する通知の状態通知します。

この通知を使用して、 [ **NDIS\_WWAN\_IP\_アドレス\_状態**](https://msdn.microsoft.com/library/windows/hardware/dn449746)構造体。

<a name="remarks"></a>注釈
-------

この通知は、追加の PDP コンテキストのセッションに関連付けられた NDIS ポートで送信する必要があります。

ミニポート ドライバーは、追加の PDP コンテキストが正常にアクティブ化し、そのコンテキストの IP 構成が取得された後、この通知を送信する必要があります。 デバイスには、要請していない IP 構成の変更後のコンテキストのアクティベーションが示されている場合ミニポート ドライバー更新された IP 構成でこの通知が不要なを示す値を送信する必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 と Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_IP\_ADDRESS\_STATE**](https://msdn.microsoft.com/library/windows/hardware/dn449746)

 

 




