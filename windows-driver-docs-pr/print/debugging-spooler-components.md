---
title: スプーラー コンポーネントのデバッグ
description: スプーラー コンポーネントのデバッグ
ms.assetid: ed4dcd29-105c-4562-9741-858cb9542449
keywords:
- スプーラコンポーネントのデバッグ (WDK プリンター)
- スプーラコンポーネントのデバッグ WDK 印刷
- トレースメッセージ WDK プリンター
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 301a9d630f316f345e1c93614fc6be795fd11805
ms.sourcegitcommit: 0a0b75d93130b6c5854279607cd0aac099f65fd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428307"
---
# <a name="debugging-spooler-components"></a>スプーラー コンポーネントのデバッグ

ここでは、スプーラコンポーネントでデバッグメッセージを有効にする方法について説明します。 このセクションの最初の部分では、スプーラコンポーネントで使用されるデバッグ変数を示します。 これらのデバッグ変数を使用すると、スプーラコンポーネントから生成されたデバッグメッセージを表示することができます。 これらのコンポーネントのチェックされたビルドを使用する必要があることに注意してください。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

このセクションの後半では、スプーラコンポーネントにトレースメッセージを表示するために必要な手順について詳しく説明します。

> [!NOTE]
> [XPSDrv プリンタードライバーのデバッグ](debugging-xpsdrv-printer-drivers.md)には、特別な考慮事項があります。

## <a name="displaying-trace-messages-in-a-spooler-component"></a>スプーラコンポーネントでのトレースメッセージの表示

次の手順は、winspool のチェックされたビルドでトレースメッセージを表示するために必要な手順を示しています。 トレースメッセージを表示する手順は、他のスプーラコンポーネントにも似ています。

スプーラコンポーネントにトレースメッセージを表示するには、次のようにします。

1. デバッガーをアタッチします。

1. デバッグするプロセスを中断します。

1. デバッグ変数である winspool を見つけます。ClientDebug。

1. \_Winspool の下位ワードで DBG トレースビット (0x0008) を設定します。ClientDebug 変数。

1. [実行] をクリックします。
