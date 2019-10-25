---
title: イベント通知の提供
description: イベント通知の提供
ms.assetid: 53ca7ef0-fa8b-4ae1-9b5e-b145c2d02db2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ad2daa463e3c59cfbbb4e3f38c27fbfdc205da3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840771"
---
# <a name="providing-event-notification"></a>イベント通知の提供





WIA サービスは、 [**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドを呼び出すことによって、サポートされているデバイスイベントを wia ミニドライバーに通知します。 このメソッドでは、ミニドライバーは、イベントに応答するために必要なデバイス固有の機能を実装します。 WIA サービスは、 [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドでデバイスがサポートできることをミニドライバーが指定したイベントに対してのみ、 **IWiaMiniDrv::d rvnotifypnpevent**メソッドを呼び出します。

ミニドライバーは、STI イベントメカニズムを使用するか、 [**Wiasqueueevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)を使用して、このデバイスからイベントキューにイベント通知を追加して、イベントを開始します。

### <a name="asynchronous-behavior-power-management-and-io-cancellation"></a>非同期動作: 電源管理と i/o キャンセル

ほとんどの場合、WIA サービスによって、一度に1つのドライバーに対して一度に実行される呼び出しは1つだけになります。 ただし、一部のメソッドは本質的に非同期で再入可能です。 この例の好例は、 [**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドです。

WIA サービスは、このメソッドを使用して、直ちに対処する必要があるイベントをドライバーに通知します。 たとえば、デバイスが削除されたことを示すプラグアンドプレイイベントを WIA サービスが受信すると、直ちにドライバーに通知します。 その他の例としては、アプリケーションからの電源管理イベントや i/o キャンセル要求などがあります。

さまざまな種類のイベントに応答する方法を示す[**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドの実装例については、「[割り込みイベントのサポートの追加](adding-interrupt-event-support.md)」を参照してください。

 

 




