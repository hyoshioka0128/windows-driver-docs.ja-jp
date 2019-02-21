---
title: マルチプロセッサ環境でのエラー
description: マルチプロセッサ環境でのエラー
ms.assetid: 8a76b8d6-14d8-4709-8b15-e8b6b5094a1b
keywords:
- 信頼性 WDK カーネルでは、競合状態
- 競合条件 WDK カーネル
- 信頼性の WDK カーネル、マルチプロセッサ環境のエラー
- マルチプロセッサ環境エラー WDK カーネル
- ロックの WDK カーネル
- WDK のカーネルを処理する複数の I/O 要求
- I/O 要求の WDK カーネル
- スレッド競合 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4b7866b7ef29c9e79336c2b228a25296a850ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531249"
---
# <a name="errors-in-a-multiprocessor-environment"></a>マルチプロセッサ環境でのエラー





NT ベースのオペレーティング システムのドライバーは、マルチ スレッドです。別のスレッドから同時に複数の I/O 要求を受信できます。 ドライバーを設計する必要があります、SMP システム上で実行され、データの整合性を確保するための対策になることは想定しています。

具体的には、ドライバーがグローバルに変更されるたびに使用することもファイル オブジェクトのデータにする必要があります、インタロックされたシーケンスまたはロック競合状態を回避します。

### <a name="encountering-a-race-condition-when-referencing-global-or-file-object-specific-data"></a>グローバルを参照するか、オブジェクトに固有のデータをファイルに、競合状態が発生

ドライバーでグローバル データにアクセスするときに、次のコード スニペットで、競合状態が発生する可能性があります**Data.LpcInfo**:

```cpp
   PLPC_INFO pLpcInfo = &Data.LpcInfo; //Pointer to global data
   ...
   ...
   // This saved pointer may be overwritten by another thread.
   pLpcInfo->LpcPortName.Buffer = ExAllocatePool(
                                     PagedPool,
                                     arg->PortName.Length);
```

複数のスレッドが、IOCTL 呼び出しの結果としてこのコードを入力するように、ポインターが上書きされますメモリ リークが発生可能性があります。 この問題を回避するために、ドライバーを使用する必要があります、 **ExInterlocked * Xxx*** ルーチンまたは何らかの種類のグローバル データを変更するときにロックします。 ドライバーの要件は、許容可能なロックの種類を決定します。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)、[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)、および[ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)します。

次の例では、特定のファイルのバッファーを再配置しようとしました。 (**エンドポイント -&gt;LocalAddress**) エンドポイント アドレスを保持するために。

```cpp
   Endpoint = FileObject->FsContext;

    if ( Endpoint->LocalAddress != NULL &&
         Endpoint->LocalAddressLength <
                   ListenEndpoint->LocalAddressLength ) {

      FREE_POOL (Endpoint->LocalAddress,
                 LOCAL_ADDRESS_POOL_TAG
                 );
      Endpoint->LocalAddress  = NULL;
   }

    if ( Endpoint->LocalAddress == NULL ) {
       Endpoint->LocalAddress =
            ALLOCATE_POOL (NonPagedPool,
                           ListenEndpoint->LocalAddressLength,
                           LOCAL_ADDRESS_POOL_TAG);
   }
```

この例で競合状態でしたが行われるアクセス ファイル オブジェクト。 ドライバーがすべてのロックを所持していないので、同じファイル オブジェクトの 2 つの要求は、この関数を入力できます。 結果は同じメモリを解放するための複数の試行、解放されたメモリへの参照、またはメモリ リークが発生します。 2 つのこれらのエラーを回避するために**場合**ステートメントは、スピン ロックで囲む必要があります。








