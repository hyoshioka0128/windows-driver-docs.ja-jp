---
title: WinDbg でのプロセスとスレッドの制御
description: WinDbg でのプロセスとスレッドの制御
ms.assetid: d4755889-9a65-4e81-b3a3-e0bbc6324d3e
keywords:
- デバッグ情報のウィンドウ、プロセスとスレッド ウィンドウ
- プロセスとスレッド ウィンドウ
- プロセス、プロセスとスレッド ウィンドウ
- スレッド、プロセスとスレッド ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee0b3de8d15f9fa23b2c7c754efbcf7716f5e14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362407"
---
# <a name="controlling-processes-and-threads-in-windbg"></a>WinDbg でのプロセスとスレッドの制御


## <span id="ddk_processes_and_threads_window_dbg"></span><span id="DDK_PROCESSES_AND_THREADS_WINDOW_DBG"></span>


、WinDbg では、プロセスとスレッドのウィンドウには、システム、プロセス、およびデバッグ中のスレッドに関する情報が表示されます。 このウィンドウを使用して、新しいシステム、プロセス、およびアクティブ化するスレッドを選択することもできます。

### <a name="span-idopeningtheprocessesandthreadswindowspanspan-idopeningtheprocessesandthreadswindowspanopening-the-processes-and-threads-window"></a><span id="opening_the_processes_and_threads_window"></span><span id="OPENING_THE_PROCESSES_AND_THREADS_WINDOW"></span>プロセスおよびスレッド ウィンドウを開く

プロセスとスレッド ウィンドウを開くには、次のように選択します。**プロセスとスレッド**から、**ビュー**メニュー。 (ALT + 9 キーを押すこともできますかをクリックして、**プロセスとスレッド**ボタン (![プロセスとスレッドのボタンのスクリーン ショット](images/window-processes-threads.png))、ツールバーの。 ALT + SHIFT + 9 ウィンドウを閉じるプロセスとスレッドです。)

次のスクリーン ショットでは、プロセスとスレッドのウィンドウの例を示します。

![プロセスとスレッドのウィンドウのスクリーン ショット](images/window-prth.png)

プロセスとスレッドのウィンドウには、現在デバッグ中のすべてのプロセスの一覧が表示されます。 プロセスのスレッドは、各プロセスの下に表示されます。 複数のシステムにデバッガーをアタッチすると、システムには、下位のプロセスとの下位に、プロセスのスレッドで、ツリーの最上部に表示されます。

各システムの一覧には、サーバー名およびプロトコルの詳細が含まれています。 デバッガーが実行されているシステムとして識別 **&lt;ローカル&gt;** します。

各プロセスの一覧には、デバッガーが使用するインデックスの内部の 10 進数の処理、16 進数のプロセス ID、およびプロセスに関連付けられているアプリケーションの名前が含まれています。

各スレッドの一覧には、デバッガーを使用する内部の 10 進数のスレッドのインデックスと 16 進数のスレッド ID が含まれます。

### <a name="span-idusingtheprocessesandthreadswindowspanspan-idusingtheprocessesandthreadswindowspanusing-the-processes-and-threads-window"></a><span id="using_the_processes_and_threads_window"></span><span id="USING_THE_PROCESSES_AND_THREADS_WINDOW"></span>プロセスとスレッド ウィンドウを使用してください。

プロセスとスレッド ウィンドウで、現在またはアクティブなシステム、プロセス、およびスレッドが太字で示されます。 新しいシステム、プロセス、またはスレッドをアクティブにするのには、ウィンドウ内の行をクリックします。

プロセスとスレッドのウィンドウには、その他のコマンドをショートカット メニューがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅のアイコンをクリックします。![スクラッチ パッド ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/window-processes-threads.png)). 次の一覧では、メニュー コマンドの一部について説明します。

-   **新しいドッキングするのには移動**プロセスとスレッド ウィンドウを閉じるし、新しいドッキング ステーションで開かれます。

-   **常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   **フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメソッドを表示するか、システムを制御するのでは、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。 その他のメソッドを表示するか、プロセスとスレッドを制御するのでは、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

 

 





