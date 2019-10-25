---
title: MSI 割り込みの処理
description: MSI 割り込みの処理
ms.assetid: c8e2a5a4-17f5-48a3-a2d0-6eca2a0b7f45
keywords:
- MSI-X WDK ネットワーク, 割り込みの処理
- メッセージシグナルによる WDK ネットワークの割り込み、割り込みの処理
- Msi WDK ネットワーク, 割り込みの処理
- WDK ネットワークの割り込み、処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72a8b3c29b99cf6887595bc7cc1176dc40345d88
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840477"
---
# <a name="handling-an-msi-interrupt"></a>MSI 割り込みの処理





NDIS は、ネットワークインターフェイスカード (NIC) が割り込みを生成するときに、 [*Miniportmessageinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)関数を呼び出します。 この関数の*MessageId*パラメーターは、MSI-X メッセージを識別します。

*Miniportmessageinterrupt*は、メッセージの割り込みが共有されていないため、割り込みを処理した後、常に**TRUE**を返す必要があります。

ミニポートドライバーは、 *Miniportmessageinterrupt*関数でできるだけ少ない作業を行う必要があります。 ドライバーは、 [*MiniportMessageInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc)関数に i/o 操作を遅延させる必要があります。この関数は、割り込みの遅延処理を完了するために NDIS を呼び出します。

[*Miniportmessageinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt)が返された後に追加の遅延プロシージャ呼び出し (dpc) をキューに追加するために、ミニポートドライバーは、 *Miniportmessageinterrupt*関数の*targetprocessors*パラメーターのビットを設定します。 *Miniportmessageinterrupt*または*MiniportMessageInterruptDPC*から追加の dpc を要求するために、ミニポートドライバーは[**NdisMQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueuedpc)関数を呼び出すことができます。

ミニポートドライバーは**NdisMQueueDpc**を呼び出して、他のプロセッサに対して追加の dpc を要求できます。

NDIS 6.1 以降のバージョンでは、同じ CPU に対してスケジュールされている異なるメッセージの Dpc が個別にキューに格納されることが保証されます。 たとえば、ミニポートドライバーで CPU 1 で同時に2つの Dpc がスケジュールされている場合 (メッセージ0の場合は 1 DPC、メッセージ1の場合はその他の dpc)、2つの Dpc が CPU 1 のためにキューに置かれます (1 つはメッセージ0、もう1つはメッセージ1を含む dpc)。

また、NDIS では、異なる Cpu でスケジュールされた同じメッセージの Dpc が個別にキューに入れられることも保証されます。 たとえば、ミニポートドライバーで2つの Dpc がスケジュールされている場合 (メッセージ0の場合は CPU 0、メッセージ0の場合は CPU 1 に1つの dpc)、2つの Dpc は、メッセージ0の CPU 0 と CPU 1 でキューに入れられます。

 

 





