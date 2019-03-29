---
title: スプーラー コンポーネントのデバッグ
description: スプーラー コンポーネントのデバッグ
ms.assetid: ed4dcd29-105c-4562-9741-858cb9542449
keywords:
- スプーラー コンポーネントの WDK プリンターのデバッグ
- スプーラー コンポーネントのデバッグ WDK の印刷
- トレース メッセージの WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5a98123f71cbfb90b9473edd7a78086e714383f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580035"
---
# <a name="debugging-spooler-components"></a>スプーラー コンポーネントのデバッグ





このセクションでは、スプーラー コンポーネントのデバッグ メッセージを有効にする方法についての情報を提供します。 このセクションの最初の部分には、スプーラー コンポーネントで使用されるデバッグ変数が一覧表示します。 これらを使用することができますが、スプーラー コンポーネントで生成されたデバッグ メッセージが表示される変数をデバッグします。 (チェックで作業する必要がありますので注意をこれらのコンポーネントの作成) します。

このセクションでは、手順について詳しく説明の 2 番目の部分は、スプーラー コンポーネントにトレース メッセージを表示する必要があります。

**注**  に関する注意事項がある[XPSDrv プリンター ドライバーをデバッグ](debugging-xpsdrv-printer-drivers.md)します。

 

### <a name="displaying-trace-messages-in-a-spooler-component"></a>スプーラー コンポーネントのトレース メッセージを表示します。

次の手順は、winspool.drv のビルドでチェックされたトレース メッセージを表示することができるために必要な手順を示します。 トレース メッセージを表示するための手順では、他のスプーラー コンポーネントと似ています。

トレースを表示するには、スプーラー コンポーネントをメッセージします。

1.  デバッガーをアタッチします。

2.  デバッグするプロセスを分割します。

3.  デバッグの変数、winspool を確認してください。ClientDebug します。

4.  設定、DBG\_winspool の下位ワードのトレース ビット (0x0008)。ClientDebug 変数です。

5.  をクリックします。

 

 




