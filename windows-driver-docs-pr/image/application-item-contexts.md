---
title: アプリケーション アイテムのコンテキスト
description: アプリケーション アイテムのコンテキスト
ms.assetid: d11b1750-999f-411c-9e83-6d2b20ce65db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfdd92b362f40573f2c4ced936a56dc21cb5fa5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552903"
---
# <a name="application-item-contexts"></a>アプリケーション アイテムのコンテキスト





アプリケーションのアイテムとも呼ばれますのコンテキストを*WIA サービス コンテキスト*、WIA サービスがいくつかのいずれかの呼び出しでミニドライバーに渡すルートまたは子アイテムへの参照は、 [IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)メソッド。 WIA サービス ライブラリの機能を呼び出すときに、ミニドライバーは、この参照を使用します。 項目のアプリケーション項目のコンテキストでは、メソッドで処理されるはどれを示します。 ミニドライバーは、アプリケーションのコンテキスト アイテムに直接アクセスしないでください。 ミニドライバーは、ドライバー サービス ライブラリ関数を呼び出すことでは、ルート項目または子項目に、項目かどうかを判断できます[ **wiasGetItemType**](https://msdn.microsoft.com/library/windows/hardware/ff549255)します。

アプリケーションは、作成、WIA 項目にデバイスからのデータ転送を要求、転送を開始するには、WIA サービス上で呼び出します。 WIA サービスのアプリケーション項目のコンテキストからミニドライバーのエントリ ポイントへのなど渡します、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)メソッド。 その後、使用する場合、ミニドライバー、WIA サービス ライブラリ関数など[ **wiasReadPropLong**](https://msdn.microsoft.com/library/windows/hardware/ff549330)アプリケーションのコンテキスト アイテムのパス、WIA サービス読み取りから指定したプロパティと、プロパティは、そのアプリケーションのアイテムに関連付けられた記憶域

 

 




