---
title: チェック ビルドとデバッガー
description: チェック ビルドとデバッガー
ms.assetid: 851d9b5b-cd1c-4b1e-b3ec-d13645795705
keywords:
- チェックされたビルド WDK、デバッガー
- デバッガーの WDK チェックビルド
- ホストコンピューターの WDK チェックビルド
- ターゲットコンピューターの WDK チェックビルド
- ヌルモデムケーブル WDK
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 380d20e7bd4c2e4c2be31635f28c0caae4305af3
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428337"
---
# <a name="the-checked-build-and-the-debugger"></a>チェック ビルドとデバッガー

Windows オペレーティングシステムでカーネルモードドライバーをデバッグするための一般的なセットアップは、ネットワーク、USB、またはシリアル接続を使用して接続された2台のコンピューターで構成されています。 カーネルモードデバッグの設定の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

*ホストコンピューター*は、デバッガーが実行されているシステムです。 安定したシステムである必要があり、常にオペレーティングシステムの無償ビルドを実行する必要があります。

*ターゲットコンピューター*は、テスト対象のドライバーが実行されるシステムです。 無料のビルドまたはチェックされたビルドのいずれかを実行できます。 より正確なデバッグを行うには、チェックされたビルドを使用することをお勧めします。

ホストコンピューター上で実行されているデバッガーは、確立したデバッグ接続を介して対象のコンピューターを制御します。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。
