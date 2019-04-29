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
ms.openlocfilehash: dff730dc4167f50d302fb1b9ec83629b77ace5b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388098"
---
# <a name="language-monitors"></a>言語モニター





言語モニターは、2 つの目的のユーザー モード Dll:

-   印刷スプーラとソフトウェアにアクセス可能な状態情報を提供することができる双方向プリンター間の全二重通信パスを提供します。

-   これらは、プリンターのコントロールは、データ ストリームへのプリンター ジョブ言語によって定義されたコマンドなどを追加します。

マイクロソフトは、言語モニター、Pjlmon.dll で、サポートを提供しています*プリンター ジョブ言語 (PJL)*、し PJL プリンターの双方向通信を提供します。 このモニターとして Microsoft Windows Driver Kit (WDK) で含まれている、[サンプル言語モニター](sample-language-monitor.md)します。

その他のジョブ制御言語をサポートするためにカスタマイズされた言語モニターを書き込むことが一方向または双方向プリンターです。

言語モニターは、省略可能なだけ」の説明に従って、プリンターの INF ファイルに含まれている場合は、特定のプリンター型に関連付けられている[印刷モニターをインストール](installing-a-print-monitor.md)します。

オフにした場合**双方向サポートを有効にする** チェック ボックス、**ポート**プリンターのプロパティ ダイアログ ボックス、スプーラーのタブは呼び出しません、 [ **StartDocPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562710)、 [ **WritePort**](https://msdn.microsoft.com/library/windows/hardware/ff563792)、 [ **EndDocPort**](https://msdn.microsoft.com/library/windows/hardware/ff548742)、 [ **GetPrinterDataFromPort**](https://msdn.microsoft.com/library/windows/hardware/ff550506)、 [**して**](https://msdn.microsoft.com/library/windows/hardware/ff561909)言語モニターの機能です。 呼び出す、スプーラーは引き続き、 [ **OpenPortEx**](https://msdn.microsoft.com/library/windows/hardware/ff559596)、 [ **ClosePort**](https://msdn.microsoft.com/library/windows/hardware/ff545975)、 [ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)場合であっても関数**双方向サポートを有効にする**がオフになっています。 **双方向サポートを有効にする** チェック ボックスでは、アプリケーションは、双方向通信 API の関数を呼び出すときに行われた言語モニターへの呼び出しには影響しません。

言語モニターが、プリンターに関連付けられている場合は、言語モニターは、プリント プロセッサからプリンターのデータ ストリームを受信する、変更しとプリンターのポート モニターに渡します。 詳細については、次を参照してください。[言語およびポート モニターの相互作用](language-and-port-monitor-interaction.md)します。

**注**  常に言語モニターを実装する必要があります、 **SendRecvBidiDataFromPort**関数し、で、関数のアドレスが含まれて、 *pfnSendRecvBidiDataFromPort*メンバー、 [ **MONITOR2** ](https://msdn.microsoft.com/library/windows/hardware/ff557532)構造体。

言語モニター ポート モニターへの呼び出しを転送する必要があります、言語モニターが、Bidi をサポートしていないか、Bidi スキーマ値で、言語モニターがサポートされていませんが、要求に含まれています、こと**SendRecvBidiDataFromPort**関数。

 

 

 




