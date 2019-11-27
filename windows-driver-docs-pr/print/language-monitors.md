---
title: 言語モニター
description: 言語モニター
ms.assetid: 26ba1c22-390a-4187-b67a-3f3497964f8e
keywords:
- 印刷モニター WDK、言語モニター
- 言語モニターの WDK 印刷
- 言語モニターの WDK 印刷、言語モニターについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c4046ffe79c986cfc478bf4b2b32be09a83a85b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843253"
---
# <a name="language-monitors"></a>言語モニター





言語モニターは、次の2つの目的で機能するユーザーモードの Dll です。

-   これらは、ソフトウェアからアクセスできる状態情報を提供できる印刷スプーラと双方向のプリンターの間の全二重通信パスを提供します。

-   プリンタージョブ言語によって定義されたコマンドなどのプリンター制御情報をデータストリームに追加します。

Microsoft は、 *printer job language (PJL)* をサポートし、PJL プリンターの双方向通信を提供する、言語モニターである Pjlmon .dll を提供しています。 このモニターは、Microsoft Windows Driver Kit (WDK) の[サンプル言語モニター](sample-language-monitor.md)に含まれています。

カスタマイズされた言語モニターは、一方向または双方向のプリンター用に、他のジョブ制御言語をサポートするように記述できます。

言語モニターはオプションであり、プリンターの INF ファイルに含まれている場合にのみ、特定のプリンターの種類に関連付けられます (「[印刷モニターのインストール](installing-a-print-monitor.md)」を参照)。

プリンターのプロパティ] ダイアログボックスの **[ポート]** タブで **[双方向サポートを有効に]** する チェックボックスをオフにした場合、スプーラは[**startdocport**](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))、 [**writeport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)、 [**enddocport**](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))、 [**GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))を呼び出しません。言語モニターの[**Readport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)関数。 [**双方向サポートを有効に**する] がオフになっている場合でも、スプーラは[**openportex**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))、 [**closeport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)、 [**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))関数を呼び出し続けます。 [**双方向サポートを有効に**する] チェックボックスは、アプリケーションが双方向通信 API で関数を呼び出すときに行われる言語モニターの呼び出しには影響しません。

言語モニターがプリンターに関連付けられている場合、言語モニターはプリンターのデータストリームを印刷プロセッサから受け取り、それを変更して、プリンターのポートモニターに渡します。 詳細については、「[言語およびポートモニターの相互作用](language-and-port-monitor-interaction.md)」を参照してください。

   言語モニターは常に**SendRecvBidiDataFromPort**関数を実装し、 [**MONITOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitor2)構造体の*pfnSendRecvBidiDataFromPort*メンバーに関数のアドレスを含める必要がある**ことに注意**してください。

言語モニターで Bidi がサポートされていない場合、または言語モニターでサポートされていない Bidi スキーマ値が要求に含まれている場合、言語モニターはポートモニターの**SendRecvBidiDataFromPort**関数への呼び出しを転送する必要があります。

 

 

 




