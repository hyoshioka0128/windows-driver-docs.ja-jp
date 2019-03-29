---
title: COM インターフェイスの提供
description: COM インターフェイスの提供
ms.assetid: c3e1578e-26f1-4fe3-b56d-a2baacb8e4c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49e4b4615b26e424bda25c196a5b424d3bea75d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578399"
---
# <a name="providing-a-com-interface"></a>COM インターフェイスの提供





WIA ミニドライバーをサポートする必要があります、 **IWiaMiniDrv**、 **IStiUSD**、および**IUnknown**インターフェイスが認識され、WIA サービスによって読み込まれます。 WIA ドライバーに次のインターフェイス id を追加する必要があります**QueryInterface**メソッド。

-   **IID\_IWiaMiniDrv** -のインターフェイスの識別子、 [IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)、標準的な WIA インターフェイス WIA 固有の機能にアクセスするために使用します。

-   **IID\_IStiUSD** -のインターフェイスの識別子、 [IStiUSD インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543827)、標準的な STI インターフェイス WIA ドライバーの STI 機能にアクセスするために使用

-   **IID\_IUnknown** -のインターフェイスの識別子、 **IUnknown** Microsoft Windows SDK ドキュメントで定義されている標準の COM インターフェイスのインターフェイスします。

呼び出すようにミニドライバーの WIA サービスへの応答でこれらのインターフェイス id をエクスポート、ミニドライバー **QueryInterface**メソッド。

これらのインターフェイスを実装する方法の例については、次を参照してください、 *wiascanr*スキャナー サンプル ミニドライバー ファイル*wiascanr.h*、 *iwiaminidrv.cpp*と *。istiusd.cpp または s*ee、 *wiacam*カメラ サンプル ミニドライバー ファイル*IWiaMiniDrv.cpp*と*IStiUSD.cpp*します。

 

 




