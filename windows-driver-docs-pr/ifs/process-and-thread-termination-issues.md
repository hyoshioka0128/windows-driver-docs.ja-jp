---
title: 処理とスレッド終了に関する問題
description: 処理とスレッド終了に関する問題
ms.assetid: 11b38c60-1bd8-4f1b-a80e-14a93e4ac474
keywords:
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティ チェックの WDK ファイル システム、プロセスとスレッドの終了
- プロセスの終了を WDK ファイル システム
- スレッドの終了を WDK ファイル システム
- WDK ファイル システムのプロセスまたはスレッドの終了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d3f917b21439da077cded5461b9b7a01385245
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352766"
---
# <a name="process-and-thread-termination-issues"></a>処理とスレッド終了に関する問題


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


特定のユーザーに関連する状態情報を格納するファイル システムは、プロセスとスレッドの終了条件を監視する必要があります。 たとえば、暗号化キーの特定のユーザーに関連付けられている必要があります、終了時に破棄されます (計画済みまたは途中) かどうかのアプリケーションの特殊なコントロール。 これらの条件を処理するために使用されるルーチンの詳細については、次を参照してください[ **PsSetCreateProcessNotifyRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559951)と[ **PsSetCreateThreadNotifyRoutine。**](https://msdn.microsoft.com/library/windows/hardware/ff559954).

 

 




