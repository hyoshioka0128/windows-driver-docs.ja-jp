---
title: キャンセルされた要求のロジックを修正する
description: キャンセルされた要求のロジックを修正する
ms.assetid: 8246826A-BDBD-4A9B-9FFC-B813033E0FDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7013926ddcb1692e54d1ccd15cb1bd4ff7165ab3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842207"
---
# <a name="revise-canceled-request-logic"></a>キャンセルされた要求のロジックを修正する


I/o 要求が取り消された場合、WDM ドライバーはいくつかの複雑な競合状態を管理する必要があります。 要求は、キュー内にあるとき、またはドライバーが処理中のときにキャンセルされる可能性があります。 どちらの場合も、ドライバーはロックの組み合わせを使用して、要求が1回だけキャンセルされ、完了するようにする必要があります。

WDF キューメカニズムによって、キャンセルが大幅に簡素化されます。 要求がキューにある間にキャンセルされた場合、フレームワークはドライバーに通知せずにキャンセルを処理します。 ドライバーは、 [*EvtIoCanceledOnQueue*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)コールバック関数を登録することによって通知を要求できます。 フレームワークがドライバーに要求を配信した後、既定では、要求はキャンセルできません。 ドライバーは、いつでも[**Wdfrequestiscanceled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)を呼び出して、要求が取り消されたかどうかを確認できます。

詳細については、「 [I/o 要求のキャンセル](canceling-i-o-requests.md)」を参照してください。

 

 





