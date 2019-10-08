---
title: Windows コンポーネントの概要
description: Windows コンポーネントの概要
ms.assetid: b941197d-732c-4b9a-8367-46beb14c33cf
keywords:
- Windows コンポーネント WDK
- Windows NT コンポーネント WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 0c295794930137c214ade9871d61781c197fedfa
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007628"
---
# <a name="overview-of-windows-components"></a>Windows コンポーネントの概要





次の図は、Windows オペレーティングシステムの主要な内部コンポーネントを示しています。

![windows コンポーネントの概要を示す図](images/ntarch.png)

図に示すように、Windows オペレーティングシステムには、ユーザーモードとカーネルモードの両方のコンポーネントが含まれています。 Windows ユーザーモードとカーネルモードの詳細については、「[ユーザーモードとカーネルモード](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode)」を参照してください。

ドライバーは、さまざまなカーネルコンポーネントによってエクスポートされるルーチンを呼び出します。 たとえば、デバイスオブジェクトを作成するには、i/o マネージャーによってエクスポートされる[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)ルーチンを呼び出します。 ドライバーが呼び出すことができるカーネルモードルーチンの一覧については、「[ドライバーサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)」を参照してください。

また、ドライバーはオペレーティングシステムからの特定の呼び出しに応答し、他のシステムコールに応答できる必要があります。 ドライバーがサポートする必要があるカーネルモードルーチンの一覧については、「[標準ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)」を参照してください。

すべてのカーネルモードコンポーネントが上の図に示されているわけではありません。 カーネルモードコンポーネントの一覧については、「[カーネルモードマネージャーとライブラリ](kernel-mode-managers-and-libraries.md)」を参照してください。

 

 




