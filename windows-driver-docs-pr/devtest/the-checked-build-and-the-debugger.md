---
title: チェック ビルドとデバッガー
description: チェック ビルドとデバッガー
ms.assetid: 851d9b5b-cd1c-4b1e-b3ec-d13645795705
keywords:
- チェック ビルド WDK、デバッガー
- デバッガー WDK ビルドの確認
- ホスト コンピューター WDK ビルドの確認
- ターゲット コンピューター WDK ビルドをチェックします。
- WDK のヌル モデム ケーブル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3012add621ab43728c0d08d55c0b98264b860ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391300"
---
# <a name="the-checked-build-and-the-debugger"></a>チェック ビルドとデバッガー


## <span id="ddk_the_checked_build_and_the_debugger_tools"></span><span id="DDK_THE_CHECKED_BUILD_AND_THE_DEBUGGER_TOOLS"></span>


Windows オペレーティング システムのカーネル モード ドライバーをデバッグするための一般的なセットアップは、ネットワーク、USB、シリアル、または 1394 接続を使用して接続されている 2 台のコンピューターで構成されます。 カーネル モードのデバッグの設定の詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

*ホスト コンピューター*はデバッガーを実行するシステムです。 安定したシステムし、オペレーティング システムの無料のビルドを常に実行する必要があります。

*対象のコンピュータ*はテストするドライバーを実行するシステムです。 無料のビルドまたはチェック ビルドのいずれかで実行できます。 正確なデバッグ チェックのビルドが適しています。

ホスト コンピューターで実行されているデバッガーでは、デバッグ接続経由でターゲット コンピュータを制御します。

 

 





