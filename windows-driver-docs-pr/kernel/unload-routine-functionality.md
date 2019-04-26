---
title: アンロード ルーチンの機能
description: アンロード ルーチンの機能
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- ルーチンの WDK カーネル、機能をアンロードします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f67e9d6499af2cd412fdf69508b7ce5613267d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355285"
---
# <a name="unload-routine-functionality"></a>アンロード ルーチンの機能





ドライバーの役割[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンがかどうか、ドライバーが PnP にサポートするかどうかに依存します。

同様、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) PnP ドライバーのルーチンは、通常は単純なそのため、*アンロード*ルーチン、」の説明に従って[A PnP ドライバーのアンロード ルーチン](pnp-driver-s-unload-routine.md).

非 PnP ドライバーの*アンロード*ルーチンのデバイス オブジェクトの解放し、ドライバーに割り当てられたリソースを解放する必要があります。 それに対応するによって実行される作業を取り消す必要があります、 **DriverEntry**と[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)ドライバー、そのデバイスとそのリソースの初期化ルーチン。 参照してください[A 非 PnP ドライバーのアンロードに日常的な](non-pnp-driver-s-unload-routine.md)詳細についてはします。

 

 




