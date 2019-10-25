---
title: VMQ 割り込み要件
description: VMQ 割り込み要件
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d7e461b18cc53dbc7637815bd52b24b0f8cb8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842945"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 割り込み要件


バーチャルマシンキュー (VMQ) 機能をサポートするミニポートドライバーでは、次の割り込み割り当て要件もサポートする必要があります。

-   ミニポートドライバーは、MSI-X をサポートする必要があります。 このドライバーでは、ndis **\_receive\_filter\_MSI\_X\_** supported フラグを設定する必要があります。このフラグは、Ndis の**supportedqueueproperties**メンバーで\_[**受信\_フィルター\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)によって取得されます。データ.

    このドライバーは、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数の呼び出しでドライバーが使用する[ **\_属性の構造\_\_、NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)のこの構造体を返します。

-   ミニポートドライバーは、割り込みベクターを割り当てるためのプロセッサ情報を取得するために、 [**NdisGetRssProcessorInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation)関数を呼び出す必要があります。 割り込み割り当てのために、レジストリキーや他のソースから取得した情報に依存しないようにする必要があります。

    [**NdisGetRssProcessorInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation)は、ミニポートドライバーが RSS および VMQ に使用できるプロセッサのセットに関する情報を返します。 この情報は、 [**NDIS\_RSS\_PROCESSOR\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)構造体に含まれています。

-   ミニポートドライバーは、 [**NDIS\_RSS\_processor\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)構造体で指定されている各プロセッサに対して、割り込みベクターを1つだけ割り当てる必要があります。

    ミニポートドライバーは、送信または受信パケット操作に関連付けられていない他のイベントに対して、2つ以上の割り込みベクターを割り当てる必要があります。 たとえば、ドライバーはリンクステータスイベントの IDT を割り当てることができます。

-   ミニポートドライバーは、次の表に定義されている、最小数の MSI-X 割り込みベクターをサポートする必要があります。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">キューの数</th>
    <th align="left">必要な MSI-X 割り込みベクターの最小数</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>1 ~ 16</p></td>
    <td align="left"><p>1 ~ 16</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>17 ~ 64</p></td>
    <td align="left"><p>16 ~ 32</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>65以上</p></td>
    <td align="left"><p>32以上</p></td>
    </tr>
    </tbody>
    </table>

     

 

 





