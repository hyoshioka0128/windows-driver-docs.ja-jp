---
title: 省電力プロトコル オフロードの現在のパラメーター設定の取得
description: 省電力プロトコル オフロードの現在のパラメーター設定の取得
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc19bed34980a8f615743f13771ed28a5dfcb1a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837741"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>省電力プロトコル オフロードの現在のパラメーター設定の取得





プロトコルドライバーは、 [oid\_PM\_プロトコル\_オフロード\_リスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)oid クエリを使用して、ネットワークアダプター上のそのプロトコルによってオフロードされたすべてのプロトコルの一覧を取得できます。 クエリから正常に戻った後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造のリストへのポインターが含まれています。現在アクティブなプロトコルのオフロードを記述します。 **NDIS\_PM\_プロトコル\_オフロード**構造の内容については、「[低電力プロトコルオフロードの追加と削除](adding-and-deleting-low-power-protocol-offloads.md)」を参照してください。

NDIS では、 [oid\_pm\_プロトコル\_オフロード\_リスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID と GUID\_PM\_プロトコル\_オフロード\_、ミニポートドライバーに代わって WMI 要求を一覧表示します。 そのため、NDIS ミニポートドライバーは、OID\_PM\_プロトコル\_オフロード\_リスト OID 要求をサポートするためには必要ありません。

これまでのドライバーでは、 [oid\_PM\_使用して\_プロトコル\_オフロード](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-get-protocol-offload)方式の OID を取得し、ミニポートドライバーから低電力プロトコルオフロードのパラメーター設定を取得することができます。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初にプロトコルオフロード識別子へのポインターが含まれています。 メソッド要求から正常に戻った後、 **ndis\_OID\_要求**構造の**informationbuffer**メンバーには、 [**ndis\_PM\_プロトコル\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)構造へのポインターが含まれています。

 

 





