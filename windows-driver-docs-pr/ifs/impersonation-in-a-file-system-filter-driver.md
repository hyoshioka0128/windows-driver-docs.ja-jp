---
title: ファイル システム フィルター ドライバーでの偽装
description: ファイル システム フィルター ドライバーでの偽装
ms.assetid: ee56cd54-01ac-46ad-8ee4-e76131b058f3
keywords:
- セキュリティ WDK ファイルシステム、偽装
- 権限借用 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5432cd537ba355f37964a413581b2efdedd84d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841208"
---
# <a name="impersonation-in-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーでの偽装


## <span id="ddk_impersonation_in_a_file_system_filter_driver_if"></span><span id="DDK_IMPERSONATION_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


ファイルシステムフィルタードライバーが使用しようとしている可能性のある別の操作は、偽装です。 偽装は、他のスレッドの代わりにセキュリティを処理するための非常に強力な手法ですが、コンポーネントの代わりに使用するための適切な注意も必要です。 ファイルシステムフィルタードライバーの場合は、偽装を使用して実行する必要がある操作を識別することが重要です。 次に、ファイルシステムフィルタードライバーによって実行される他の操作を、偽装を使用して実行しないようにする必要があります。 偽装のリスクは、通常、呼び出し元のドライバーよりも呼び出し元の特権が低いことを示します。 したがって、偽装を使用して呼び出しが行われた場合、偽装を行わずに成功する可能性がありますが、失敗する可能性があります。

ハンドルはオブジェクトへの参照を表し、セキュリティチェックが実行されたポイントであるため、新しいハンドルを作成するすべての操作には偽装が必要です。 たとえば、ファイルまたは他のオブジェクト ( [**Zw/** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection) [**zwcreateevent、Zwcreateevent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)など) を開くときには偽装が必要になります。 これらの呼び出しでは、これらを呼び出すフィルタードライバーが、渡されたパラメーターが有効であることを確認する必要があります。これは、他のオペレーティングシステム操作では、カーネルモードからの呼び出しに有効なパラメーターがあると想定されるためです。 したがって、フィルタードライバーは、偽装している場合でも、これらの関数のいずれかにユーザーバッファーアドレスを安全に渡すことができません。

[**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)の場合は、対応する i/o Manager 呼び出し[**iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)を使用する必要があります。これは、フィルタードライバーが IO\_指定して\_アクセス\_チェックを強制することができるためです。 このオプションを指定しないと、i/o マネージャーは適切なユーザーレベルのアクセスチェックを強制しません。

 

 




