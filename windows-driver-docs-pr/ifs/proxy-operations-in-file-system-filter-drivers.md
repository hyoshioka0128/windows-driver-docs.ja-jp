---
title: ファイル システム フィルター ドライバーでのプロキシ操作
description: ファイル システム フィルター ドライバーでのプロキシ操作
ms.assetid: 01cc7a48-8b27-4de7-8968-8958e9512989
keywords:
- セキュリティの WDK ファイル システム、プロキシの操作
- プロキシ操作 WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 740894dc3a3bf2e0103175f177868ee3ccf61627
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385147"
---
# <a name="proxy-operations-in-file-system-filter-drivers"></a>ファイル システム フィルター ドライバーでのプロキシ操作


## <span id="ddk_proxy_operations_in_file_system_filter_drivers_if"></span><span id="DDK_PROXY_OPERATIONS_IN_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


ファイル システム フィルター ドライバーは、頻繁に (ユーザー モード) の最初の呼び出し元の代わりに操作を実行する必要があります。 これを行うときに、ファイル システム フィルター ドライバーが、元のユーザーがない可能性のあるアクションを要する可能性がある操作を実行する必要があります。 たとえば、ユーザーがファイルのファイルを開くしようとする\_優先的します。 フィルター ドライバーを同じの種類を使用してアクセスを指定するファイルを開くことはできません試みます[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)、たとえば、ため、ユーザーが、ファイルを置き換えるためのアクセス許可を持っていない場合でも、ファイル システム フィルター ドライバーによって実行されるときに、操作は成功します。

ファイル システム フィルター ドライバーがこのような問題を生じるかもしれない方法は多数あります。 ファイル システム フィルター ドライバーは、ユーザーの操作の結果を知ることがなく、基になるファイル システムで操作を実行いつでも実行することができます。 ファイル システム フィルター ドライバーする必要があります、したがってこのようなケースを特定し、操作の結果と判断されたか、または実際のユーザーの操作でエラーから復旧するためのメカニズムがあることを確認します。 たとえばの場合は、ファイルの置き換えの要求、フィルター ドライバー必要がありますを使用して、元の呼び出し元に代わってファイルを開く[ **IoCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)ファイルに対するセキュリティ権限を示すを優先的操作のための十分なとなります。 フィルター ドライバー、IO を使用する場合\_FORCE\_アクセス\_チェック オプション、たとえば、セキュリティ チェックが行います、現在のスレッドの資格情報でカーネル ドライバーからの呼び出しがもできます。

ドライバーがの代理として、またはの結果として、操作を実行するインスタンスを識別するには、ファイル システム フィルター ドライバーに不可欠な一部のユーザー レベルで操作します。 このような場合は、正常に動作させる方法に関する明確な戦略を識別する必要があります。

 

 




