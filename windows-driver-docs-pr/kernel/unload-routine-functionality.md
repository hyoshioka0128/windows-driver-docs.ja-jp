---
title: 日常的な機能をアンロードします。
description: 日常的な機能をアンロードします。
ms.assetid: a36b4687-df1d-498f-b9f3-d13ae2a9a3cd
keywords:
- ルーチンの WDK カーネル、機能をアンロードします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f67e9d6499af2cd412fdf69508b7ce5613267d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557712"
---
# <a name="unload-routine-functionality"></a>日常的な機能をアンロードします。





ドライバーの役割[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンがかどうか、ドライバーが PnP にサポートするかどうかに依存します。

同様、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) PnP ドライバーのルーチンは、通常は単純なそのため、*アンロード*ルーチン、」の説明に従って[A PnP ドライバーのアンロード ルーチン](pnp-driver-s-unload-routine.md).

非 PnP ドライバーの*アンロード*ルーチンのデバイス オブジェクトの解放し、ドライバーに割り当てられたリソースを解放する必要があります。 それに対応するによって実行される作業を取り消す必要があります、 **DriverEntry**と[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)ドライバー、そのデバイスとそのリソースの初期化ルーチン。 参照してください[A 非 PnP ドライバーのアンロードに日常的な](non-pnp-driver-s-unload-routine.md)詳細についてはします。

 

 




