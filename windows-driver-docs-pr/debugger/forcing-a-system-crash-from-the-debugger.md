---
title: デバッガーから強制的にシステムのクラッシュ
description: デバッガーから強制的にシステムのクラッシュ
ms.assetid: 7d7d9b07-00a3-4f87-8eb9-01b3f2fa312f
keywords:
- デバッガーの原因と、システムのクラッシュ
- デバッガーからのバグ チェック
- デバッガーから強制的にシステムのクラッシュ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6cb6b4a90323a247a652f8f6b4c1567206f68a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549563"
---
# <a name="forcing-a-system-crash-from-the-debugger"></a>デバッガーから強制的にシステムのクラッシュ


## <span id="ddk_forcing_a_system_crash_from_the_debugger_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_DEBUGGER_DBG"></span>


KD または WinDbg には、カーネル モードのデバッグが実行して、システムのクラッシュが発生するを強制的にできます。 これは、入力することで、 [ **(システムがクラッシュする Force) .crash** ](-crash--force-system-crash-.md)コマンド プロンプトでコマンド。 (対象のコンピューターがすぐにクラッシュしない場合、これをに従って、 [ **g (移動)** ](g--go-.md)コマンド)。

このコマンドが発行されると、システムが呼び出さ**KeBugCheck**と問題[**バグ チェック 0 xe2** ](bug-check-0xe2--manually-initiated-crash.md) (手動で\_INITIATED\_クラッシュ)。 クラッシュ ダンプを無効になっている場合を除き、この時点で、クラッシュ ダンプ ファイルが書き込まれます。

クラッシュ ダンプ ファイルが書き込まれると、カーネル デバッガー ホスト コンピューターでは警告が表示され、クラッシュしたターゲットを積極的にデバッグするために使用できます。

 

 





