---
title: ポートの構成
description: ポートの構成
ms.assetid: f5996e94-aa48-4aa0-82f5-331a57d2fb6b
keywords:
- ポート管理 WDK 印刷、ポートの構成
- ConfigurePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a50bed088d0aaea74f55ff2c7661bdd1324df2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843681"
---
# <a name="configuring-a-port"></a>ポートの構成





ポートの構成は、以前に追加されたポートに対してポートモニターサーバー DLL の格納されている構成情報を変更することで行います。

アプリケーションが印刷スプーラの[**ConfigurePort**](https://docs.microsoft.com/previous-versions/ff546286(v=vs.85))関数 (Microsoft Windows SDK のドキュメントで説明) を呼び出すと、 **ConfigurePort**関数は、のポートモニター UI DLL に含まれている[**ConfigurePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)関数を呼び出します。適切なポートモニター。

ポートモニターの UI DLL の[**ConfigurePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)関数は、次の操作を実行する必要があります。

1.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの OpenPrinter 関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvOpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)関数が呼び出されます。

2.  印刷スプーラの[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数を1回以上呼び出して、UI dll とサーバー DLL の間で構成情報を転送します。 **XcvData**関数は、サーバー DLL の[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)関数を呼び出します。 [**ConfigurePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)関数は、通常、ダイアログボックスを表示して、ユーザーから構成情報を取得します。

3.  (Windows SDK のドキュメントで説明されている) 印刷スプーラの ClosePrinter 関数を呼び出します。これにより、ポートモニターサーバー DLL の[**XcvClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)関数が呼び出されます。

これらの操作の詳細については、 [**ConfigurePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)の説明を参照してください。 「[ポート構成情報の格納](storing-port-configuration-information.md)」も参照してください。

 

 




