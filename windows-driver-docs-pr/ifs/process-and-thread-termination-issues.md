---
title: プロセスとスレッドの終了に関する問題
description: プロセスとスレッドの終了に関する問題
ms.assetid: 11b38c60-1bd8-4f1b-a80e-14a93e4ac474
keywords:
- セキュリティ WDK ファイルシステム、セキュリティチェックの追加
- セキュリティチェック WDK ファイルシステム、プロセスとスレッドの終了
- プロセス終了 WDK ファイルシステム
- スレッド終了 WDK ファイルシステム
- 終了したプロセスまたはスレッドの WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dea17e2a2f4d4218f5ec969dcd32632743d15fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841025"
---
# <a name="process-and-thread-termination-issues"></a>プロセスとスレッドの終了に関する問題


## <span id="ddk_process_and_thread_termination_issues_if"></span><span id="DDK_PROCESS_AND_THREAD_TERMINATION_ISSUES_IF"></span>


特定のユーザーに関連する状態情報を格納するファイルシステムでは、プロセスとスレッド終了の状態を監視する必要がある場合があります。 たとえば、特定のユーザーに関連付けられている暗号化キーは、特殊なコントロールアプリケーションの終了 (予定されているかどうかに関係なく) によって破棄される必要があります。 これらの条件の処理に使用されるルーチンの詳細については、「 [**Pssetcreateprocessnotifyroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine) 」と「 [**Pssetcreateprocessnotifyroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)」を参照してください。

 

 




