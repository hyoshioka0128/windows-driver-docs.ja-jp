---
title: ライブのカーネル モードのターゲット
description: ライブのカーネル モードのターゲット
ms.assetid: 88820097-4a47-428d-88dd-d0a08e5debdc
keywords:
- ターゲット、ライブのカーネル モード
- カーネル モードのターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2839190f77adedd030950da670d422b44421ddd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559839"
---
# <a name="live-kernel-mode-targets"></a>ライブのカーネル モードのターゲット


## <span id="ddk_live_kernel_mode_targets_dbx"></span><span id="DDK_LIVE_KERNEL_MODE_TARGETS_DBX"></span>


アタッチする、[デバッガー エンジン](introduction.md#debugger-engine)カーネル モード デバッグの対象のコンピュータにメソッドを使用して[ **AttachKernel**](https://msdn.microsoft.com/library/windows/hardware/ff538145)します。

**注**   、エンジンはまでカーネルに接続することは完全には、 [ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)メソッドが呼び出されました。 カーネルは、イベントをなど、生成した後にのみ、[最初のブレークポイント](initial-breakpoint.md)-は、使用可能になるデバッガー セッション側でします。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

接続オプションを使って検索を使用して、ターゲット コンピューターを照会できますデバッガー エンジンがローカル カーネルではないカーネルにアタッチされ、接続が eXDI 接続ではない、 [ **GetKernelConnectionOptions**](https://msdn.microsoft.com/library/windows/hardware/ff546970). 接続が再同期することもできますを使用して、接続速度の変更または[ **SetKernelConnectionOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556729)します。

ローカルのカーネルにデバッガーをアタッチできますで、コンピューターが起動場合にのみ、限定された方法でのみ、 **/debug**ブート スイッチ。 (一部の Windows インストールでローカル カーネル デバッグはサポートされてなどの他のスイッチが使用される場合 **/debugport**が、これは Windows の機能の保証ではありませんに依存する必要があります)。[**IsKernelDebuggerEnabled** ](https://msdn.microsoft.com/library/windows/hardware/ff551088)ローカル コンピューターがデバッグに使用できるか判断するために使用します。 カーネルの詳細については、1 台のコンピューターでのデバッグを参照してください[ローカル カーネル デバッグを実行する](performing-local-kernel-debugging.md)します。

 

 





