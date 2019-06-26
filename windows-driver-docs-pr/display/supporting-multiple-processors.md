---
title: 複数プロセッサのサポート
description: 複数プロセッサのサポート
ms.assetid: 906d6b31-a447-4a94-b1a5-cd3028722db7
keywords:
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista では、複数のプロセッサ
- 複数のプロセッサ サポート WDK の表示
- 複数プロセッサの最適化のランタイム処理 WDK の表示
- ドライバーで処理される複数のプロセッサの最適化 WDK の表示します。
- 複数プロセッサの最適化 WDK を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d2d04c42b662d4aa3688b27619a1cf964b86f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380551"
---
# <a name="supporting-multiple-processors"></a>複数プロセッサのサポート


マルチ プロセッサ コンピューターでユーザー モードのディスプレイ ドライバーが、マイクロソフトの Direct3D ランタイムの複数プロセッサの最適化を処理できます。 または、ドライバーは、独自のマルチ プロセッサの最適化を実行できます。

### <a name="span-idruntime-handledmultiple-processoroptimizationsspanspan-idruntime-handledmultiple-processoroptimizationsspanspan-idruntime-handledmultiple-processoroptimizationsspanruntime-handled-multiple-processor-optimizations"></a><span id="Runtime-Handled_Multiple-Processor_Optimizations"></span><span id="runtime-handled_multiple-processor_optimizations"></span><span id="RUNTIME-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>ランタイムで処理される複数プロセッサの最適化

サポートするドライバーだけで Direct3D ランタイムによって処理される複数のプロセッサの最適化が有効になっている、 [ **LockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)、および[**の名前を変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)関数。 これらの関数は、頻繁に動的リソースをロックするアプリケーションでうまく機能する複数プロセッサの最適化を有効にします。 *LockAsync*と*UnlockAsync*関数--と共にで、 [ **GetQueryData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getquerydata)関数 - ドライバーの再入可能である必要がありますが以上の 0x0000000B DDI バージョンを公開します。 ドライバーが DDI バージョン値を返します、 **DriverVersion**のメンバー、 [ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)ドライバーのへの呼び出しで構造体[**OpenAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)関数。 ランタイムが再入可能な方法でドライバー関数を呼び出すときに、1 つのスレッドは内に別のドライバー関数内で同じディスプレイ デバイスを参照する別のスレッドの実行中の関数を実行できます。

Direct3D のランタイムを別々 のプロセッサに作業をオフロードし、コンピューターのパフォーマンスを向上させるいくつかの状況でマルチ プロセッサの最適化を使用します。 複数プロセッサの最適化を有効にすると、Direct3D のランタイムと、ユーザー モードのディスプレイ ドライバーの間、追加のソフトウェア レイヤーが追加されます。 このソフトウェアのレイヤーでは、Direct3D ランタイムは、ユーザー モードのディスプレイ ドライバーの機能を構成するそれ以外の場合、すべての呼び出しをインターセプトします。

ソフトウェアのレイヤーは、ワーカー スレッドを非同期的に処理するバッチにコマンドをキュー、ユーザー モードを呼び出す代わりには、ドライバーを直接表示されます。 ただし、ソフトウェア レイヤーは、ユーザー モードのディスプレイ ドライバーの機能に加えられたすべての呼び出しをバッチすることはできません。 具体的には、ソフトウェアのレイヤーが情報を返す関数への呼び出しをバッチことはできません (たとえば、 [ **CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource))。 ソフトウェアのレイヤーには、これらの種類のドライバーの関数のいずれかを呼び出す必要がありますと、ワーカー スレッドですべてのキューに置かれたコマンドをフラッシュ ソフトウェア レイヤーがメイン アプリケーション スレッドでドライバー関数を呼び出すし。

### <a name="span-iddriver-handledmultiple-processoroptimizationsspanspan-iddriver-handledmultiple-processoroptimizationsspanspan-iddriver-handledmultiple-processoroptimizationsspandriver-handled-multiple-processor-optimizations"></a><span id="Driver-Handled_Multiple-Processor_Optimizations"></span><span id="driver-handled_multiple-processor_optimizations"></span><span id="DRIVER-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>ドライバーで処理される複数のプロセッサの最適化

場合、ドライバーは、独自のマルチ プロセッサの最適化を実行する必要がありますを実装していない[ **LockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [ **UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)と[**の名前を変更**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)関数。 このような状況で、ドライバーを呼び出す必要があります、 [ **pfnSetAsyncCallbacksCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setasynccallbackscb)ランタイムを開始または受信を停止するかどうか、ランタイムに通知する関数呼び出しからの実行時のコールバック関数をワーカー スレッド。

ドライバーは、独自のマルチ プロセッサの最適化を実行する場合は、Direct3D ランタイムが複数プロセッサの最適化を有効にすると判断した場合に使用する同じポリシーに従う必要があります。 このポリシーは、すべてのプロセスでシステム リソースの公正な共有を有効します。 具体的には、ドライバーは、次の状況での複数プロセッサの最適化を無効にする必要があります。

-   アプリケーションは、ウィンドウ表示モードで実行されます。

-   コンピューターには、1 つだけプロセッサ (またはプロセッサ コア) が含まれています。ドライバーは、ハイパー スレッディング シングル プロセッサ コンピューターでの最適化を無効にする必要があります。

-   アプリケーションでは、複数プロセッサの最適化を有効にするありません、要求されたか、アプリケーションは、ソフトウェアの頂点の処理を使用してこの情報は、ドライバーの[ **CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数。

ベンダーは、このような状況のいずれかでマルチ プロセッサの最適化を有効にする場合、Microsoft 最初に接続する必要があります。

 

 





