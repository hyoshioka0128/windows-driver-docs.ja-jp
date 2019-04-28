---
title: プロトコル ドライバーのページ可能で破棄可能なコード
description: プロトコル ドライバーのページ可能で破棄可能なコード
ms.assetid: acc27690-cdc3-433c-85c4-489501ea3d26
keywords:
- プロトコル ドライバー WDK のネットワーク、ページング、および破棄できるコード
- NDIS プロトコル ドライバー WDK、ページングと破棄コード
- ページングと破棄コード WDK NDIS プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6c661ccc3942785b1ae9c4c5a0336f7f654cb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376250"
---
# <a name="pageable-and-discardable-code-in-a-protocol-driver"></a>プロトコル ドライバーのページ可能で破棄可能なコード





ドライバー開発者向けがコードとして指定可能であれば、ページング可能なメモリ常駐型にする必要があるコードのシステム領域を解放します。 ページング可能として関数をマークすることができます、 [ **NDIS\_PAGEABLE\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff557121)マクロ。 ページングの中からは、IRQL、リソースの管理機能、および関数の他の特性は、関数は、禁止する可能性があります。

すべて*ProtocolXxx*パッシブから範囲の IRQL で関数が実行される\_レベル ディスパッチを\_レベル。 IRQL でのみ実行される関数 = パッシブ\_レベルは、ページング可能としてマークする必要があります。

IRQL で実行されるドライバー関数 = パッシブ\_レベルにできるページング可能な限り、呼び出すことも、IRQL で実行されている任意の関数によって呼び出される&gt;= ディスパッチ\_レベル--スピン ロックを取得する関数などです。 取得のスレッドの IRQL をディスパッチするときに生成されるスピン ロックを取得すると、\_レベル。 などのドライバー関数[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)、IRQL で実行される = パッシブ\_レベルでは、呼び出す必要がありますいない**Ndis * Xxx*** IRQLで実行される関数&gt;= ディスパッチ\_レベルのドライバー関数がページング可能なコードとしてマークされている場合。 それぞれの IRQL の詳細については**Ndis * Xxx*** 関数を参照してください[NDIS ライブラリ関数](https://msdn.microsoft.com/library/windows/hardware/ff557039)します。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数からのみ呼び出されるコードと同様に、NDIS プロトコル ドライバーの**DriverEntry**を使用して、コードの初期化専用として指定する必要があります[ **NDIS\_INIT\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff557007)マクロ。 このマクロで識別されるコードでは、システムの初期化時に 1 回だけ実行すると見なされます、その結果、その時間中にのみマップされます。 初期化のみを返します。 としてマークされた関数後は、破棄されます。

 

 





