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
ms.openlocfilehash: 9cfd3480d7f509280c5cbd43f2e925b784d80747
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369008"
---
# <a name="adding-a-port"></a>ポートの追加





ポートの追加は、ポートの名前とポート モニター サーバー DLL のローカル ストレージ内またはレジストリ内のユーザーが変更可能な構成情報を格納するので構成されます。

アプリケーション (Microsoft Windows SDK のドキュメントで説明)、印刷スプーラー AddPort 関数を呼び出すときに、関数の引数としてポート モニターの名前を指定します。 スプーラ呼び出し、 [ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)ポート モニターは、指定されたポート モニタの UI の DLL に含まれる関数。

ポート モニター UI の DLL の[ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)関数は、次の操作を実行する必要があります。

1.  関数を呼び出して印刷スプーラーのようになりました (Windows SDK のドキュメントで説明)、これにより、 [ **XcvOpenPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvopenport)ポート監視のサーバー DLL を呼び出す関数。

2.  印刷スプーラーを呼び出す[ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))を複数回にポート監視サーバーのポートを追加して、UI の DLL と、サーバー DLL 間構成情報を転送する DLL を要求する機能します。 **XcvData**関数呼び出しのサーバー DLL の[ **XcvDataPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvdataport)関数。 [ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)関数通常構成情報を取得、ユーザーからのダイアログ ボックスを表示することで。

3.  関数を呼び出して、印刷スプーラー ClosePrinter (Windows SDK のドキュメントで説明)、これにより、 [ **XcvClosePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvcloseport)ポート監視のサーバー DLL を呼び出す関数。

これらの操作の詳細については、の説明を参照してください。 [ **AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)します。 参照してください[ポートの構成情報を格納する](storing-port-configuration-information.md)します。

ポート モニタを[ **EnumPorts** ](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))関数が追加されているすべてのポートを列挙する必要があります。 各ポート モニターを呼び出すことができます、スプーラー **EnumPorts**プリント サーバーでサポートされているポートのセットを決定する関数。

 

 




