---
title: ポートの追加
description: ポートの追加
ms.assetid: ec908ddd-761b-4a82-8fc3-ac45c39a0571
keywords:
- ポート管理 WDK 印刷、ポートの追加
- ポートの追加
- AddPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2f12c5a784dcd61b9934c1fc3ad10c903bfa588
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824784"
---
# <a name="adding-a-port"></a>ポートの追加





ポートを追加するには、ポートモニターサーバー DLL のローカルストレージまたはレジストリ内に、ポートの名前とユーザーが変更可能な構成情報を格納します。

アプリケーションが印刷スプーラの AddPort 関数 (Microsoft Windows SDK のドキュメントで説明されています) を呼び出すと、ポートモニターの名前が関数の引数として指定されます。 スプーラは、指定されたポートモニタのポートモニタ UI DLL に含まれる[**AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)関数を呼び出します。

ポートモニターの UI DLL の[**AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)関数は、次の操作を実行する必要があります。

1.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの OpenPrinter 関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvOpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)関数が呼び出されます。

2.  印刷スプーラの[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数を複数回呼び出して、ポートモニタサーバー dll にポートを追加し、UI dll とサーバー dll 間で構成情報を転送するように要求します。 **XcvData**関数は、サーバー DLL の[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)関数を呼び出します。 [**AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)関数は、通常、ダイアログボックスを表示して、ユーザーから構成情報を取得します。

3.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの ClosePrinter 関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)関数が呼び出されます。

これらの操作の詳細については、 [**AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)の説明を参照してください。 「[ポート構成情報の格納](storing-port-configuration-information.md)」も参照してください。

ポートモニターの[**enumports**](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))関数は、追加されたすべてのポートを列挙する必要があります。 スプーラは、各ポートモニタの**Enumports**関数を呼び出して、プリントサーバーでサポートされているポートのセットを特定できます。

 

 




