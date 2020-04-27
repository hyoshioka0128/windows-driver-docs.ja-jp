---
title: Windows コンポーネントの概要
description: Windows コンポーネントの概要
ms.assetid: b941197d-732c-4b9a-8367-46beb14c33cf
keywords:
- Windows コンポーネント WDK
- Windows NT コンポーネント WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: a00ba3404db010c505007d32d0d243dacbcc42f8
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72827716"
---
# <a name="overview-of-windows-components"></a>Windows コンポーネントの概要





次の図は、Windows オペレーティングシステムの主要な内部コンポーネントを示しています。

![Windows コンポーネントの概要を示す図](images/ntarch.png)

図に示すように、Windows オペレーティングシステムには、ユーザー モードとカーネル モードの両方のコンポーネントが含まれています。 Windows のユーザー モードとカーネル モードについて詳しくは、「[ユーザー モードとカーネル モード](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)」を参照してください。

ドライバーにより、さまざまなカーネル コンポーネントによってエクスポートされるルーチンが呼び出されます。 たとえば、デバイス オブジェクトを作成するには、I/O マネージャーによってエクスポートされる [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) ルーチンを呼び出します。 ドライバーが呼び出すことのできるカーネル モードのルーチンの一覧については、[ドライバー サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に関する記事を参照してください。

また、ドライバーはオペレーティング システムからの特定の呼び出しに応答し、他のシステム コールに応答できる必要があります。 ドライバーによってサポートする必要があるカーネル モード ルーチンの一覧については、[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)に関する記事を参照してください。

すべてのカーネル モードのコンポーネントが上の図に示されているわけではありません。 カーネル モード コンポーネントの一覧については、「[カーネル モードのマネージャーとライブラリ](kernel-mode-managers-and-libraries.md)」を参照してください。

 

 




