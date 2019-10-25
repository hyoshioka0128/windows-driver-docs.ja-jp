---
title: アンロード ルーチンの記述
description: アンロード ルーチンの記述
ms.assetid: 578f3499-28fc-412b-bbb7-75f8023fa7c1
keywords:
- 標準ドライバールーチン WDK カーネル、アンロードルーチン
- ドライバールーチン WDK カーネル、アンロードルーチン
- ルーチン WDK カーネル、アンロードルーチン
- アンロードルーチン WDK カーネル
- アンロードルーチン WDK カーネル、アンロードルーチンについて
- ドライバーの置換
- WDK カーネルのドライバーの置き換え
- ドライバーのアンロード
- ドライバーの再読み込み WDK カーネル
- WDK カーネルのドライバーのアンロード
- ドライバーの再読み込み WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 289c7ed0c67ac74329eb9db8fd20d182a979e5b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838289"
---
# <a name="writing-an-unload-routine"></a>アンロード ルーチンの記述





システムの実行中に置き換える、またはアンロードおよび再読み込みが可能なすべてのドライバーは、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンが必要です。 すべての WDM ドライバーには、*アンロード*ルーチンが必要です。

*アンロード*ルーチンは、WDM 以外のドライバーに対しては省略可能ですが、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)は、*アンロード*ルーチンを提供しないすべてのドライバーに対して失敗します。

このセクションでは、次のトピックについて説明します。

[ルーチン環境のアンロード](unload-routine-environment.md)

[アンロードのルーチン機能](unload-routine-functionality.md)

 

 




