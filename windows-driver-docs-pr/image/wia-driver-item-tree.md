---
title: WIA ドライバーの項目ツリー
description: WIA ドライバーの項目ツリー
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d0438807f4f2a8fc7cbd5095fc89ce6edc95e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840706"
---
# <a name="wia-driver-item-tree"></a>WIA ドライバーの項目ツリー





WIA では、イメージングデバイスは、次のカメラツリーの図に示すように、WIA 項目の階層ツリーとして論理的に表されます。

![wia ドライバーの項目ツリーを示す図](images/art-2.png)

ルート項目は実際のデバイスを表し、子項目はイメージまたはフォルダーを表します。 フォルダーには、イメージや他のフォルダーを含めることができます。 アイテムには、ミニドライバーが設定またはクエリを実行できるプロパティがあります。

アプリケーションでは、WIA サービスを通じて、デバイス情報の取得と設定、デバイスの制御、ドライバー項目の列挙の開始などのタスクを実行するために、項目を使用します。

アプリケーションでは、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドを呼び出して、項目からのデータ転送を要求することによって、項目からデータを取得できます。

 

 




