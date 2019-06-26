---
title: WIA ドライバーの項目ツリー
description: WIA ドライバーの項目ツリー
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a69867888e0b379b81275db6223ce01598643d3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383774"
---
# <a name="wia-driver-item-tree"></a>WIA ドライバーの項目ツリー





WIA で、イメージング デバイスとして表されます論理的に WIA の項目の階層ツリー カメラ ツリーの次の図に示すようにします。

![wia ドライバーの項目のツリーを示す図](images/art-2.png)

ルート項目は、実際のデバイスを表し、子項目は、イメージまたはフォルダーを表します。 フォルダーは、イメージやその他のフォルダーに含めることができます。 項目では、ミニドライバーは、設定またはクエリを実行できるプロパティがあります。

WIA サービスを通過、アプリケーションは、取得、デバイス情報を設定して、デバイスを制御する、およびドライバー項目の列挙を開始などのタスクを実行するのに項目を使用します。

アプリケーションが呼び出すことができます、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)項目からのデータ転送を要求することによって、アイテムからのデータを取得します。

 

 




