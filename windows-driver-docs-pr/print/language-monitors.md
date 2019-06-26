---
title: 言語モニター
description: 言語モニター
ms.assetid: 26ba1c22-390a-4187-b67a-3f3497964f8e
keywords:
- 印刷モニター WDK、言語モニター
- 言語モニター WDK を印刷します。
- 言語モニター WDK を印刷する言語モニタについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2680b98b86f826898bf92c4213a80b0b3f19d43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353539"
---
# <a name="language-monitors"></a>言語モニター





言語モニターは、2 つの目的のユーザー モード Dll:

-   印刷スプーラとソフトウェアにアクセス可能な状態情報を提供することができる双方向プリンター間の全二重通信パスを提供します。

-   これらは、プリンターのコントロールは、データ ストリームへのプリンター ジョブ言語によって定義されたコマンドなどを追加します。

マイクロソフトは、言語モニター、Pjlmon.dll で、サポートを提供しています*プリンター ジョブ言語 (PJL)* 、し PJL プリンターの双方向通信を提供します。 このモニターとして Microsoft Windows Driver Kit (WDK) で含まれている、[サンプル言語モニター](sample-language-monitor.md)します。

その他のジョブ制御言語をサポートするためにカスタマイズされた言語モニターを書き込むことが一方向または双方向プリンターです。

言語モニターは、省略可能なだけ」の説明に従って、プリンターの INF ファイルに含まれている場合は、特定のプリンター型に関連付けられている[印刷モニターをインストール](installing-a-print-monitor.md)します。

オフにした場合**双方向サポートを有効にする** チェック ボックス、**ポート**プリンターのプロパティ ダイアログ ボックス、スプーラーのタブは呼び出しません、 [ **StartDocPort** ](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))、 [ **WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)、 [ **EndDocPort**](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))、 [ **GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))、 [**して**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)言語モニターの機能です。 呼び出す、スプーラーは引き続き、 [ **OpenPortEx**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))、 [ **ClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-closeport)、 [ **SendRecvBidiDataFromPort** ](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))場合であっても関数**双方向サポートを有効にする**がオフになっています。 **双方向サポートを有効にする** チェック ボックスでは、アプリケーションは、双方向通信 API の関数を呼び出すときに行われた言語モニターへの呼び出しには影響しません。

言語モニターが、プリンターに関連付けられている場合は、言語モニターは、プリント プロセッサからプリンターのデータ ストリームを受信する、変更しとプリンターのポート モニターに渡します。 詳細については、次を参照してください。[言語およびポート モニターの相互作用](language-and-port-monitor-interaction.md)します。

**注**  常に言語モニターを実装する必要があります、 **SendRecvBidiDataFromPort**関数し、で、関数のアドレスが含まれて、 *pfnSendRecvBidiDataFromPort*メンバー、 [ **MONITOR2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_monitor2)構造体。

言語モニター ポート モニターへの呼び出しを転送する必要があります、言語モニターが、Bidi をサポートしていないか、Bidi スキーマ値で、言語モニターがサポートされていませんが、要求に含まれています、こと**SendRecvBidiDataFromPort**関数。

 

 

 




