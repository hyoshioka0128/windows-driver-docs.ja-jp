---
title: 最初のブレークポイント
description: 最初のブレークポイント
ms.assetid: c7fda1f0-bbfb-41d8-b3c9-568f2f0a74e1
keywords:
- 最初のブレークポイント
- ブレークポイント、最初のブレークポイント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393e0bb94aa8788310f944fe99ca8fad747e5094
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580341"
---
# <a name="initial-breakpoint"></a>最初のブレークポイント


デバッガーでは、新しいターゲット アプリケーションを起動するとメイン イメージの後に最初のブレークポイントが自動的が発生し、DLL の初期化ルーチンを呼び出す前に、静的にリンクされているすべての Dll が読み込まれます。

既存のユーザー モード アプリケーション、最初に、デバッガーをアタッチするときに[ブレークポイント](using-breakpoints.md)直後に発生します。

**-G**コマンド ライン オプションは、最初のブレークポイントを無視するには、WinDbg または CDB します。 この時点で自動的にコマンドを実行することができます。 このような状況の詳細については、[を制御する例外とイベント](controlling-exceptions-and-events.md)を参照してください。

新しいターゲットを起動し、実際のアプリケーションの実行が開始するときに、そこに中断する場合は使用しないでください、 **-g**オプション。 代わりに、最初のブレークポイントが発生することができます。 デバッガーがアクティブで後にブレークポイントを設定、**メイン**または**winmain**ルーチンと、次を使用して、 [ **g (移動)** ](g--go-.md)コマンド。 実行し、すべての初期化手順と、メイン アプリケーションの実行が開始するときに、アプリケーションを停止します。

カーネル モードで自動のブレークポイントの詳細については、[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)を参照してください。

 

 





