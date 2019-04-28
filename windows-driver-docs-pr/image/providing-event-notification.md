---
title: イベント通知の提供
description: イベント通知の提供
ms.assetid: 53ca7ef0-fa8b-4ae1-9b5e-b145c2d02db2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9651d28f798138c8ba78f67e18c0ed11f33732ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379628"
---
# <a name="providing-event-notification"></a>イベント通知の提供





WIA サービスが呼び出すことによってサポートされているデバイス イベントの WIA ミニドライバーを通知、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)メソッド。 このメソッドで、ミニドライバーは、イベントに応答するために必要なデバイス固有の機能を実装します。 WIA サービスの呼び出し、 **IWiaMiniDrv::drvNotifyPnpEvent**のみ、ミニドライバーは、デバイスでサポートを示されたイベントのメソッド、 [ **IWiaMiniDrv::drvGetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

STI イベント メカニズムを使用するかを使用して、ミニドライバーが、イベントを開始[ **wiasQueueEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549296)イベント通知をこのデバイスからイベント キューに追加します。

### <a name="asynchronous-behavior-power-management-and-io-cancellation"></a>非同期の動作:電源管理と I/O キャンセル

ほとんどの場合では、WIA サービスは、一度に 1 つだけの呼び出しをドライバーが行われたことを確認します。 ただし、一部のメソッドは本質的に非同期と本質的に再入可能です。 これの良い例は、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)メソッド。

WIA サービスでは、このメソッドを使用して、早急な対応が必要とするイベントのドライバーに通知します。 たとえば、WIA サービス、デバイスが削除されたことを示すプラグ アンド プレイ イベントを受け取るときに通知ドライバーすぐにします。 その他の例には、電源管理イベントとアプリケーションからの I/O キャンセル要求が含まれます。

実装例については、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)さまざまな種類のイベントに応答する必要がある方法を示すメソッドを参照してください[中断イベント サポートの追加](adding-interrupt-event-support.md).

 

 




