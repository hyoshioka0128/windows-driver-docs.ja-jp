---
title: アプリケーション項目とドライバー項目
description: アプリケーション項目とドライバー項目
ms.assetid: 33b602dc-4a0b-47e1-90e2-b77ecc05f66d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbe2f2839fd2a88d47ddb122eba30cf7881cb49d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840896"
---
# <a name="application-items-and-driver-items"></a>アプリケーション項目とドライバー項目





WIA 項目は、デバイス属性とデバイスデータを表します。 イメージングアプリケーションでは、WIA デバイスが項目の階層ツリーとして表示されます。これには、デバイス自体を表すルート項目と、イメージまたはイメージを含むフォルダーを表す子項目が含まれます。 ただし、アプリケーションに表示されるツリーは、WIA ミニドライバーによって作成および管理されるツリーとは別のものです。 ミニドライバーが項目のツリーを作成すると、WIA サービスによって、このツリーの同一のコピーが自動的に作成されます。このコピーは、イメージングアプリケーションで表示できます。 コピーされたツリー内の項目は、*アプリケーション項目*と呼ばれます。 ミニドライバーによって作成されたツリー内の項目は、*ドライバー項目*と呼ばれます。

複数のイメージングアプリケーションで、一度に1つのイメージングデバイスを使用できます。 したがって、デバイスツリー内の項目オブジェクトの各アプリケーションのビューは、別のアプリケーションのビューに依存しないようにする必要があります。 これは次のように行われます。

1.  ミニドライバーは、 [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)と[WIA ドライバーサービスライブラリ関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index)を使用して、 [IWiaDrvItem インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)オブジェクトの項目ツリーを作成します。 このドライバー項目ツリー内の項目は、ミニドライバーがデバイスの項目を表すために使用するグローバルオブジェクトです。

2.  イメージングアプリケーションがツリー内の項目へのアクセスを要求すると、WIA サービスはドライバー項目のコピーである項目オブジェクトを返します。 アプリケーションが**Iwiaitem** (Microsoft Windows SDK ドキュメントで説明) 項目オブジェクト (アプリケーション項目) を取得すると、このオブジェクトは、ミニドライバーの対応する**IWiaDrvItem**オブジェクトにリンクされます。*ドライバー項目ツリー*。

3.  WIA では、アプリケーションごとに個別の*アプリケーション項目ツリー*が作成されます。各アプリケーション項目ツリーは、ドライバー項目ツリーのコピーです。

通常、アプリケーションは、 **Iwiaitem**オブジェクトを使用して、項目のプロパティの読み取り、検証、および書き込みを行い、項目データを要求します。

次の図は、アプリケーション項目とドライバー項目の関係を示しています。

![アプリケーション項目とドライバー項目の関係を示す図](images/art-5.png)

図に示すように、各イメージングアプリケーションには項目ツリーの個別のコピーがあります。 アプリケーション項目ツリーのルート項目には、デバイス項目ツリーのルート項目へのポインターが含まれています。

このセクションの残りの部分では、次のトピックについて説明します。

[項目のプロパティについて](about-item-properties.md)

[WIA ドライバー項目ツリー](wia-driver-item-tree.md)

[WIA カメラツリー](wia-camera-tree.md)

[WIA スキャナーツリー](wia-scanner-tree.md)

[共通、カメラ、スキャナーのプロパティ](common--camera--and-scanner-properties.md)

 

 




