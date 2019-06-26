---
title: アプリケーション項目のコンテキスト
description: アプリケーション項目のコンテキスト
ms.assetid: d11b1750-999f-411c-9e83-6d2b20ce65db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b978c24f9a58fb070bd494a8df861db60070f7a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366758"
---
# <a name="application-item-contexts"></a>アプリケーション項目のコンテキスト





アプリケーションのアイテムとも呼ばれますのコンテキストを*WIA サービス コンテキスト*、WIA サービスがいくつかのいずれかの呼び出しでミニドライバーに渡すルートまたは子アイテムへの参照は、 [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)メソッド。 WIA サービス ライブラリの機能を呼び出すときに、ミニドライバーは、この参照を使用します。 項目のアプリケーション項目のコンテキストでは、メソッドで処理されるはどれを示します。 ミニドライバーは、アプリケーションのコンテキスト アイテムに直接アクセスしないでください。 ミニドライバーは、ドライバー サービス ライブラリ関数を呼び出すことでは、ルート項目または子項目に、項目かどうかを判断できます[ **wiasGetItemType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype)します。

アプリケーションは、作成、WIA 項目にデバイスからのデータ転送を要求、転送を開始するには、WIA サービス上で呼び出します。 WIA サービスのアプリケーション項目のコンテキストからミニドライバーのエントリ ポイントへのなど渡します、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッド。 その後、使用する場合、ミニドライバー、WIA サービス ライブラリ関数など[ **wiasReadPropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong)アプリケーションのコンテキスト アイテムのパス、WIA サービス読み取りから指定したプロパティと、プロパティは、そのアプリケーションのアイテムに関連付けられた記憶域

 

 




