---
title: IWiaMiniDrvCallBack COM インターフェイス
description: IWiaMiniDrvCallBack COM インターフェイス
ms.assetid: a535d718-e34f-4cd0-9137-83d28d0b8e9c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 047e3afae8893e25663fbe101e1683acc82effb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378875"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM インターフェイス





[IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)ミニドライバーとアプリケーションの間の通信のチェーン内の 1 つのリンクを提供します。 2 つの間の通信を仲介経由、逆、ミニドライバーは、アプリケーションと直接通信できないため、: WIA サービス。 この通信は、アプリケーションによって実装できるようにする、 **IWiaDataCallback**インターフェイス (Microsoft Windows SDK のドキュメントで説明)。 このインターフェイスには、 **IWiaDataCallback::BandedDataCallback**メソッドで、WIA サービスを呼び出すことができます。 WIA サービスが別のコールバックを作成するアプリケーションでは、このコールバック ルーチンを提供する場合、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)ミニドライバーで使用するために提供するメソッド。

WIA サービスの呼び出すようにミニドライバーのイメージング デバイスから画像データを送信するか (たとえば、転送データの割合) のステータス メッセージを転送する準備ができたら**IWiaMiniDrvCallBack**::**MiniDrvCallback**します。 WIA サービス、データやに沿ってメッセージに渡しますアプリケーション、アプリケーションのコールバックを呼び出すとき。

 

 




