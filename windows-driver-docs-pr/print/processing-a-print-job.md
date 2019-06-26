---
title: 印刷ジョブの処理
description: 印刷ジョブの処理
ms.assetid: c5e291d9-069c-4877-a167-862ba5794368
keywords:
- WDK のプロセッサの印刷、印刷ジョブの処理
- WDK の印刷ジョブ、処理
- 印刷ジョブを送信します。
- WDK 印刷、処理のジョブ
- EMF レコード再生 WDK プリント プロセッサ
- N アップ印刷 WDK
- PrintDocumentOnPrintProcessor
- WDK の出力形式のプリント プロセッサ
- 入力形式 WDK のプリント プロセッサ
- WDK のジョブを印刷します。
- WDK の印刷ジョブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96ffaf327ea69f80653b85e6d088114a0d333ea1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356029"
---
# <a name="processing-a-print-job"></a>印刷ジョブの処理





プリント プロセッサの呼び出し、スプーラーのプリント プロセッサに印刷ジョブを送信する準備ができたら[ **OpenPrintProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openprintprocessor)関数。 この関数は、初期化する操作を実行し、ハンドルを返します。

スプーラーを呼び出して[ **PrintDocumentOnPrintProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-printdocumentonprintprocessor)、プリント プロセッサ関数入力形式からのデータ ストリームを出力形式に変換し、変換されたを返しますスプーラーにストリームします。

入力の形式は、EMF、NT-ベースのオペレーティング システムの場合、 **PrintDocumentOnPrintProcessor**関数は、記載関数を使用して EMF レコードの再生を制御できます[のプリント プロセッサで GDI 関数の使用](using-gdi-functions-in-print-processors.md). これらの関数は、プリント プロセッサと、プリンター ドライバー間のインターフェイスを提供します。 このインターフェイスは、印刷ページの物理的なレイアウトを制御するプリント プロセッサを使用し、したがって物理ページ ("n-up"印刷) ごとに複数のドキュメント ページの印刷などの機能の実装を容易に、逆の順序でページを印刷および印刷各ページの複数のコピー。

プリント プロセッサの出力データ ストリームは、スプーラーに返される必要があります。 通常、データ変換をかどうかは、プリンター ドライバーの対話が必要です[プリンター グラフィックス DLL](printer-graphics-dll.md) (EMF 入力データの場合は、として、) 呼び出すことによってグラフィックスの DLL がスプーラーにストリームを返します[ **EngWritePrinter**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)します。 その一方で (生の入力データの場合と同様)、変換でプリンター グラフィックス DLL が要求されていない場合に、プリント プロセッサ呼び出します**WritePrinter** (Microsoft Windows SDK のドキュメントで説明)。

**PrintDocumentOnPrintProcessor**関数は、スプーラーからプリント プロセッサへの非同期の呼び出しによって中断されることができます[ **ControlPrintProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-controlprintprocessor)関数。 この関数は、一時停止、再開、または印刷ジョブをキャンセルするアプリケーションの機能を実装します。

後**PrintDocumentOnPrintProcessor**データ ストリームとを返します。 変換が完了すると、スプーラーを呼び出す、のプリント プロセッサ[ **ClosePrintProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-closeprintprocessor)関数。

 

 




