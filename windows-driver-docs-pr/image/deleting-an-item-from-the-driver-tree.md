---
title: ドライバー ツリーからの項目の削除
description: ドライバー ツリーからの項目の削除
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9a90ca163f6f729995bad4d035d9094234fc88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353803"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>ドライバー ツリーからの項目の削除





ドライバーの項目を削除するためには、WIA サービスはミニドライバーのエントリ ポイントを呼び出します。 [ **IWiaMiniDrv::drvDeleteItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)します。 このメソッドで、ミニドライバーは、WIA がコンテキスト パラメーターをサービスするアイテムを削除する試行*pWiasContext*ポイント。 場合は、項目が正常に削除すると、メソッドを返します。 S\_[ok]、デバイスのエラー値パラメーターを*plDevErrVal*、ゼロにします。 メソッドが失敗し、デバイスに固有のエラー値を返しますデバイス エラーが発生した場合*plDevErrVal*します。 ミニドライバーを呼び出す必要があります、 [ **wiasQueueEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)接続されているすべてのアプリケーションのアイテムが削除されたことを通知する関数。

WIA サービスが呼び出すルート項目が削除されると、 [ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)ドライバー固有のコンテキストで使用されるリソースを解放します。 WIA サービスは、アイテムと、ドライバー固有のコンテキストを削除します。

 

 




