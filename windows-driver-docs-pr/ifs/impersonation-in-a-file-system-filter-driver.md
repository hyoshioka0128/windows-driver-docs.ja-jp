---
title: ファイル システム フィルター ドライバーでの偽装
description: ファイル システム フィルター ドライバーでの偽装
ms.assetid: ee56cd54-01ac-46ad-8ee4-e76131b058f3
keywords:
- セキュリティの WDK ファイル システム、権限借用
- 権限借用 WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13eaab1da6e87e96f0641c2917eaa72a247279d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375704"
---
# <a name="impersonation-in-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーでの偽装


## <span id="ddk_impersonation_in_a_file_system_filter_driver_if"></span><span id="DDK_IMPERSONATION_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


ファイル システム フィルター ドライバーは可能性がありますを使用しようとします。 別の操作では、偽装があります。 権限借用には、他のスレッドの代わりのセキュリティを処理するための非常に強力な手法が、これも注意が必要です適切な任意のコンポーネントの代わりに使用するためです。 ファイル システム フィルター ドライバーでは、実行する必要のある操作を識別するために重要な権限借用を使用します。 重要なため、ファイル システム フィルター ドライバーによって実行されるその他の操作を実行しない必要がありますが、権限借用を使用します。 権限借用でリスクとは通常、呼び出し元が、呼び出しを行うドライバーよりも少ない権限を持っています。 そのため、権限借用で呼び出しが行われた場合、可能性があります失敗、偽装を使用しないことに成功します。

ハンドル オブジェクトへの参照を表すポイントして、セキュリティ チェックが実行されているために、新しいハンドルを作成する操作の偽装が必要です。 たとえば、偽装は、必要なファイルまたはその他のオブジェクトを開くときに (を使用して[ **ZwCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection)、 [ **ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)と[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)など)。 これらの呼び出しで、それらを呼び出すフィルター ドライバーは必ず他のオペレーティング システムの操作では、カーネル モードから発信された通話は有効なパラメーターがあると想定されますので、渡されるパラメーターが有効であることを確認する必要があります。 そのため、フィルター ドライバーを渡すことはできません安全にユーザー バッファーのアドレス、これらの関数のいずれかに偽装するときにします。

場合に[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)、対応する I/O マネージャー呼び出しがある[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)で使用する必要があります。権限借用 IO を指定するフィルター ドライバーを許容するため\_FORCE\_アクセス\_を確認します。 このオプションは、存在しない I/O マネージャーに適切なユーザー レベルのアクセス確認は適用されません。

 

 




