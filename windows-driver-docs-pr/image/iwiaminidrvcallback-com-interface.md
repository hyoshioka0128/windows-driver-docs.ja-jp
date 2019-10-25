---
title: IWiaMiniDrvCallBack COM インターフェイス
description: IWiaMiniDrvCallBack COM インターフェイス
ms.assetid: a535d718-e34f-4cd0-9137-83d28d0b8e9c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf662ac75dd21b8f33fa347cc87fbc8ba5abc1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840795"
---
# <a name="iwiaminidrvcallback-com-interface"></a>IWiaMiniDrvCallBack COM インターフェイス





[IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)は、ミニドライバーとアプリケーションの間の通信チェーンに1つのリンクを提供します。 ミニドライバーはアプリケーションと直接通信することはできず、その逆も可能であるため、2つの間の通信は、"中間" を経由する必要があります。つまり、WIA サービスです。 この通信を有効にするために、アプリケーションは**IWiaDataCallback**インターフェイス (Microsoft Windows SDK のドキュメントで説明) を実装します。 このインターフェイスには、 **IWiaDataCallback:: BandedDataCallback**メソッドが含まれています。このメソッドは、WIA サービスが呼び出すことができます。 アプリケーションがこのコールバックルーチンを提供する場合、WIA サービスは別のコールバック ( [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッド) を作成します。これは、ミニドライバーによって使用されます。

ミニドライバーがイメージデータをイメージングデバイスから送信したり、ステータスメッセージ (転送されたデータの割合など) を転送したりする準備ができたら、WIA サービスの**IWiaMiniDrvCallBack**::**MiniDrvCallback**を呼び出します。 次に、アプリケーションのコールバックを呼び出すときに、WIA サービスがアプリケーションにデータまたはメッセージを渡します。

 

 




