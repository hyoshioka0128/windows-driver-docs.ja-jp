---
title: WIA ドライバーの項目ツリーの作成
description: WIA ドライバーの項目ツリーの作成
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a32a896f27bf3b45c142273eca5fd5d8f4ff9d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840865"
---
# <a name="creating-the-wia-driver-item-tree"></a>WIA ドライバーの項目ツリーの作成





ミニドライバーを初期化した後、次の方法で[**IWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドにドライバー項目ツリーを作成する必要があります。

1.  ドライバー項目ツリーがまだ存在しない場合は作成します。 ミニドライバーは、ルート項目フラグを設定し、ドライバーサービスライブラリ関数[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)を呼び出してルート項目を作成します。 ミニドライバーは、返されたポインターをプライベートメンバー変数のルート項目に格納します。

2.  [**WiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)関数を使用して、デバイス上の項目ごとに子項目を作成します。 この関数は、ミニドライバーが項目に関する情報を格納できるデバイス固有のコンテキストを作成します。

3.  各子項目に対して[**IWiaDrvItem:: AddItemToFolder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder)メソッドを呼び出して、項目をドライバー項目ツリーに追加します。

 

 




