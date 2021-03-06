---
title: アプリケーション項目とドライバー項目
description: アプリケーション項目とドライバー項目
ms.assetid: 33b602dc-4a0b-47e1-90e2-b77ecc05f66d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17f2e83816dd4d51f1ad7cc6b3073942a8ef6e81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372605"
---
# <a name="application-items-and-driver-items"></a>アプリケーション項目とドライバー項目





WIA 項目は、デバイスの属性とデバイスのデータを表します。 イメージング アプリケーションには、デバイス自体を表すルート項目とイメージまたはイメージを含むフォルダーを表すすべての子項目で、項目の階層ツリーとして WIA デバイスが参照してください。 ただし、アプリケーションが表示されるツリーが作成され、WIA ミニドライバーによって維持されるツリーから別は。 ミニドライバーは、項目のツリーを作成するとき、WIA サービスは自動的にこのイメージング アプリケーションで表示できるツリーの完全なコピーを作成します。 コピーしたツリー内の項目が呼び出される*アプリケーション項目*します。 ミニドライバーで作成されたツリー内の項目が呼び出される*ドライバー項目*します。

1 つ以上のイメージング アプリケーションでは、同時に 1 つのイメージング デバイスを使用できます。 デバイス ツリー内の項目オブジェクトの各アプリケーションのビューは、別のアプリケーションのビューに依存しないため場合があります。 これは、次のように実現されます。

1.  ミニドライバーのツリー項目を作成する[IWiaDrvItem インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)オブジェクトを使用して、 [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)と[WIA ドライバー サービス ライブラリ関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index)します。 このドライバーの項目のツリー内の項目は、デバイスの項目を表す、ミニドライバーを使用するグローバル オブジェクトです。

2.  イメージング アプリケーション要求へのアクセスをツリー内の項目、WIA サービスは、ドライバーの項目のコピーである項目オブジェクトを返します。 アプリケーションがアプリケーションを獲得する場合**IWiaItem** (Microsoft Windows SDK のドキュメントで説明) 項目オブジェクト (アプリケーションの項目)、ミニドライバーにこのオブジェクトの対応する WIA サービスへのリンク**IWiaDrvItem**オブジェクト、*ドライバー項目ツリー*します。

3.  WIA 作成個別*アプリケーション項目のツリー*アプリケーション項目ツリーの各アイテム ツリーの ドライバーのコピーである、アプリケーションごとにします。

アプリケーションを使用して、通常、 **IWiaItem**を読み取り、検証、および項目のプロパティを書き込み、および項目データを要求するオブジェクト。

次の図は、ドライバーの項目にアプリケーション アイテムのリレーションシップを示します。

![アプリケーションのアイテムとドライバーのアイテム間の関係を示す図](images/art-5.png)

各イメージング アプリケーションの図に示した項目ツリーの独立したコピーがあります。 アプリケーションのアイテム ツリーのルート項目には、バックアップ デバイス項目ツリーのルート項目へのポインターが含まれています。

このセクションの残りの部分には、次のトピックが含まれています。

[アイテムのプロパティについて](about-item-properties.md)

[WIA ドライバー項目ツリー](wia-driver-item-tree.md)

[WIA カメラ ツリー](wia-camera-tree.md)

[WIA スキャナー ツリー](wia-scanner-tree.md)

[一般的なカメラ、およびスキャナーのプロパティ](common--camera--and-scanner-properties.md)

 

 




