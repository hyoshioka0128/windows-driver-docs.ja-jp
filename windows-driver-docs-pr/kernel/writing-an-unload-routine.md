---
title: アンロード ルーチンの記述
description: アンロード ルーチンの記述
ms.assetid: 578f3499-28fc-412b-bbb7-75f8023fa7c1
keywords:
- 標準のドライバーのルーチンの WDK カーネル、アンロード ルーチン
- ドライバーのルーチンの WDK カーネル、アンロード ルーチン
- ルーチンの WDK カーネル、アンロード ルーチン
- アンロード ルーチン WDK カーネル
- アンロード ルーチンについて、アンロード ルーチンの WDK カーネル
- ドライバーの置き換え
- ドライバーの置換の WDK カーネル
- アンロード ドライバー
- ドライバー WDK カーネルの再読み込み
- ドライバー アンロード WDK カーネル
- ドライバーの再読み込み WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 814cbfd448b1d7d3de0f731036537a1e807fc73d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573058"
---
# <a name="writing-an-unload-routine"></a>アンロード ルーチンの記述





置換、またはアンロード、およびシステムの実行中の再読み込みが可能な任意のドライバーが必要、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。 WDM ドライバーがすべて必要があります*アンロード*ルーチン。

*アンロード*ルーチンが非 WDM ドライバーでは、省略可能な[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)は用意されていないドライバーの失敗、*アンロード*ルーチン。

このセクションでは、次のトピックについて説明します。

[日常的な環境をアンロードします。](unload-routine-environment.md)

[日常的な機能をアンロードします。](unload-routine-functionality.md)

 

 




