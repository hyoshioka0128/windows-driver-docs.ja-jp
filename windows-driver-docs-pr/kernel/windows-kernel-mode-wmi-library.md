---
title: Windows カーネルモード WMI ライブラリ
description: Windows カーネルモード WMI ライブラリ
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 84d834e8c8efed50820882e959de43ad5e77a662
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580379"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows カーネルモード WMI ライブラリ


Windows では、コンポーネントを管理するための一般的なメカニズムを提供します。 このシステムは、Windows Management Instrumentation (WMI) と呼ばれます。 Windows Driver Model (WDM) の要件を満たしてに、ドライバーは、システムによって管理できるように、ドライバーの WMI を実装する必要があります。

WMI の詳細については、次を参照してください。 [Windows Management Instrumentation](implementing-wmi.md)します。

WMI ライブラリへの直接のインターフェイスを提供するルーチンには、文字のプレフィックス"**Wmi**"WMI のルーチンの一覧を参照してください。 [Windows Management Instrumentation (WMI) ライブラリ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566359)します。

WMI のコールバックの一覧は、次を参照してください。 [WMI ライブラリ コールバック ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566357)します。

WMI との通信は Irp で実行されます。 ドライバーは Irp を受信に使用できるルーチンの一覧は、次を参照してください。 [WMI IRP の処理ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566353)します。 ドライバーを使用して WMI Irp を送信するルーチンの一覧は、次を参照してください。 [WMI IRP を送信するルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566355)します。 WMI で使用される Irp の一覧は、次を参照してください。 [WMI マイナー Irp](https://msdn.microsoft.com/library/windows/hardware/ff566361)します。

 

 




