---
title: WIA ドライバーの項目ツリーの作成
description: WIA ドライバーの項目ツリーの作成
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127a4002016604ba29c997c2535e9c6231809713
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370072"
---
# <a name="creating-the-wia-driver-item-tree"></a>WIA ドライバーの項目ツリーの作成





ドライバーの項目のツリーを作成する必要があります、ミニドライバーが初期化された後、 [ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)によってメソッド。

1.  存在しない場合は、ドライバーの項目のツリーを作成します。 ミニドライバー ルート項目のフラグを設定し、ドライバー サービス ライブラリ関数を呼び出すことによって、ルート項目を作成します。 [ **wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)します。 ミニドライバーは、プライベート メンバー変数に返されたルート項目にポインターを格納します。

2.  使用して、デバイスで各アイテムのアイテムの子を作成、 [ **wiasCreateDrvItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatedrvitem)関数。 この関数が、ミニドライバーは、項目に関する情報を保存できるデバイスに固有のコンテキストを作成します。

3.  呼び出す、 [ **IWiaDrvItem::AddItemToFolder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)ドライバー項目のツリーにアイテムを追加するには、各子項目のメソッド。

 

 




