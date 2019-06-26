---
title: NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS
description: ミニポート ドライバーでは、NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 通知を使用して、ネットワークの更新の結果としてプロビジョニングされたコンテキストの一覧に更新プログラムに関する MB サービスに通知します。
ms.assetid: 3ec3d991-98c0-4be3-a157-a04e8565a54b
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 44590017fcb49bb1b7d14f9937555c8e88c13f36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377589"
---
# <a name="ndisstatuswwanprovisionedcontexts"></a>NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト


ミニポート ドライバーを使用して、NDIS\_状態\_WWAN\_プロビジョニング済み\_MB サービスにネットワークの更新の結果としてプロビジョニングされたコンテキストの一覧に更新プログラムに関する通知のコンテキストの通知。

ミニポート ドライバーには、この通知が不要なイベントを送信できます。

この通知を使用して、 [ **NDIS\_WWAN\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)構造体。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーを設定する必要があります、 **ElementType**の NDIS メンバー\_WWAN\_プロビジョニング済み\_コンテキスト構造体の**ContextListHeader**に**WwanStructContext**します。

場合によっては、ネットワークでプロビジョニングされているコンテキストの一覧を更新、Over-The-Air (OTA) または、ショート メッセージ サービス (SMS)。 ミニポート ドライバーでは、それに応じてプロビジョニングのコンテキストの一覧を更新する必要があります。 その後、ミニポート ドライバーでは、MB サービスに更新された一覧でこのを示す値を使用して更新プログラムの詳細を通知する必要があります。

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
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)

[OID\_WWAN\_プロビジョニング済み\_コンテキスト](oid-wwan-provisioned-contexts.md)

 

 




