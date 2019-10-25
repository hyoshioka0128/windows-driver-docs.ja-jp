---
title: COM インターフェイスの提供
description: COM インターフェイスの提供
ms.assetid: c3e1578e-26f1-4fe3-b56d-a2baacb8e4c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6be693a184e2c98db2850032aad49c6b8cf73336
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840769"
---
# <a name="providing-a-com-interface"></a>COM インターフェイスの提供





Wia ミニドライバーは、WIA サービスによって認識されて読み込まれるように、 **IWiaMiniDrv**、 **i usd**、 **IUnknown**の各インターフェイスをサポートする必要があります。 次のインターフェイス識別子は、WIA ドライバーの**QueryInterface**メソッドに追加する必要があります。

-   **IID\_IWiaMiniDrv** - [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)のインターフェイス識別子。 wia 固有の機能にアクセスするために使用される標準的な wia インターフェイスです。

-   **IID\_iで**は、 [i、usd インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)のインターフェイス識別子です。これは、WIA ドライバーの sti 機能へのアクセスに使用される標準の sti インターフェイスです。

-   **IID\_** iunknown-Microsoft Windows SDK ドキュメントで定義されている標準の COM インターフェイスである**iunknown**インターフェイスのインターフェイス識別子。

ミニドライバーは、ミニドライバーの**QueryInterface**メソッドを呼び出す WIA サービスへの応答として、これらのインターフェイス識別子をエクスポートします。

これらのインターフェイスの実装方法の例については、 *wiascanr*スキャナーのサンプルミニドライバーファイル*wiascanr. h*、 *iwiaminidrv* *、およびミニドライバー*を参照してください。 *wiacam*カメラサンプルファイル*IWiaMiniDrv*と*iは、.cpp*です。

 

 




