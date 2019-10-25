---
title: ドライバー ツリーからの項目の削除
description: ドライバー ツリーからの項目の削除
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 174d59206f65ce200393ea0e75fc457c9aa12b27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840859"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>ドライバー ツリーからの項目の削除





ドライバー項目を削除するために、WIA サービスはミニドライバー entry point [**IWiaMiniDrv::D rvdeleteitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)を呼び出します。 このメソッドでは、ミニドライバーは、WIA サービスコンテキストパラメーター *Pwiascontext*が指す項目を削除しようとします。 項目が正常に削除された場合、メソッドは\_OK を返し、デバイスエラー値パラメーター *Pldeverrval*を0に設定します。 デバイスエラーが発生した場合、メソッドは失敗し、 *Pldeverrval*にデバイス固有のエラー値を返します。 ミニドライバーは、すべての接続されているアプリケーションに対して項目が削除されたことを通知するために、 [**Wiasqueueevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)関数を呼び出す必要があります。

ルート項目が削除されると、WIA サービスは[**IWiaMiniDrv::D rvfreedrvitemcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)を呼び出して、ドライバー固有のコンテキストで使用されるリソースを解放します。 その後、WIA サービスによって、項目とドライバー固有のコンテキストが削除されます。

 

 




