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
ms.openlocfilehash: 17970f99a883ff1a2488370da303f65e68acf3e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538471"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation ルーチン





ドライバーの[ *DispatchQueryInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_クエリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550788) I/O 関数のコード。 この I/O 関数のコードのドライバー サポートのオプションですとに通常表示される上位レベルまたはファイル システム ドライバー。 この要求は、I/O マネージャーとその他のオペレーティング システムのコンポーネントでは、その他のカーネル モード ドライバーによって送信されます。 たとえば、ユーザー モード アプリケーションを呼び出すときに送信される[ **GetFileInformationByHandle**](https://msdn.microsoft.com/library/windows/desktop/aa364952)、カーネル モード コンポーネントを呼び出すと、 [ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052).

 

 




