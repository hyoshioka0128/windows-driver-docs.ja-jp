---
title: 読み取り/書き込みスピン ロック
description: Windows Vista Service Pack 1 (SP1) 以降では、関連する一連のルーチンが、リーダーとライターによって共有されるデータ構造への同期アクセスをサポートするために、スピンロックを使用します。
ms.assetid: E2853F35-590E-4EF5-8647-1261BC4B8D15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c0fac2388e801faae9f874989c534233fcf672bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827574"
---
# <a name="readerwriter-spin-locks"></a>読み取り/書き込みスピン ロック


Windows Vista Service Pack 1 (SP1) 以降では、関連する一連のルーチンが、リーダーとライターによって共有されるデータ構造への同期アクセスをサポートするために、スピンロックを使用します。 データ構造に対する読み取りアクセスのみを必要とするスレッドは、スピンロックを使用して、この構造体を他のリーダースレッドと共有できます。 共有データ構造に書き込む必要があるスレッドでは、この構造体に書き込む前に、スピンロックを使用してデータ構造への排他アクセスを取得する必要があります。

リーダースレッドが共有アクセス用のスピンロックを取得する必要があり、ライタースレッドによる排他アクセスのためにロックが既に保持されている場合、リーダーは最初にライターがロックを解放するまで待機する必要があります。 同様に、ライタースレッドが排他アクセス用のスピンロックを取得する必要があり、そのロックが1つ以上のリーダースレッドによって共有アクセスに対して既に保持されている場合、ライタースレッドは、これらすべてのリーダースレッドがロックを解放するまで待機する必要があります。 ライターは待機中に、新しいリーダースレッドがロックを取得することはできません。 代わりに、ライターが待機しているロックを取得する必要があるリーダーは、まずライターがロックを取得して解放するまで待機する必要があります。

スレッドは、リーダーとライターの間でロールを切り替えることができます。 共有アクセスのスピンロックを既に保持しているスレッドは、スピンロックのアクセスモードを共有モードから排他モードに変換することができます。 この試行は、共有アクセスのスピンロックをまだ保持しているリーダーがいない場合、および排他アクセスのスピンロックを取得するためにライターが既に待機していない場合に成功します。

スピンロックを再帰的に取得するとデッドロックが発生し、許可されません。

Windows Vista SP1 以降で読み取り/書き込みスピンロックを管理するために使用できるルーチンの一覧を次に示します。

| ルーチン名                                                                                | 説明                                                                                                           |
|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**ExAcquireSpinLockExclusive**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451007(v=vs.85))                         | 呼び出し元による排他アクセスのためのスピンロックを取得し、\_レベルをディスパッチするための IRQL を発生させます。                      |
| [**ExAcquireSpinLockExclusiveAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451009(v=vs.85))    | IRQL &gt;= ディスパッチ\_レベルで既に実行されている呼び出し元による排他アクセスのためのスピンロックを取得します。          |
| [**ExAcquireSpinLockShared**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451053(v=vs.85))                               | 呼び出し元による共有アクセスのスピンロックを取得し、\_レベルをディスパッチするための IRQL を発生させます。                         |
| [**ExAcquireSpinLockSharedAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451055(v=vs.85))           | IRQL &gt;= ディスパッチ\_レベルで既に実行されている呼び出し元による、共有アクセスのためのスピンロックを取得します。             |
| [**ExReleaseSpinLockExclusive**](https://msdn.microsoft.com/library/windows/hardware/hh451061)                        | 呼び出し元が排他アクセス用に取得したスピンロックを解放し、元の IRQL を復元します。                   |
| [**ExReleaseSpinLockExclusiveFromDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451058(v=vs.85)) | 呼び出し元が排他アクセス用に取得したスピンロックを解放し、IRQL を低くしません。                      |
| [**ExReleaseSpinLockShared**](https://msdn.microsoft.com/library/windows/hardware/hh451067)                              | 呼び出し元が共有アクセス用に取得したスピンロックを解放し、元の IRQL を復元します。                      |
| [**ExReleaseSpinLockSharedFromDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh451064(v=vs.85))      | 呼び出し元が共有アクセス用に取得したスピンロックを解放し、IRQL を低くしません。                         |
| [**ExTryConvertSharedSpinLockExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-extryconvertsharedspinlockexclusive)      | 呼び出し元が排他アクセスに対して既に保持しているスピンロックのアクセス状態の変換を試みます。 |

 

リーダー/ライターのスピンロックルーチンはすべて、最初のパラメーターとして、1番目のパラメーターとして、 **\_スピン\_ロック**構造体であるスピンロックへのポインターになります。 この構造は、ドライバーに対して非透過的です。 ドライバーは、非ページシステムメモリからスピンロックのストレージを割り当て、ロックをゼロに初期化します。

 

 




