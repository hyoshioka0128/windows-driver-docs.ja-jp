---
title: DispatchSetInformation ルーチン
description: DispatchSetInformation ルーチン
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchSetInformation ルーチン
- DispatchSetInformation ルーチン
- 情報のディスパッチ ルーチン WDK カーネルを設定します。
- IRP_MJ_SET_INFORMATION I/O 関数のコード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc2bc374abc5ff464a69c18d55b0f9ad5da67ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384969"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation ルーチン





ドライバーの[ *DispatchSetInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_設定\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information) I/O 関数のコード。 この I/O 関数のコードのドライバー サポートのオプションですとに通常表示される上位レベルまたはファイル システム ドライバー。 この要求は、I/O マネージャーとその他のオペレーティング システムのコンポーネントでは、その他のカーネル モード ドライバーによって送信されます。 たとえば、ユーザー モード アプリケーションを呼び出すときに送信される[ **SetEndOfFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-setendoffile)、カーネル モード コンポーネントを呼び出すと、 [ **ZwSetInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile).

 

 




