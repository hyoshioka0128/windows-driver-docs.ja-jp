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
ms.openlocfilehash: 62be0a7598133680490c9435e564d72a52c30deb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360930"
---
# <a name="the-checked-build-and-the-debugger"></a>チェック ビルドとデバッガー


## <span id="ddk_the_checked_build_and_the_debugger_tools"></span><span id="DDK_THE_CHECKED_BUILD_AND_THE_DEBUGGER_TOOLS"></span>


Windows オペレーティング システムのカーネル モード ドライバーをデバッグするための一般的なセットアップは、ネットワーク、USB、シリアル、または 1394 接続を使用して接続されている 2 台のコンピューターで構成されます。 カーネル モードのデバッグの設定の詳細については、次を参照してください。 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。

*ホスト コンピューター*はデバッガーを実行するシステムです。 安定したシステムし、オペレーティング システムの無料のビルドを常に実行する必要があります。

*対象のコンピュータ*はテストするドライバーを実行するシステムです。 無料のビルドまたはチェック ビルドのいずれかで実行できます。 正確なデバッグ チェックのビルドが適しています。

ホスト コンピューターで実行されているデバッガーでは、デバッグ接続経由でターゲット コンピュータを制御します。

 

 





