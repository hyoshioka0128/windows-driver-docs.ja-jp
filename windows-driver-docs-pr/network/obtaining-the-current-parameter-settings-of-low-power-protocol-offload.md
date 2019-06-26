---
title: 省電力プロトコル オフロードの現在のパラメーター設定の取得
description: 省電力プロトコル オフロードの現在のパラメーター設定の取得
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3189321632cfd7cb72d5cf6d01e5a507c07951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354511"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>省電力プロトコル オフロードの現在のパラメーター設定の取得





プロトコル ドライバーを使用して[OID\_PM\_プロトコル\_オフロード\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)ネットワーク アダプターでは、そのプロトコルがオフロードされているすべてのプロトコルの一覧を取得する OID クエリ。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造に含まれる、一覧へのポインター [ **NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)現在アクティブなプロトコルを記述する構造体の負荷を軽減します。 内容については、 **NDIS\_PM\_プロトコル\_オフロード**構造体は、「[の追加および削除する低電力プロトコルをオフロード](adding-and-deleting-low-power-protocol-offloads.md)します。

NDIS ハンドル[OID\_PM\_プロトコル\_オフロード\_一覧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID と GUID\_PM\_プロトコル\_オフロード\_一覧 WMIミニポート ドライバーの代わりに要求します。 そのため、NDIS ミニポート ドライバーは、OID をサポートする必要はありません\_PM\_プロトコル\_オフロード\_一覧 OID 要求。

後続のドライバーを使用できます、 [OID\_PM\_取得\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-get-protocol-offload)メソッド低電力プロトコル パラメーター設定を取得する OID のミニポート ドライバーから負荷を軽減します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体には最初にプロトコル オフロードへのポインターが含まれています識別子です。 メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 [**NDIS\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造体。

 

 





