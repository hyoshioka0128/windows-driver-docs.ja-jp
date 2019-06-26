---
title: イベント通知の提供
description: イベント通知の提供
ms.assetid: 53ca7ef0-fa8b-4ae1-9b5e-b145c2d02db2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b41138b5fc9b5f4fa3fd202bdd6837e44b0e7c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374294"
---
# <a name="providing-event-notification"></a>イベント通知の提供





WIA サービスが呼び出すことによってサポートされているデバイス イベントの WIA ミニドライバーを通知、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッド。 このメソッドで、ミニドライバーは、イベントに応答するために必要なデバイス固有の機能を実装します。 WIA サービスの呼び出し、 **IWiaMiniDrv::drvNotifyPnpEvent**のみ、ミニドライバーは、デバイスでサポートを示されたイベントのメソッド、 [ **IWiaMiniDrv::drvGetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッド。

STI イベント メカニズムを使用するかを使用して、ミニドライバーが、イベントを開始[ **wiasQueueEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)イベント通知をこのデバイスからイベント キューに追加します。

### <a name="asynchronous-behavior-power-management-and-io-cancellation"></a>非同期の動作:電源管理と I/O キャンセル

ほとんどの場合では、WIA サービスは、一度に 1 つだけの呼び出しをドライバーが行われたことを確認します。 ただし、一部のメソッドは本質的に非同期と本質的に再入可能です。 これの良い例は、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッド。

WIA サービスでは、このメソッドを使用して、早急な対応が必要とするイベントのドライバーに通知します。 たとえば、WIA サービス、デバイスが削除されたことを示すプラグ アンド プレイ イベントを受け取るときに通知ドライバーすぐにします。 その他の例には、電源管理イベントとアプリケーションからの I/O キャンセル要求が含まれます。

実装例については、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)さまざまな種類のイベントに応答する必要がある方法を示すメソッドを参照してください[中断イベント サポートの追加](adding-interrupt-event-support.md).

 

 




