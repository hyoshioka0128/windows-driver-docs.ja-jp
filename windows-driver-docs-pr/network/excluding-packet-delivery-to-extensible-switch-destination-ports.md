---
title: 拡張可能スイッチ宛先ポートへのパケット配信の除外
description: 拡張可能スイッチ宛先ポートへのパケット配信の除外
ms.assetid: 04BF02A6-360F-482E-A86B-31232AFCB778
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5094495651665b2d78bab0a63c39d6092a0ffb89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834743"
---
# <a name="excluding-packet-delivery-to-extensible-switch-destination-ports"></a>拡張可能スイッチ宛先ポートへのパケット配信の除外


このトピックでは、Hyper-v 拡張可能スイッチ拡張機能を使用して、拡張可能なスイッチポートへのパケットの配信を除外する方法について説明します。 パケットの宛先ポートは、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造内の帯域外 (OOB) 転送コンテキスト内で指定されます。 このコンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

**メモ** このページでは、 [hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。


**メモ** 拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは*拡張可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。 拡張機能の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)」を参照してください。

拡張機能のフィルター処理と転送では、拡張可能なスイッチの受信または送信データパスで取得したパケットの配信を除外できます。 パケット配信の除外は、次の方法で行うことができます。

-   この拡張機能は、パケットの要求または指示を完了することによってパケットを削除できます。 これにより、拡張可能なスイッチポートへのパケットの配信が除外されます。 このメソッドは、1つまたは複数の宛先ポートを持つパケットで使用できます。

    拡張可能スイッチの受信データパスで取得されたパケットの場合、拡張機能は[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)を呼び出してパケット送信要求を完了します。

    拡張可能なスイッチの送信データパスで取得されたパケットの場合、拡張機能は[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)を呼び出すことによってパケット受信の表示を完了します。

-   複数の宛先ポートを持つ送信データパスで取得されたパケットの場合、拡張機能は1つまたは複数の宛先ポートのデータを変更することによって、パケット配信を除外できます。 この拡張機能では、宛先ポートの[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体の**IsExcluded**メンバーを1の値に設定することによってこれを行います。 このメソッドは、 **IsExcluded**値がゼロに設定されているポートにパケットを配信できるようにします。

    **メモ** 受信データパスで取得したパケットに宛先ポートが含まれていません。 このデータは、拡張可能なスイッチによって送信データパスにパケットが転送された後にのみ使用できます。

拡張機能によって宛先ポートの**IsExcluded**値が変更された後、送信データパスのパケットを後続の拡張機能に転送する必要があります。 ただし、すべてのパケットの宛先ポートの**IsExcluded**データが1に設定されている場合、拡張機能はパケットを転送するのではなく、パケットの受信通知を完了してパケットを破棄する必要があります。

**メモ** 拡張機能によって宛先ポートの**IsExcluded**値が1に設定された後、送信データパスの追加の拡張でこの値を0に変更することはできません。

**メモ** 拡張機能のキャプチャでは、拡張可能なスイッチポートへのパケットの配信を除外することはできません。

拡張可能なスイッチポートへのパケット配信を除外するには、次のガイドラインに従う必要があります。

-   拡張可能スイッチの受信データパスでは、フィルターおよび転送拡張機能は、パケットの送信元ポートまたはデータのポリシー条件に基づいてパケット配信を除外できます。

    送信元ポートの情報は、パケットの Net\_buffer\_[**list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の OOB データ内の[ **\_詳細\_net\_buffer\_list\_INFO\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)されるように、NDIS\_スイッチに格納されます。データ. 拡張機能は、NET\_BUFFER\_LIST を使用してデータを取得し[ **\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロを使用します。

    受信データパスから取得したパケットの配信が拡張機能によって除外される場合、パケット送信要求を完了することによってパケットを削除する必要があります。

-   拡張可能スイッチの受信データパスでは、転送拡張機能によってパケットの宛先ポートが決定され、この情報がパケットの OOB データに追加されます。 拡張機能によって適用されるポリシー条件に基づいて、宛先ポート情報を OOB データに追加しないことで、ポートへのパケット配信を除外できます。

    この手順の詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

-   拡張可能なスイッチの送信データパスでは、フィルターおよび転送拡張機能によって、ポリシーの条件に基づいてパケットの配信が除外される場合があります。 たとえば、フィルター拡張機能は、パケットの発信元ポートまたは宛先ポートのポリシー条件に基づいて、パケット配信を除外できます。

    拡張機能は、次の手順に従って、パケットの宛先ポートへの配信を除外します。

    1.  拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)を呼び出してパケットの宛先ポートを取得します。 呼び出しによって、NDIS\_STATUS\_SUCCESS が返された場合、DESTINATION*パラメーターには、* [**送信先\_配列構造\_転送\_、ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)へのポインターが含まれます。 この構造体は、パケットの拡張可能なスイッチの宛先ポートを指定します。 各宛先ポートは、 [**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造としてフォーマットされます。

        **メモ** [**NDIS\_スイッチの NUMDESTINATIONS メンバー\_転送\_転送先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造に0の値が含まれている場合、パケットには宛先ポートのデータがありません。

2.  この拡張機能では、宛先ポートの**IsExcluded**メンバーに[**ポート\_の NDIS\_スイッチ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)を設定することにより、拡張可能なスイッチポートへのパケット配信が除外されます。

    **メモ** 拡張機能がすべての宛先ポートへのパケットの配信を除外する場合、拡張機能はパケットの受信通知を完了してパケットを削除する必要があります。

3.  拡張機能がパケット内の1つまたはすべての宛先ポートへの配信を除外する場合は、次の操作を行う必要があります。

    -   拡張機能は[*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)にこれらの変更をコミットする必要があります。

    -   拡張機能は[*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)を呼び出す必要があります。 この関数が呼び出されると、拡張可能なスイッチインターフェイスによってカウンターが増加し、除外されるパケットのイベントがログに記録されます。 拡張機能は、パケットを取得した拡張可能なスイッチデータパス内のパケットを転送する前に、この呼び出しを行う必要があります。

    同様に、拡張機能がパケット送信要求を完了した場合、またはパケットのすべてのポートへの配信を除外するように指示した場合は、 [*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)も呼び出す必要があります。

    **メモ** 拡張機能では、拡張機能によって除外されているパケットの[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストを作成できます。 拡張機能が[*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)を呼び出すと、そのリンクリストへのポインターには、 *NetBufferLists*パラメーターが設定されます。

拡張可能なスイッチの受信と送信のデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。