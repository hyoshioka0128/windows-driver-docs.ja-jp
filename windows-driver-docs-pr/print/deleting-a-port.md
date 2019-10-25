---
title: ポートの削除
description: ポートの削除
ms.assetid: 0d491368-e529-4f04-a323-678e31a862c3
keywords:
- ポート管理 WDK 印刷、ポートの削除
- 印刷ポートの削除
- 印刷ポートの削除
- DeletePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e3c494d631b54abcff1275b063a8f7126793d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838881"
---
# <a name="deleting-a-port"></a>ポートの削除





ポートを削除するには、ポートモニターサーバー DLL のローカルストレージまたはレジストリから、ポートの格納されている名前とユーザーが変更可能な構成情報を削除します。

アプリケーションが印刷スプーラの**Deleteport**関数 (Microsoft Windows SDK のドキュメントで説明されています) を呼び出すと、 **deleteport**関数は、のポートモニター UI DLL に含まれている[**DeletePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)関数を呼び出します。適切なポートモニタ。

ポートモニターの UI DLL の**DeletePortUI**関数は、次の操作を実行する必要があります。

1.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの**OpenPrinter**関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvOpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)関数が呼び出されます。

2.  印刷スプーラの[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数を1回以上呼び出して、ポートモニタサーバー DLL にポートの削除を要求します。 **XcvData**関数は、サーバー DLL の[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)関数を呼び出します。

3.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの**Closeprinter**関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)関数が呼び出されます。

これらの操作の詳細については、 [**DeletePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)の説明を参照してください。

 

 




