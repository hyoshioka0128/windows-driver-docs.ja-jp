---
title: 古いミニポート ドライバーの電源管理
description: 古いミニポート ドライバーの電源管理
ms.assetid: 676c8c4c-3fd7-4063-a704-2bbfdd03a94e
keywords:
- 電源管理 WDK NDIS ミニポート、古いミニポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d9c75e3f6e7b337ab656f783ce89091b23ec04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843500"
---
# <a name="power-management-for-old-miniport-drivers"></a>古いミニポート ドライバーの電源管理





次の場合、NDIS はミニポートドライバーを、電源管理に対応していない古いミニポートドライバーとして扱います。

-   初期化中、バスドライバーはシステムまたは NIC が電源管理に対応していないことを示します。

-   ミニポートドライバーは、 [OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)クエリに応答して、サポートされていない NDIS\_ステータス\_を返します。 この OID クエリを受信するのは、NDIS 5.1 以前のミニポートドライバーまたは中間ドライバーだけです。

-   ユーザーは、ユーザーインターフェイスで電源管理を無効にします。

NDIS でサポートされていない古いミニポートドライバーでは、電源が最も高い (D0) 状態と D3 状態の2つのデバイスの電源状態のみがサポートされます。

初期化中、古いミニポートドライバーは、システムがスリープ状態 (D3) に移行する前に、NDIS が停止しないように指定できます。 ミニポートドライバーでは、NDIS\_属性を設定することによって、ミニポートドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数に渡す*attributeflags*パラメーターの\_SUSPEND フラグに\_\_\_ないことを示します。 古いミニポートドライバーは、次のことが可能な場合にのみこのフラグを設定する必要があります。

-   必要になる可能性のあるすべてのハードウェアコンテキストを保存します。

-   NIC をスリープ状態 (D3) に適した状態にします。

-   NIC を最高電力状態 (D0) に再アクティブ化します。

NDIS が電源管理に対応していないことをバスドライバーから特定した場合、およびミニポートドライバーで NDIS\_属性が設定されていない場合は、\_SUSPEND フラグで\_\_停止\_は実行されません。管理機能。 ただし、ミニポートドライバーによって NDIS\_属性が設定されている場合\_\_SUSPEND フラグの\_\_停止しないと、NDIS はミニポートドライバーに[OID\_PNP\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)要求を発行します。 この場合、ミニポートドライバーは、NDIS\_状態\_成功を含む OID\_PNP\_機能要求を正常に完了する必要があります。 この要求に応答してミニポートドライバーから返される NDIS\_PM\_WAKE\_UP\_の機能の構造では、ミニポートドライバーでは、それぞれのデバイスの電源状態を**NdisDeviceStateUnspecified**に指定する必要があります。ウェイクアップ機能。

NDIS は、古いミニポートドライバーに対する次の電源管理サポートを提供します。

-   NDIS は、すべての[**IRP\_完了\_クエリ\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) 、システム電源マネージャーが NIC を表すデバイスオブジェクトに送信する電源要求を成功させることができます。 つまり、NDIS では、システムからの電源要求を\_する IRP\_\_に応答して、ミニポートドライバーの NIC が D3 状態に移行することを保証します。

-   ミニポートドライバーが NDIS の\_属性を設定しなかった場合\_初期化中に\_SUSPEND フラグの\_\_停止しません。そのため、NDIS はミニポートドライバーの NIC の前にミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。状態 D3 に遷移します。 ミニポートドライバーの NIC は、すべてのハードウェアコンテキスト情報を失います。

-   ミニポートドライバーで NDIS\_属性が設定されていても、初期化中に\_SUSPEND フラグの\_\_停止しない\_、システムが状態 D3 に移行する前に、NDIS はミニポートドライバーを停止しません。 代わりに、NDIS は、電源要求\_D3 状態に\_設定された[OID\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) 、ミニポートドライバーを発行します。 ミニポートドライバーは、使用しているハードウェアコンテキストをすべて保存し、D3 状態に適した状態に NIC を配置する必要があります。

-   システムが S0[システムの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)に移行している間、ndis はミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。 NDIS がミニポートドライバーを停止しなかった場合、NDIS は、\_電源要求を D0 状態に設定する OID\_、ミニポートドライバーを\_します。 ミニポートドライバーは、NIC を D0 状態に適した状態にする必要があります。

-   ミニポートドライバーが停止し、再初期化された場合、NDIS は OID 要求を発行して、パケットフィルターやマルチキャストアドレス一覧など、すべての適切なミニポートドライバー設定を復元します。 ミニポートドライバーが停止してから再初期化されなかった場合、ミニポートドライバーはこのような設定を復元する必要があります。

 

 





