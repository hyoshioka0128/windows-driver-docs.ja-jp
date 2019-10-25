---
title: NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 通知を使用して、ネットワーク更新の結果として、プロビジョニングされたコンテキストの一覧の更新について MB サービスに通知します。
ms.assetid: 3ec3d991-98c0-4be3-a157-a04e8565a54b
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 574e248b92c76aaa41d49953d2870c8834e5b6da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844693"
---
# <a name="ndis_status_wwan_provisioned_contexts"></a>NDIS\_ステータス\_WWAN\_プロビジョニングされた\_コンテキスト


ミニポートドライバーは、NDIS\_ステータス\_WWAN\_プロビジョニングされた\_コンテキスト通知を使用して、ネットワーク更新の結果として、プロビジョニングされたコンテキストの一覧の更新について MB サービスに通知します。

ミニポートドライバーは、この通知を使用して、要請されていないイベントも送信できます。

この通知では、 [**NDIS\_WWAN\_プロビジョニング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)された\_コンテキスト構造を使用します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーでは、\_CONTEXT 構造体の**ContextListHeader**を**WwanStructContext**にプロビジョニングするために、NDIS\_\_WWAN の**ElementType**メンバーを設定する必要があります。

場合によっては、プロビジョニングされたコンテキストの一覧が、無線 (OTA) またはショートメッセージサービス (SMS) のいずれかでネットワークによって更新されます。 ミニポートドライバーは、それに応じて、プロビジョニングされたコンテキストの一覧を更新する必要があります。 その後、ミニポートドライバーは、更新された一覧を使用して、更新プログラムに関する情報を MB サービスに通知する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_プロビジョニングされた\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)

[OID\_WWAN\_プロビジョニングされた\_コンテキスト](oid-wwan-provisioned-contexts.md)

 

 




