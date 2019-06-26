---
title: 印刷ジョブの印刷
description: 印刷ジョブの印刷
ms.assetid: 2e881f99-9dbe-4e89-8628-feb05137c9b0
keywords:
- 印刷モニター WDK、印刷ジョブの印刷
- WDK の印刷ジョブ, 印刷
- WDK の印刷、印刷ジョブ
- WritePort
- して
- GetPrinterDataFromPort
- 双方向通信 WDK の印刷
- 双方向通信 WDK の印刷
- WDK の印刷ジョブの印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef56613fab90d24c0806bd9a5b23b700f5ab6acd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356028"
---
# <a name="printing-a-print-job"></a>印刷ジョブの印刷





」の説明に従って、ポートが開かれた後[ポートを開いたり閉じたり](opening-and-closing-a-port.md)スプーラーは印刷ジョブをポートに送信できます。

各印刷ジョブは、言語またはポート モニターのスプーラーの呼び出しで区切られた[ **StartDocPort** ](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))と[ **EndDocPort** ](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))関数。 スプーラがプリント プロセッサが、スプーラーを呼び出すときに、これらの関数を呼び出す**StartDocPrinter**と**EndDocPrinter**関数で、Microsoft Windows SDK のドキュメントに記載されています。 一連のスコープ内で**StartDocPort**と**EndDocPort**関数、モニターの無制限のスプーラー呼び出し[ **WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)、[**して**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)、および[ **GetPrinterDataFromPort** ](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))関数が発生することができます。

これらの関数によって返されるポート ハンドルが必要です[ **OpenPortEx** ](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)) (または[ **OpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openport)) を入力引数のように指定できます。 通常、言語モニターを実装する各関数が関連付けられているポート モニターのような名前付き関数を呼び出すことによって。

スプーラが、言語モニターを呼び出すときに**WritePort**ポートにデータ ストリームを送信する関数を関数で、言語固有の情報をなど追加通常*PJL*コマンドを受信したデータ関連付けられているポート モニターに渡す前にストリーム**WritePort**関数。

**して**関数を呼び出すことによって、言語モニターが、スプーラーに送信する双方向プリンターのハードウェアからステータス情報を取得するために使用**割り込みが**Windows に記述されています。SDK のドキュメントです。 スプーラは呼び出しません、**して**関数。

印刷のハードウェアが双方向の場合は、言語モニターとそのポート モニターの両方をサポートする必要があります、 **GetPrinterDataFromPort**関数。 言語モニターの**GetPrinterDataFromPort**関数は、レジストリ値の名前を入力としてを受け入れるよう、その名前の値を取得する必要があります (ポート モニターの一般に呼び出すことによって関連付けられている**WritePort**と**関数**)、呼び出し元に値を返します。 ポート モニタを**GetPrinterDataFromPort**関数には、入力、呼び出しとしての I/O 制御コードがそのまま使用する必要があります[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Windows SDK のドキュメントで説明)ポートのドライバーにコントロールのコードを渡すし、結果が返されます。

 

 




