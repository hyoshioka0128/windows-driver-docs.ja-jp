---
title: 複数プロセッサのサポート
description: 複数プロセッサのサポート
ms.assetid: 906d6b31-a447-4a94-b1a5-cd3028722db7
keywords:
- ユーザーモードディスプレイドライバー WDK Windows Vista、複数プロセッサ
- マルチプロセッササポート WDK ディスプレイ
- 実行時に処理されたマルチプロセッサの最適化の WDK ディスプレイ
- ドライバーで処理されたマルチプロセッサの最適化の WDK ディスプレイ
- マルチプロセッサの最適化 WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d15fdcbc5df5e086b72087f908e4fcca653b572
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829392"
---
# <a name="supporting-multiple-processors"></a>複数プロセッサのサポート


マルチプロセッサコンピューター上のユーザーモード表示ドライバーは、Microsoft Direct3D ランタイムがマルチプロセッサの最適化を処理できるようにしたり、ドライバーが独自のマルチプロセッサの最適化を実行したりすることができます。

### <a name="span-idruntime-handled_multiple-processor_optimizationsspanspan-idruntime-handled_multiple-processor_optimizationsspanspan-idruntime-handled_multiple-processor_optimizationsspanruntime-handled-multiple-processor-optimizations"></a><span id="Runtime-Handled_Multiple-Processor_Optimizations"></span><span id="runtime-handled_multiple-processor_optimizations"></span><span id="RUNTIME-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>実行時に処理されたマルチプロセッサの最適化

Direct3D ランタイムによって処理されるマルチプロセッサの最適化は、 [**Lockasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)、および[**Rename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)の各関数をサポートするドライバーでのみ有効になります。 これらの関数を使用すると、動的リソースを頻繁にロックするアプリケーションでマルチプロセッサの最適化を効果的に行うことができます。 *Lockasync*関数と*UnlockAsync*関数は、 [**getquerydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getquerydata)関数と共に、0x0000000B 以上の DDI バージョンを公開するドライバーで再入可能である必要があります。 ドライバーは、ドライバーの[**openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter)関数の呼び出しで、 [**D3D10DDIARG\_openadapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)構造体の**driverversion**メンバーの DDI バージョンの値を返します。 ランタイムが再入可能な方法でドライバー関数を呼び出すと、同じディスプレイデバイスを参照する別のスレッドが別のドライバー関数内で実行されている間に、その関数内で1つのスレッドが実行される可能性があります。

Direct3D ランタイムは、状況によっては複数プロセッサの最適化を使用して、作業を別のプロセッサにオフロードし、コンピューターのパフォーマンスを向上させます。 マルチプロセッサの最適化を有効にすると、Direct3D ランタイムとユーザーモードの表示ドライバーの間に追加のソフトウェアレイヤーが追加されます。 このソフトウェアレイヤーは、Direct3D ランタイムがユーザーモードの表示ドライバーの機能に対して行うすべての呼び出しをインターセプトします。

ユーザーモードの表示ドライバーを直接呼び出すのではなく、ソフトウェアレイヤーは、ワーカースレッドが非同期的に処理するバッチにコマンドをキューに入れます。 ただし、ソフトウェアレイヤーでは、ユーザーモードの表示ドライバーの機能に対して行われたすべての呼び出しをバッチ処理することはできません。 特に、情報を返す関数 ( [**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)など) の呼び出しをソフトウェアレイヤーでバッチ処理することはできません。 ソフトウェアレイヤーは、これらの種類のドライバー関数のいずれかを呼び出す必要がある場合、キューに置かれているすべてのコマンドをワーカースレッドからフラッシュし、ソフトウェアレイヤーがメインアプリケーションスレッドでドライバーの機能を呼び出します。

### <a name="span-iddriver-handled_multiple-processor_optimizationsspanspan-iddriver-handled_multiple-processor_optimizationsspanspan-iddriver-handled_multiple-processor_optimizationsspandriver-handled-multiple-processor-optimizations"></a><span id="Driver-Handled_Multiple-Processor_Optimizations"></span><span id="driver-handled_multiple-processor_optimizations"></span><span id="DRIVER-HANDLED_MULTIPLE-PROCESSOR_OPTIMIZATIONS"></span>ドライバーで処理されたマルチプロセッサの最適化

ドライバーが独自のマルチプロセッサの最適化を実行する場合、 [**Lockasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)、 [**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)、 [**Rename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rename)の各関数を実装する必要はありません。 この場合、ドライバーは、ランタイムがワーカースレッドからランタイムのコールバック関数への呼び出しの受信を開始または停止するかどうかをランタイムに通知するために、 [**pfnSetAsyncCallbacksCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setasynccallbackscb)関数を呼び出す必要があります。

ドライバーが独自のマルチプロセッサの最適化を実行する場合は、Direct3D ランタイムがマルチプロセッサの最適化を有効にすることを決定するときに使用するのと同じポリシーに従う必要があります。 このポリシーにより、すべてのプロセスでシステムリソースを公平に共有できるようになります。 特に、次のような場合に、ドライバーはマルチプロセッサの最適化を無効にする必要があります。

-   アプリケーションはウィンドウモードで実行されます。

-   コンピューターにはプロセッサ (またはプロセッサコア) が1つだけ含まれています。ドライバーは、ハイパースレッディングを使用するシングルプロセッサコンピューターでの最適化を無効にする必要があります。

-   アプリケーションは、マルチプロセッサの最適化が有効になっていないことを要求したか、アプリケーションがソフトウェアの頂点処理を使用しています。この情報は、ドライバーの[**CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)関数に渡されます。

これらのいずれかの状況でベンダーがマルチプロセッサの最適化を有効にする場合は、最初に Microsoft に問い合わせる必要があります。

 

 





