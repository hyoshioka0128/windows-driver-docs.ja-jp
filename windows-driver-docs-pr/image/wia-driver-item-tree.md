---
title: WIA ドライバーの項目ツリー
description: WIA ドライバーの項目ツリー
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 241e5b28472b23cddcfef2b1fe1669b4bb439d61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366881"
---
# <a name="wia-driver-item-tree"></a>WIA ドライバーの項目ツリー





WIA で、イメージング デバイスとして表されます論理的に WIA の項目の階層ツリー カメラ ツリーの次の図に示すようにします。

![wia ドライバーの項目のツリーを示す図](images/art-2.png)

ルート項目は、実際のデバイスを表し、子項目は、イメージまたはフォルダーを表します。 フォルダーは、イメージやその他のフォルダーに含めることができます。 項目では、ミニドライバーは、設定またはクエリを実行できるプロパティがあります。

WIA サービスを通過、アプリケーションは、取得、デバイス情報を設定して、デバイスを制御する、およびドライバー項目の列挙を開始などのタスクを実行するのに項目を使用します。

アプリケーションが呼び出すことができます、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)項目からのデータ転送を要求することによって、アイテムからのデータを取得します。

 

 




