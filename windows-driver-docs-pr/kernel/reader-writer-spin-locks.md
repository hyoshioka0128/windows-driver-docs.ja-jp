---
title: 読み取り/書き込みスピン ロック
description: Windows Vista Service Pack 1 (SP1)、関連するルーチンのセットで、リーダーとライターによって共有されるデータ構造体への同期アクセスをサポートするために、スピン ロックを使用を開始します。
ms.assetid: E2853F35-590E-4EF5-8647-1261BC4B8D15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9da891fc77c5a1f3a4bd17b36936cf2c9eab7035
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570775"
---
# <a name="readerwriter-spin-locks"></a>読み取り/書き込みスピン ロック


Windows Vista Service Pack 1 (SP1)、関連するルーチンのセットで、リーダーとライターによって共有されるデータ構造体への同期アクセスをサポートするために、スピン ロックを使用を開始します。 データ構造に対する読み取りアクセスだけを必要とするスレッドは、この構造体を他のリーダー スレッドと共有するのに、スピン ロックを使用できます。 共有データ構造を記述する必要があるスレッドは、スピン ロックを使用して、この構造体に書き込むことができる前に、データ構造体への排他アクセスを入手する必要があります。

リーダー スレッドが共有のアクセスのスピン ロックを取得する必要があるライター スレッドで、ロックが既に保持の排他アクセスの場合は、リーダーをライター ロックを解除する最初待つ必要があります。 同様に、ライター スレッドがへの排他アクセス、スピン ロックを取得する必要があるあり、1 つまたは複数のリーダー スレッドによる共有アクセスのため、ロックが保持既に場合、は、ライター スレッドがロックを解除するこれらのリーダー スレッドのすべての待機する必要があります。 ライターが待機中に新しいリーダー スレッド ロックを取得できるありません。 代わりに、待機している、ライター ロックを取得する必要があるリーダーはライターを取得およびロックの解放によって最初待つ必要があります。

スレッドは、リーダーとライターの間でのロールを切り替えることができます。 既に共有アクセス用のスピン ロックを保持しているスレッドは、スピン ロックのアクセス モードを共有モードから排他モードに変換しようとすることができます。 リーダーがない共有のアクセスのスピン ロックを保持既に、排他アクセスのスピン ロックの取得を既に待機しているライターがない場合、この試行が成功します。

スピン ロックの再帰的な取得は、デッドロックが発生しては許可されていません。

次に Windows Vista SP1 以降の読み取り/書き込みスピン ロックの管理に使用可能なルーチンの一覧を示します。

| ルーチンの名前                                                                                | 説明                                                                                                           |
|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**ExAcquireSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451007)                         | 呼び出し元、排他アクセスのスピン ロックを取得し、ディスパッチに指示\_レベル。                      |
| [**ExAcquireSpinLockExclusiveAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451009)    | IRQL で既に実行されている呼び出し元によって排他的にスピン ロック&gt;= ディスパッチ\_レベル。          |
| [**ExAcquireSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451053)                               | 共有のアクセス、呼び出し元のスピン ロックを取得し、ディスパッチする指示\_レベル。                         |
| [**ExAcquireSpinLockSharedAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451055)           | IRQL で既に実行されている呼び出し元による共有アクセス スピン ロック&gt;= ディスパッチ\_レベル。             |
| [**ExReleaseSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451061)                        | 呼び出し元がへの排他アクセスを取得し、元の IRQL が復元は、スピン ロックを解放します。                   |
| [**ExReleaseSpinLockExclusiveFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451058) | 呼び出し元がへの排他アクセスを取得し、IRQL が低下しないスピン ロックを解放します。                      |
| [**ExReleaseSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451067)                              | 取得の呼び出し元の共有アクセス、スピン ロックを解放し、元の IRQL を復元します。                      |
| [**ExReleaseSpinLockSharedFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/hh451064)      | 取得の呼び出し元の共有アクセス、スピン ロックを解放し、IRQL が低下します。                         |
| [**ExTryConvertSharedSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451070)      | 呼び出し元を既に共有アクセスのための排他アクセスを保持するスピン ロックのアクセスの状態を変換しようとしています。 |

 

これは、スピン ロックへのポインター、最初のパラメーターとして、すべて実行リーダー/ライターのスピン ロック ルーチン、 **EX\_スピン\_ロック**構造体。 この構造体は、ドライバーに対して非透過的です。 ドライバーは、スピン ロックからページングされないシステム メモリ、記憶域を割り当てる必要があり、をゼロにロックを初期化します。

 

 




