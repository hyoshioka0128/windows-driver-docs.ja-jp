---
title: DispatchQueryInformation ルーチン
description: DispatchQueryInformation ルーチン
ms.assetid: dfcb8ad0-ae95-4dd7-b4c8-a2f3ad4b12ef
keywords:
- ディスパッチルーチン WDK カーネル、DispatchQueryInformation ルーチン
- DispatchQueryInformation ルーチン
- IRP_MJ_QUERY_INFORMATION i/o 関数のコード
- クエリ情報ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d401c4e61c8c6e840682dc4fa1e847ea87daa02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836842"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation ルーチン





ドライバーの[*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)I/o 関数コードの irp を処理します。 この i/o 関数コードに対するドライバーのサポートは省略可能であり、通常は上位レベルまたはファイルシステムのドライバーで表示されます。 この要求は、i/o マネージャーと他のオペレーティングシステムコンポーネント、およびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが[**GetFileInformationByHandle**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getfileinformationbyhandle)を呼び出し、カーネルモードコンポーネントが[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)を呼び出すときに送信されます。

 

 




