---
title: ライブ カーネルモード ターゲット
description: ライブ カーネルモード ターゲット
ms.assetid: 88820097-4a47-428d-88dd-d0a08e5debdc
keywords:
- ターゲット、ライブのカーネル モード
- カーネル モードのターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b34235579c9ab5ee99a5c21cc9dfcc99d599b41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366490"
---
# <a name="live-kernel-mode-targets"></a>ライブ カーネルモード ターゲット


## <span id="ddk_live_kernel_mode_targets_dbx"></span><span id="DDK_LIVE_KERNEL_MODE_TARGETS_DBX"></span>


アタッチする、[デバッガー エンジン](introduction.md#debugger-engine)カーネル モード デバッグの対象のコンピュータにメソッドを使用して[ **AttachKernel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-attachkernel)します。

**注**   、エンジンはまでカーネルに接続することは完全には、 [ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されました。 カーネルは、イベントをなど、生成した後にのみ、[最初のブレークポイント](initial-breakpoint.md)-は、使用可能になるデバッガー セッション側でします。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

接続オプションを使って検索を使用して、ターゲット コンピューターを照会できますデバッガー エンジンがローカル カーネルではないカーネルにアタッチされ、接続が eXDI 接続ではない、 [ **GetKernelConnectionOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getkernelconnectionoptions). 接続が再同期することもできますを使用して、接続速度の変更または[ **SetKernelConnectionOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setkernelconnectionoptions)します。

ローカルのカーネルにデバッガーをアタッチできますで、コンピューターが起動場合にのみ、限定された方法でのみ、 **/debug**ブート スイッチ。 (一部の Windows インストールでローカル カーネル デバッグはサポートされてなどの他のスイッチが使用される場合 **/debugport**が、これは Windows の機能の保証ではありませんに依存する必要があります)。[**IsKernelDebuggerEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-iskerneldebuggerenabled)ローカル コンピューターがデバッグに使用できるか判断するために使用します。 カーネルの詳細については、1 台のコンピューターでのデバッグを参照してください[ローカル カーネル デバッグを実行する](performing-local-kernel-debugging.md)します。

 

 





