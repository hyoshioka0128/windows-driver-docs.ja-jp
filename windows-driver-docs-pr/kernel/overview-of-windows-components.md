---
title: Windows コンポーネントの概要
description: Windows コンポーネントの概要
ms.assetid: b941197d-732c-4b9a-8367-46beb14c33cf
keywords:
- Windows コンポーネント WDK
- Windows NT コンポーネント WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44537db010e89498573f4ec73b061fe0e40a4efb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383815"
---
# <a name="overview-of-windows-components"></a>Windows コンポーネントの概要





次の図は、Windows オペレーティング システムの主要な内部コンポーネントを示しています。

![windows コンポーネントの概要を示す図](images/ntarch.png)

図に示すように、Windows オペレーティング システムには、ユーザー モードとカーネル モードの両方のコンポーネントが含まれています。 Windows ユーザーおよびカーネル モードの詳細については、次を参照してください。[ユーザー モードとカーネル モード](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)します。

ドライバーは、さまざまなカーネル コンポーネントによってエクスポートされるルーチンを呼び出します。 たとえば、デバイス オブジェクトを作成するにを呼び出す、 [ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice) I/O マネージャーがエクスポートしたルーチン。 ドライバーを呼び出すことができるルーチンをカーネル モードの一覧は、次を参照してください。[ドライバー サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

さらに、ドライバーはオペレーティング システムからの特定の呼び出しに応答する必要があります、その他のシステム呼び出しに応答できます。 ドライバーがサポートする必要があるカーネル モードのルーチンの一覧は、次を参照してください。[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)します。

上の図では、すべてのカーネル モード コンポーネントが含まれています。 カーネル モード コンポーネントの一覧は、次を参照してください。[カーネル モードの管理者とライブラリ](kernel-mode-managers-and-libraries.md)します。

 

 




