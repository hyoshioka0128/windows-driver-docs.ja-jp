---
title: ポートの構成
description: ポートの構成
ms.assetid: f5996e94-aa48-4aa0-82f5-331a57d2fb6b
keywords:
- ポート管理 WDK の印刷、ポートを構成します。
- ConfigurePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8407e96d073b73556cfe1f50abc7683ee91fb95b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330311"
---
# <a name="configuring-a-port"></a>ポートの構成





ポートの構成は、以前に追加されたポートのポート モニター サーバー DLL の格納されている構成情報を変更することで構成されます。

アプリケーションから印刷スプーラの[ **ConfigurePort** ](https://msdn.microsoft.com/library/windows/hardware/ff546286) (Microsoft Windows SDK のドキュメントで説明)、関数、 **ConfigurePort**関数呼び出し[ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)ポート モニター、適切なポート モニターの UI の DLL に含まれる関数。

ポート モニター UI の DLL の[ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)関数は、次の操作を実行する必要があります。

1.  関数を呼び出して印刷スプーラーのようになりました (Windows SDK のドキュメントで説明)、これにより、 [ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)ポート監視のサーバー DLL を呼び出す関数。

2.  印刷スプーラーを呼び出す[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255) UI の DLL と、サーバー DLL 間構成情報を転送する 1 つ以上の時間に機能します。 **XcvData**関数呼び出しのサーバー DLL の[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)関数。 [ **ConfigurePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546290)関数通常構成情報を取得、ユーザーからのダイアログ ボックスを表示することで。

3.  関数を呼び出して、印刷スプーラー ClosePrinter (Windows SDK のドキュメントで説明)、これにより、 [ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)ポート監視のサーバー DLL を呼び出す関数。

これらの操作の詳細については、の説明を参照してください。 [ **ConfigurePortUI**](https://msdn.microsoft.com/library/windows/hardware/ff546290)します。 参照してください[ポートの構成情報を格納する](storing-port-configuration-information.md)します。

 

 




