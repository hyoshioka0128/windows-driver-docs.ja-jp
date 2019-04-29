---
title: WIA ドライバーの項目ツリーの作成
description: WIA ドライバーの項目ツリーの作成
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4077776f9abfd7925172feca885ae5e6a35a2bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386308"
---
# <a name="creating-the-wia-driver-item-tree"></a>WIA ドライバーの項目ツリーの作成





ドライバーの項目のツリーを作成する必要があります、ミニドライバーが初期化された後、 [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)によってメソッド。

1.  存在しない場合は、ドライバーの項目のツリーを作成します。 ミニドライバー ルート項目のフラグを設定し、ドライバー サービス ライブラリ関数を呼び出すことによって、ルート項目を作成します。 [ **wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)します。 ミニドライバーは、プライベート メンバー変数に返されたルート項目にポインターを格納します。

2.  使用して、デバイスで各アイテムのアイテムの子を作成、 [ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)関数。 この関数が、ミニドライバーは、項目に関する情報を保存できるデバイスに固有のコンテキストを作成します。

3.  呼び出す、 [ **IWiaDrvItem::AddItemToFolder** ](https://msdn.microsoft.com/library/windows/hardware/ff543856)ドライバー項目のツリーにアイテムを追加するには、各子項目のメソッド。

 

 




