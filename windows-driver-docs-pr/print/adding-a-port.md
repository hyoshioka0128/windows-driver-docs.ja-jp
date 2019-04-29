---
title: ポートの追加
description: ポートの追加
ms.assetid: ec908ddd-761b-4a82-8fc3-ac45c39a0571
keywords:
- ポート管理 WDK の印刷、ポートの追加
- ポートの追加
- AddPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613cb46a4fd7c383c008c7212bc4fd928dc36c67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390621"
---
# <a name="adding-a-port"></a>ポートの追加





ポートの追加は、ポートの名前とポート モニター サーバー DLL のローカル ストレージ内またはレジストリ内のユーザーが変更可能な構成情報を格納するので構成されます。

アプリケーション (Microsoft Windows SDK のドキュメントで説明)、印刷スプーラー AddPort 関数を呼び出すときに、関数の引数としてポート モニターの名前を指定します。 スプーラ呼び出し、 [ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)ポート モニターは、指定されたポート モニタの UI の DLL に含まれる関数。

ポート モニター UI の DLL の[ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)関数は、次の操作を実行する必要があります。

1.  関数を呼び出して印刷スプーラーのようになりました (Windows SDK のドキュメントで説明)、これにより、 [ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)ポート監視のサーバー DLL を呼び出す関数。

2.  印刷スプーラーを呼び出す[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)を複数回にポート監視サーバーのポートを追加して、UI の DLL と、サーバー DLL 間構成情報を転送する DLL を要求する機能します。 **XcvData**関数呼び出しのサーバー DLL の[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)関数。 [ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)関数通常構成情報を取得、ユーザーからのダイアログ ボックスを表示することで。

3.  関数を呼び出して、印刷スプーラー ClosePrinter (Windows SDK のドキュメントで説明)、これにより、 [ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)ポート監視のサーバー DLL を呼び出す関数。

これらの操作の詳細については、の説明を参照してください。 [ **AddPortUI**](https://msdn.microsoft.com/library/windows/hardware/ff545026)します。 参照してください[ポートの構成情報を格納する](storing-port-configuration-information.md)します。

ポート モニタを[ **EnumPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff548754)関数が追加されているすべてのポートを列挙する必要があります。 各ポート モニターを呼び出すことができます、スプーラー **EnumPorts**プリント サーバーでサポートされているポートのセットを決定する関数。

 

 




