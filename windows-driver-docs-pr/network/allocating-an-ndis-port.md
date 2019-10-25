---
title: NDIS ポートの割り当て
description: NDIS ポートの割り当て
ms.assetid: 39c77921-5841-40f5-90ba-0fba89b3b55e
keywords:
- ポート WDK NDIS、割り当て
- NDIS ポート WDK、割り当て
- NDIS ポートを割り当てています
- ポート WDK NDIS、最大数
- NDIS ポート WDK、最大数
- WDK NDIS の最大ポート数
- ポートの状態 WDK NDIS
- 割り当て済みポートの状態 WDK NDIS
- ポート番号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884f3cf5b7657e681e0c64be36f57e3be57dc824
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835326"
---
# <a name="allocating-an-ndis-port"></a>NDIS ポートの割り当て





ミニポートアダプターに NDIS ポートを割り当てるために、ミニポートドライバーは[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)関数を呼び出します。 **NdisMAllocatePort**は同期的であり、NDIS によってポートに必要なリソースが正常に割り当てられた後に返されます。

ミニポートドライバーが**NdisMAllocatePort**を呼び出す前に、ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出して、 [**NDIS\_ミニポート\_アダプター\_登録\_属性の属性を設定する必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ミニポートドライバーは、 **NdisMSetMiniportAttributes**への呼び出しが正常に返された後、NDIS がそのミニポートアダプターの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出す前に、ミニポートアダプターに対して**NdisMAllocatePort**を呼び出すことができます。

ミニポートドライバーが既定のポートを割り当てないように、NDIS は常に既定のポート (ポートゼロ) を割り当てます。 ミニポートドライバーがフォーム[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)を返すと、NDIS によって既定のポートが解放されます。

ミニポートドライバーが[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)を呼び出すと、NDIS によってポートにポート番号が割り当てられます。 ドライバーは、 **NdisMAllocatePort**を呼び出す前に、 [**NDIS\_ポート\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)の構造のポート特性を指定します。 **NdisMAllocatePort**が正常に返されると、NDIS\_port の\_ポート番号のメンバーは、 *portcharacteristics*パラメーターに指定されているポート**番号を、** ndis によってポートに割り当てられたポート番号に設定します。

ミニポートドライバーは、ミニポートアダプターに関連付けられているすべてのポートを解放するために、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)から戻る前に[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)関数を呼び出す必要があります。 ミニポートアダプターの初期化に失敗した場合、ドライバーは**NdisMFreePort**を呼び出して、ドライバーが割り当てたすべてのポートを解放してから、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から制御が返されるようにする必要があります。 NDIS ポートの解放の詳細については、「 [Ndis ポートの解放](freeing-an-ndis-port.md)」を参照してください。

ミニポートドライバーが割り当てることができるポートの最大数は0xffffff です。 ただし実際には、ドライバーは、ドライバーアプリケーションのポートの種類と要件に基づいて、最大数を設定します。 たとえば、ブリッジアプリケーションの場合、ポートの数が16を超えることはほとんどありません。 802.1 x サプリサプリ ports を使用するアクセスポイントのポート数は、仮想プライベートネットワーク (VPN) ポートを使用する WAN ドライバーでは大きくなります。

ミニポートドライバーによってポートが割り当てられると、ポートは割り当て済みの状態になり、ポートはアクティブになりません。 ポートがアクティブ化されるまで、ポートを使用してデータを送受信したり、状態の表示を開始したり、OID 要求を発行したり、プラグアンドプレイ (PnP) イベントを開始したりすることはできません。 Ndis では、ミニポートドライバーによって、 [**ndis\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造の登録属性が設定された後に、既定のポートが自動的にアクティブ化されます。 Ndis に既定のポートをアクティブ**にしない**ように要求するために、ミニポートドライバーは NDIS\_ミニポート\_の\_属性\_\_コントロールに設定できます。\_の登録\_属性。

NDIS は、既定のポートの認証状態を、 [**ndis\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体の**Defaultportauthstates**メンバーにある[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡します。 ミニポートドライバーによって既定のポートが制御される場合、ミニポートドライバーによって既定のポートがアクティブになると、既定の認証設定を使用して既定のポートをアクティブにすることができます。 既定のポートのアクティブ化の詳細については、「 [NDIS ポートのアクティブ化](activating-an-ndis-port.md)」を参照してください。

ミニポートドライバーでは、NDIS の\_ポート\_CHAR\_使用できます。このフラグは、 [**ndis\_port**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)の**Flags**メンバーで、既定\_認証\_設定フラグを\_使用して、ドライバーが割り当てられ、アクティブ化されます。 割り当ての場合、NDIS は既定の認証状態を新しいポートに割り当て、 [**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)関数に渡される認証状態を無視します。

NDIS ポートの状態の詳細については、「 [Ndis ポートの状態](ndis-port-states.md)」を参照してください。 ポートのアクティブ化の詳細については、「 [NDIS ポートのアクティブ化](activating-an-ndis-port.md)」を参照してください。

 

 





