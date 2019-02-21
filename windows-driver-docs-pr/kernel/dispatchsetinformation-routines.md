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
ms.openlocfilehash: f259e0b3bf2e743bcaa3b87115d436e4e00e2a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551738"
---
# <a name="dispatchsetinformation-routines"></a>DispatchSetInformation ルーチン





ドライバーの[ *DispatchSetInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_設定\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff550799) I/O 関数のコード。 この I/O 関数のコードのドライバー サポートのオプションですとに通常表示される上位レベルまたはファイル システム ドライバー。 この要求は、I/O マネージャーとその他のオペレーティング システムのコンポーネントでは、その他のカーネル モード ドライバーによって送信されます。 たとえば、ユーザー モード アプリケーションを呼び出すときに送信される[ **SetEndOfFile**](https://msdn.microsoft.com/library/windows/desktop/aa365531)、カーネル モード コンポーネントを呼び出すと、 [ **ZwSetInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567096).

 

 




