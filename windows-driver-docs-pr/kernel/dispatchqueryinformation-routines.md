---
title: DispatchQueryInformation ルーチン
description: DispatchQueryInformation ルーチン
ms.assetid: dfcb8ad0-ae95-4dd7-b4c8-a2f3ad4b12ef
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchQueryInformation ルーチン
- DispatchQueryInformation ルーチン
- IRP_MJ_QUERY_INFORMATION I/O 関数のコード
- クエリ情報ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccd4b3f0c6c53e852a66a4dac2740d03a0d6524a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384985"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation ルーチン





ドライバーの[ *DispatchQueryInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information) I/O 関数のコード。 この I/O 関数のコードのドライバー サポートのオプションですとに通常表示される上位レベルまたはファイル システム ドライバー。 この要求は、I/O マネージャーとその他のオペレーティング システムのコンポーネントでは、その他のカーネル モード ドライバーによって送信されます。 たとえば、ユーザー モード アプリケーションを呼び出すときに送信される[ **GetFileInformationByHandle**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getfileinformationbyhandle)、カーネル モード コンポーネントを呼び出すと、 [ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile).

 

 




