---
title: ライブ カーネルモード ターゲット
description: ライブ カーネルモード ターゲット
ms.assetid: 88820097-4a47-428d-88dd-d0a08e5debdc
keywords:
- ターゲット、ライブカーネルモード
- カーネルモードターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d765dbe82db160c29044ebcc4747dbd970d565f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826354"
---
# <a name="live-kernel-mode-targets"></a>ライブ カーネルモード ターゲット


## <span id="ddk_live_kernel_mode_targets_dbx"></span><span id="DDK_LIVE_KERNEL_MODE_TARGETS_DBX"></span>


カーネルモードのデバッグ用に[デバッガーエンジン](introduction.md#debugger-engine)を対象のコンピューターにアタッチするには、 [**attachkernel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachkernel)メソッドを使用します。

[**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されるまで、エンジンはカーネルに完全にアタッチされない   に**注意**してください。 カーネルによってイベント ([最初のブレークポイント](initial-breakpoint.md)など) が生成された後にのみ、デバッガーセッションで使用できるようになります。 詳細については[、「デバッグセッションと実行モデル](debugging-session-and-execution-model.md)」を参照してください。

 

デバッガーエンジンがローカルカーネルではないカーネルにアタッチされていて、接続が eXDI 接続ではない場合、ターゲットコンピューターの検索に使用される接続オプションは、 [**Getkernel Connectionoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getkernelconnectionoptions)を使用して照会できます。 また、接続を再同期することも、 [**Setカーネル Connectionoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setkernelconnectionoptions)を使用して接続速度を変更することもできます。

デバッガーはローカルカーネルにアタッチできますが、コンピューターが **/debug**ブートスイッチで起動された場合にのみ、制限付きの方法で接続できます。 (一部の Windows インストールでは、 **/debugport**などの他のスイッチが使用されている場合、ローカルカーネルデバッグはサポートされていますが、これは Windows の保証された機能ではなく、依存することはできません)。[**Isデバッガデバッガーが有効になって**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-iskerneldebuggerenabled)いるのは、ローカルコンピューターがデバッグに使用できるかどうかを判断するためです。 1台のコンピューターでのカーネルデバッグの詳細については、「[ローカルカーネルデバッグの実行](performing-local-kernel-debugging.md)」を参照してください。

 

 





