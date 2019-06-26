---
title: WIA ミニドライバーを受け取る方法は、WIA から切断します。
description: WIA ミニドライバーが WIA サービスから接続解除イベントを受信する方法
ms.assetid: 6ae3c230-d026-469e-a699-860a295fba85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417cf2089c4e0adf9edfd92162d10fd3ea1273d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363055"
---
# <a name="how-the-wia-minidriver-receives-a-disconnect-event-from-the-wia-service"></a>WIA ミニドライバーが WIA サービスから接続解除イベントを受信する方法

デバイスが、コンピューターから、ユーザーが USB ケーブルを切断するときなど、コンピューターから突然切断されたときに、WIA サービスが呼び出す、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドをWIA\_イベント\_デバイス\_DISCONNECTED イベント。 参照してください[中断イベントのサポートを追加する](adding-interrupt-event-support.md)の実装例については、 **IWiaMiniDrv::drvNotifyPnpEvent**メソッド。

WIA ミニドライバーは、中、またはこのイベントの後に、ハードウェアと通信するためにしないようにします。 このイベントでは、WIA サービスが、ミニドライバーをアンロードすることを示します。 次のデバイス アクセスが許可されているとは、WIA サービス、ミニドライバーを再読み込みする場合です。 ミニドライバーが、すべてのフラグを設定することをお勧め[IWiaMiniDrv](iwiaminidrv-com-interface.md)再接続されるまで、ハードウェアへのアクセスからの呼び出しのインターフェイスします。

WIA\_イベント\_デバイス\_WIA ミニドライバーに DISCONNECTED イベントが常に送信されません。 コンピューターをシャット ダウンすると、WIA サービス WIA ドライバーをアンロードしています、このイベントは送信しません。 このイベントは、アクションを無効にすると、デバイスのハードウェアとして扱う必要があります。

 



