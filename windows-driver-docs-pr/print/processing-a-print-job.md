---
title: 印刷ジョブの処理
description: 印刷ジョブの処理
ms.assetid: c5e291d9-069c-4877-a167-862ba5794368
keywords:
- プリントプロセッサ WDK、印刷ジョブ処理
- 印刷ジョブ WDK, 処理
- 印刷ジョブの送信
- ジョブ WDK 印刷、処理
- EMF レコード再生の WDK プリントプロセッサ
- N-up 印刷 WDK
- PrintDocumentOnPrintProcessor
- 出力形式 WDK プリントプロセッサ
- 入力形式 WDK プリントプロセッサ
- ジョブ WDK 印刷
- 印刷ジョブ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a8719ecb7612c9a684456ef58fb9e1b8647407b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840427"
---
# <a name="processing-a-print-job"></a>印刷ジョブの処理





スプーラーが印刷プロセッサに印刷ジョブを送信する準備ができたら、印刷プロセッサの[**Openprintprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openprintprocessor)関数を呼び出します。 この関数は、初期化アクティビティを実行し、ハンドルを返します。

スプーラは[**Printdocumentonprintprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)を呼び出すことができます。これは、データストリームを入力形式から出力形式に変換し、変換されたストリームをスプーラに返す print processor 関数です。

入力形式が NT ベースのオペレーティングシステム EMF の場合、 **Printdocumentonprintprocessor**関数は、 [「印刷プロセッサの GDI 関数の使用](using-gdi-functions-in-print-processors.md)」に示されている関数を使用して、emf レコードの再生を制御できます。 これらの関数は、プリントプロセッサとプリンタードライバーの間のインターフェイスを提供します。 このインターフェイスを使用すると、印刷プロセッサはプリンターページの物理的なレイアウトを制御できるため、物理ページごとに複数のドキュメントページを印刷 ("N-up" 印刷) したり、ページを逆順に印刷したり、印刷したりするなどの機能の実装が容易になります。各ページの複数のコピー。

印刷プロセッサの出力データストリームがスプーラに返される必要があります。 通常、データ変換でプリンタードライバーの[プリンターグラフィックス DLL](printer-graphics-dll.md)を操作する必要がある場合 (EMF 入力データの場合と同様)、グラフィックス DLL は[**EngWritePrinter**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)を呼び出すことでスプーラにストリームを返します。 一方、変換でプリンタグラフィックス DLL が呼び出されない場合 (生の入力データの場合と同様)、プリントプロセッサは**Writeprinter** (Microsoft Windows SDK のドキュメントで説明) を呼び出します。

**Printdocumentonprintprocessor**関数は、スプーラからプリントプロセッサの[**controlprintprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-controlprintprocessor)関数への非同期呼び出しによって中断される場合があります。 この関数は、印刷ジョブを一時停止、再開、またはキャンセルするためのアプリケーションの機能を実装します。

**Printdocumentonprintprocessor**は、データストリームの変換を完了してを返した後、印刷プロセッサの[**closeprintprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeprintprocessor)関数を呼び出します。

 

 




