---
title: アプリケーション項目のコンテキスト
description: アプリケーション項目のコンテキスト
ms.assetid: d11b1750-999f-411c-9e83-6d2b20ce65db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4a066ef4fa0cc227283e7b8b1578fb217fa5174
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840898"
---
# <a name="application-item-contexts"></a>アプリケーション項目のコンテキスト





アプリケーション項目コンテキストは、 *wia サービスコンテキスト*とも呼ばれ、いくつかの[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)メソッドのいずれかの呼び出しで、wia サービスがミニドライバーに渡すルートまたは子項目への参照です。 次に、ミニドライバーは、特定の WIA サービスライブラリ関数を呼び出すときに、この参照を使用します。 項目のアプリケーション項目コンテキストは、メソッドで処理される項目を示します。 ミニドライバーは、アプリケーション項目コンテキストに直接アクセスしようとすることはできません。 ミニドライバーは、ドライバーサービスライブラリ関数[**wiasGetItemType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype)を呼び出すことによって、項目がルート項目であるか、子項目であるかを判断できます。

アプリケーションは、デバイスから作成された WIA 項目へのデータ転送を要求すると、その転送を開始するために、WIA サービスでを呼び出します。 WIA サービスは、アプリケーション項目のコンテキストを[**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドなどのミニドライバーエントリポイントに渡します。 その後、ミニドライバーが[**Wiasreadproplong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)ような WIA サービスライブラリ関数を使用し、アプリケーション項目コンテキストを渡すと、そのアプリケーションアイテムに関連付けられているプロパティストレージから、指定されたプロパティが wia サービスによって読み取られます。

 

 




