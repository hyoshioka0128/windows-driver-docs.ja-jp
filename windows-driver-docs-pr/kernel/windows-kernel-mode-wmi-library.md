---
title: Windows カーネルモード WMI ライブラリ
description: Windows カーネルモード WMI ライブラリ
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2bf108c1d64111182cdac53760f6d3a578163030
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386869"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows カーネルモード WMI ライブラリ


Windows では、コンポーネントを管理するための一般的なメカニズムを提供します。 このシステムは、Windows Management Instrumentation (WMI) と呼ばれます。 Windows Driver Model (WDM) の要件を満たしてに、ドライバーは、システムによって管理できるように、ドライバーの WMI を実装する必要があります。

WMI の詳細については、次を参照してください。 [Windows Management Instrumentation](implementing-wmi.md)します。

WMI ライブラリへの直接のインターフェイスを提供するルーチンには、文字のプレフィックス"**Wmi**"WMI のルーチンの一覧を参照してください。 [Windows Management Instrumentation (WMI) ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

WMI のコールバックの一覧は、次を参照してください。 [WMI ライブラリ コールバック ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

WMI との通信は Irp で実行されます。 ドライバーは Irp を受信に使用できるルーチンの一覧は、次を参照してください。 [WMI IRP の処理ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 ドライバーを使用して WMI Irp を送信するルーチンの一覧は、次を参照してください。 [WMI IRP を送信するルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 WMI で使用される Irp の一覧は、次を参照してください。 [WMI マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)します。

 

 




