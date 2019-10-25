---
title: 印刷ジョブの印刷
description: 印刷ジョブの印刷
ms.assetid: 2e881f99-9dbe-4e89-8628-feb05137c9b0
keywords:
- 印刷モニター WDK、印刷ジョブ
- 印刷ジョブ WDK, 印刷
- ジョブ WDK 印刷、印刷
- WritePort
- ReadPort
- GetPrinterDataFromPort
- 双方向通信の WDK 印刷
- bidi 通信 WDK 印刷
- 印刷ジョブの印刷 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71d83ec3c023570b81e1594dae3e41a443c3d935
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840429"
---
# <a name="printing-a-print-job"></a>印刷ジョブの印刷





ポートを開いた後、「[ポートを開いて閉じる](opening-and-closing-a-port.md)」で説明されているように、スプーラは印刷ジョブをポートに送信できます。

各印刷ジョブは、言語またはポートモニターの[**startdocport**](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))関数および[**enddocport**](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))関数のスプーラ呼び出しによって区切られます。 スプーラーは、プリントプロセッサがスプーラの**Startdocprinter**関数と**enddocprinter**関数を呼び出すときに、これらの関数を呼び出します。これについては、Microsoft Windows SDK のドキュメントを参照してください。 一連の**startdocport**および**enddocport**関数のスコープ内では、モニターの[**writeport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)、 [**readport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)、および[**GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))関数に対する無制限のスプーラ呼び出しが発生する可能性があります。

これらの各関数では、 [**Openportex**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)) (または[**openport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)) によって返されるポートハンドルを入力引数として指定する必要があります。 通常、言語モニターは、関連付けられているポートモニターで like 名前付き関数を呼び出すことによって、各関数を実装します。

スプーラーが、データストリームをポートに送信するために言語モニターの**Writeport**関数を呼び出すと、通常、この関数は、 *PJL*コマンドなどの言語固有の情報を、関連付けられたに渡す前に、受信したデータストリームに追加します。ポートモニターの**Writeport**関数。

**Readport**関数は、双方向プリンターハードウェアからステータス情報を取得するために使用されます。言語モニターは、Windows SDK のドキュメントで説明されている**setport**を呼び出すことによってスプーラに送信する場合があります。 スプーラは**Readport**関数を呼び出しません。

印刷ハードウェアが双方向である場合は、言語モニターとポートモニターの両方で**GetPrinterDataFromPort**関数がサポートされている必要があります。 言語モニターの**GetPrinterDataFromPort**関数は、入力としてレジストリ値の名前を受け取り、その名前の値を取得します (通常、関連付けられているポートモニターの**Writeport**および**readport**関数を呼び出します)。呼び出し元に値を指定します。 ポートモニターの**GetPrinterDataFromPort**関数は、入力として i/o 制御コードを受け入れる必要があります。 (Windows SDK のドキュメントで説明されている) [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出して、制御コードをポートドライバーに渡し、結果を返します。

 

 




