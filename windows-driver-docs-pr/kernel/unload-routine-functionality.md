---
title: アンロード ルーチンの機能
description: アンロード ルーチンの機能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- ルーチンの WDK カーネル、機能をアンロードします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fcaa08f6446af35f7ce40b1b70f900c2c94265a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382931"
---
# <a name="unload-routine-functionality"></a>アンロード ルーチンの機能





ドライバーの役割[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンがかどうか、ドライバーが PnP にサポートするかどうかに依存します。

同様、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize) PnP ドライバーのルーチンは、通常は単純なそのため、*アンロード*ルーチン、」の説明に従って[A PnP ドライバーのアンロード ルーチン](pnp-driver-s-unload-routine.md).

非 PnP ドライバーの*アンロード*ルーチンのデバイス オブジェクトの解放し、ドライバーに割り当てられたリソースを解放する必要があります。 それに対応するによって実行される作業を取り消す必要があります、 **DriverEntry**と[*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)ドライバー、そのデバイスとそのリソースの初期化ルーチン。 参照してください[A 非 PnP ドライバーのアンロードに日常的な](non-pnp-driver-s-unload-routine.md)詳細についてはします。

 

 




