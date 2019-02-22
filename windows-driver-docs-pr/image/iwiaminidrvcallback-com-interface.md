---
title: IWiaMiniDrvCallBack COM インターフェイス
description: IWiaMiniDrvCallBack COM インターフェイス
ms.assetid: a535d718-e34f-4cd0-9137-83d28d0b8e9c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30ac6cf3725190c975b8fbe2db49f26b08b6dacb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558146"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM インターフェイス





[IWiaMiniDrvCallBack インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543943)ミニドライバーとアプリケーションの間の通信のチェーン内の 1 つのリンクを提供します。 2 つの間の通信を仲介経由、逆、ミニドライバーは、アプリケーションと直接通信できないため、: WIA サービス。 この通信は、アプリケーションによって実装できるようにする、 **IWiaDataCallback**インターフェイス (Microsoft Windows SDK のドキュメントで説明)。 このインターフェイスには、 **IWiaDataCallback::BandedDataCallback**メソッドで、WIA サービスを呼び出すことができます。 WIA サービスが別のコールバックを作成するアプリケーションでは、このコールバック ルーチンを提供する場合、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)ミニドライバーで使用するために提供するメソッド。

WIA サービスの呼び出すようにミニドライバーのイメージング デバイスから画像データを送信するか (たとえば、転送データの割合) のステータス メッセージを転送する準備ができたら**IWiaMiniDrvCallBack**::**MiniDrvCallback**します。 WIA サービス、データやに沿ってメッセージに渡しますアプリケーション、アプリケーションのコールバックを呼び出すとき。

 

 




