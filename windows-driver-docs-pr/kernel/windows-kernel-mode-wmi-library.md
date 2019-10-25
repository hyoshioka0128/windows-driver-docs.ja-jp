---
title: Windows カーネルモード WMI ライブラリ
description: Windows カーネルモード WMI ライブラリ
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15c18e44e863edae920f1aad230e3a6dfd657732
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838305"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows カーネルモード WMI ライブラリ


Windows には、コンポーネントを管理するための一般的なメカニズムが用意されています。 このシステムは Windows Management Instrumentation (WMI) と呼ばれます。 Satisify Windows Driver Model (WDM) の要件を満たすには、ドライバーをシステムで管理できるように、ドライバーの WMI を実装する必要があります。

WMI の詳細については、「 [Windows Management Instrumentation](implementing-wmi.md)」を参照してください。

WMI ライブラリへの直接インターフェイスを提供するルーチンには、"**wmi**" という文字がプレフィックスとして付けられます。WMI ルーチンの一覧については、「 [Windows Management Instrumentation (wmi) ライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

WMI コールバックの一覧については、「 [Wmi Library Callback ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

WMI との通信は、Irp を使用して行われます。 ドライバーが Irp を受信するために使用できるルーチンの一覧については、「 [WMI IRP Processing ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 ドライバーが WMI Irp の送信に使用できるルーチンの一覧については、「 [WMI Irp 送信ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 WMI で使用される Irp の一覧については、「 [Wmi Minor irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)」を参照してください。

 

 




