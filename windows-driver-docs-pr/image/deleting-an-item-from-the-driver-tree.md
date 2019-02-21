---
title: ドライバーのツリーから項目を削除します。
description: ドライバーのツリーから項目を削除します。
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 748b20929d4584d60359508128bc021a04b29526
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552091"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>ドライバーのツリーから項目を削除します。





ドライバーの項目を削除するためには、WIA サービスはミニドライバーのエントリ ポイントを呼び出します。 [ **IWiaMiniDrv::drvDeleteItem**](https://msdn.microsoft.com/library/windows/hardware/ff543961)します。 このメソッドで、ミニドライバーは、WIA がコンテキスト パラメーターをサービスするアイテムを削除する試行*pWiasContext*ポイント。 場合は、項目が正常に削除すると、メソッドを返します。 S\_[ok]、デバイスのエラー値パラメーターを*plDevErrVal*、ゼロにします。 メソッドが失敗し、デバイスに固有のエラー値を返しますデバイス エラーが発生した場合*plDevErrVal*します。 ミニドライバーを呼び出す必要があります、 [ **wiasQueueEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549296)接続されているすべてのアプリケーションのアイテムが削除されたことを通知する関数。

WIA サービスが呼び出すルート項目が削除されると、 [ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543972)ドライバー固有のコンテキストで使用されるリソースを解放します。 WIA サービスは、アイテムと、ドライバー固有のコンテキストを削除します。

 

 




