---
title: ファイル システム フィルター ドライバーでのプロキシ操作
description: ファイル システム フィルター ドライバーでのプロキシ操作
ms.assetid: 01cc7a48-8b27-4de7-8968-8958e9512989
keywords:
- セキュリティ WDK ファイルシステム、プロキシ操作
- プロキシ操作 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c735bc1af7b9ff8732ec20e7d933fd42abb64b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841018"
---
# <a name="proxy-operations-in-file-system-filter-drivers"></a>ファイル システム フィルター ドライバーでのプロキシ操作


## <span id="ddk_proxy_operations_in_file_system_filter_drivers_if"></span><span id="DDK_PROXY_OPERATIONS_IN_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


ファイルシステムフィルタードライバーは、元の (ユーザーモード) 呼び出し元に代わって操作を頻繁に実行する必要があります。 この場合、ファイルシステムフィルタードライバーは、元のユーザーが操作できなかった操作を実行しないようにする必要があります。 たとえば、ユーザーがファイル\_置き換えるファイルを開こうとしたとします。 フィルタードライバーは、 [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を使用して同じ種類のアクセスを指定するファイルを開こうとすることはできません。たとえば、ユーザーがファイルを置き換えるアクセス許可を持っていない場合でも、ファイルシステムによって実行される操作は成功します。フィルタードライバー。

ファイルシステムフィルタードライバーによってこのような問題が発生する可能性がある方法は多数あります。 ファイルシステムフィルタードライバーが、ユーザーの操作の結果を知らなくても、基になるファイルシステムに対して操作を実行するたびに発生する可能性があります。 そのため、ファイルシステムフィルタードライバーは、このようなケースを特定し、操作の結果を判断したか、または実際のユーザー操作でエラーから復旧するためのメカニズムを備えている必要があります。 たとえば、ファイルを置き換える要求の場合、フィルタードライバーは、置き換え操作に十分なファイルのセキュリティ権限を示す[**Iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)を使用して、元の呼び出し元の代わりにファイルを開く必要があります。 フィルタードライバーが IO\_使用する場合は、\_アクセス\_チェックオプションを使用します。たとえば、カーネルドライバーからの呼び出しであっても、現在のスレッドの資格情報でセキュリティチェックが行われます。

ファイルシステムフィルタードライバーは、ユーザーレベルの操作によって、またはその結果として、ドライバーが操作を実行しているインスタンスを識別するために不可欠です。 このような場合は、適切な操作を確実に識別する方法を明確にする方法があります。

 

 




