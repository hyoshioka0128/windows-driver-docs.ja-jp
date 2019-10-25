---
title: 印刷モニターの初期化
description: 印刷モニターの初期化
ms.assetid: 006727dd-aa0f-451c-b1c9-983d0c6401df
keywords:
- 印刷モニター WDK、初期化
- 印刷モニターの初期化
- LoadLibrary
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c0e35f11a3f951df81dc68b6f168360972e1eb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842304"
---
# <a name="initializing-a-print-monitor"></a>印刷モニターの初期化





スプーラが、出力モニターの DLL を読み込むために LoadLibrary を呼び出すと、DLL の**Dllentrypoint**関数が直ちに呼び出されます。 通常は、Microsoft Windows SDK のドキュメントで説明されているように、エントリポイント関数で DisableThreadLibraryCalls を呼び出すことをお勧めします。これにより、スレッドが作成されて削除されたときに DLL が不必要に通知されることはありません。

各 DLL は、LoadLibrary を呼び出した後にスプーラが呼び出す初期化関数をエクスポートします。 言語モニター Dll およびポートモニターサーバー Dll は、 [**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)関数をエクスポートします。 ポートモニターの UI Dll は、 [**Initializeprintmonitorui**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitorui)関数をエクスポートします。

これら2つの初期化関数は、[印刷モニターで定義されている](functions-defined-by-print-monitors.md)他の関数へのポインターを返すので、スプーラはこれらの関数を呼び出すことができます。 初期化関数は、読み込み時の初期化操作を実行することもできます。 モニターの[**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)関数は、モニターインスタンスハンドルを返します。 モニターは、インスタンス固有の情報を格納するためにローカルメモリを割り当て、割り当てられたメモリの識別子としてモニターハンドルを使用する必要があります。

スプーラを初めて起動すると、インストールされているすべてのモニター Dll が読み込まれます。 すべてのモニター初期化関数を呼び出した後、スプーラは各ポートモニターの[**Enumports**](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))関数を呼び出します。この関数は、モニターでサポートされているポートを列挙します。 (ポートの[追加](adding-a-port.md)に関するページの説明に従って、ポートがモニターのデータベースに追加されている場合、モニターはポートをサポートします)。次に、「[ポートの開閉](opening-and-closing-a-port.md)」で説明されているように、サポートされている各ポートが開きます。

 

 




