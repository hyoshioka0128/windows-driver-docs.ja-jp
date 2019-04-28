---
title: 印刷モニターの初期化
description: 印刷モニターの初期化
ms.assetid: 006727dd-aa0f-451c-b1c9-983d0c6401df
keywords:
- 印刷 WDK、モニターの初期化
- 印刷のモニターを初期化しています
- LoadLibrary
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99f076d476af37b77dbfe2376e3a7172164ed519
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362765"
---
# <a name="initializing-a-print-monitor"></a>印刷モニターの初期化





スプーラは、印刷モニター DLL を読み込む LoadLibrary を呼び出し、システムは、DLL の直後を呼び出します。 **DllEntryPoint**関数。 一般のエントリ ポイント関数を呼び出す DisableThreadLibraryCalls、DLL はスレッドが作成され、削除されたときに不必要に通知しないよう、Microsoft Windows SDK のドキュメントで説明されていることをお勧めします。

各 DLL は、LoadLibrary の呼び出し後、スプーラーが呼び出して初期化関数をエクスポートします。 言語は、Dll を監視し、ポートの監視のサーバー Dll のエクスポート、 [ **InitializePrintMonitor2** ](https://msdn.microsoft.com/library/windows/hardware/ff551605)関数。 ポート モニター UI の Dll のエクスポート、 [ **InitializePrintMonitorUI** ](https://msdn.microsoft.com/library/windows/hardware/ff551608)関数。

残りの部分にポインターを返すため、これら 2 つの初期化関数は、[印刷のモニターが定義されている関数](functions-defined-by-print-monitors.md)スプーラーが呼び出すことができます。 初期化関数では、負荷時の初期化の操作も実行できます。 モニターの[ **InitializePrintMonitor2** ](https://msdn.microsoft.com/library/windows/hardware/ff551605)関数は、モニターのインスタンス ハンドルを返します。 モニターは、インスタンス固有の情報を格納するローカル メモリを割り当てるし、モニターのハンドルを割り当てられたメモリの識別子として使用する必要があります。

スプーラが開始されると、すべてのモニターがインストールされている Dll を読み込みます。 すべてのモニターの初期化関数を呼び出した後は、スプーラーは各ポート モニターを呼び出します。 [ **EnumPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff548754)関数で、モニターでサポートされているポートを列挙します。 (モニターをサポートしているポート、ポートが、モニターのデータベースに追加されている場合」の説明に従って[ポートを追加する](adding-a-port.md))。」の説明に従って、ポートを開くはサポートされている各[ポートを開いたり閉じたり](opening-and-closing-a-port.md)します。

 

 




