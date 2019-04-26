---
title: NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_LTE_ATTACH_STATUS クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用します。
ms.assetid: 8A40437E-7AAC-4829-A032-0B8C933A7AC0
ms.date: 08/23/2018
keywords: -NDIS_STATUS_WWAN_LTE_ATTACH_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e3dcd88fa09cd7d99c5baf53f9bc5fa4366035b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346072"
---
# <a name="ndisstatuswwanlteattachstatus"></a>NDIS_STATUS_WWAN_LTE_ATTACH_STATUS

ミニポート ドライバーでは、NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知を使用して、モバイル ブロード バンド (MB) サービスに前回の完了に関する通知[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)クエリ要求。

要請されていないイベントは、たとえば SIM が挿入されると、コンテキストを LTE 接続がアクティブの場合に送信されます。 この場合、ミニポート ドライバーでは、ホスト OS にこの通知を送信する必要があります。

この状態の通知を使用して、 [ **NDIS_WWAN_LTE_ATTACH_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)構造体。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB LTE アタッチの操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
