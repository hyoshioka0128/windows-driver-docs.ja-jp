---
title: ルックアサイド リストの使用
description: ルックアサイド リストの使用
ms.assetid: 07a75b8b-04b9-48ea-bda4-53889dd661a9
keywords:
- メモリ管理の WDK カーネル、ルック アサイド リスト
- ルック アサイド リストの WDK カーネル
- 固定サイズ バッファーの割り当ての WDK カーネル
- ExXxxLookasideList ルーチン WDK
- WDK ルック アサイドのエントリ
- 非ページのルック アサイド リストの WDK カーネル
- ページのルック アサイド リストの WDK カーネル
- WDK の日常的なメモリを割り当てる
- WDK のメモリの解放ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0582df0a1cf5966ffdf2a620d0a613a527c68c56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364929"
---
# <a name="using-lookaside-lists"></a>ルックアサイド リストの使用





オンデマンドでの I/O 操作を実行するには、動的に固定サイズ バッファーを割り当てる必要がありますドライバーを使用できます、 **Ex*Xxx*LookasideListEx**または**Ex*Xxx*LookasideList**ルーチンをサポートします。 このようなドライバーのルック アサイド リストの初期化後に、オペレーティング システムはルック アサイド ドライバーの一覧で、一連のドライバーの再利用可能な固定サイズのバッファーを効果的に予約するいくつかの指定されたサイズのバッファーを動的に割り当てられたを保持します。 形式とドライバーの固定サイズ バッファーの内容 (とも呼ばれます*エントリ*) のルック アサイド リストにはドライバーが決定します。

たとえば、基になる SCSI ポート/ミニポート ドライバーの SCSI 要求ブロック (される Srb) を設定する必要がある記憶域クラス ドライバーは、ルック アサイド リストを使用します。 このようなクラス ドライバーは、ルック アサイド リストされる Srb のとして必要な場合にバッファーを割り当てし、SRB が完了した IRP のクラス ドライバーに返されるたびに再利用するルック アサイド リストのルック アサイド リストに戻るには、各 SRB バッファーを解放します。 ルック アサイド リストは、割り当てとされる Srb の固定サイズのバッファーの解放を管理する方法を便利で経済的なストレージ クラス ドライバーのドライバの I/O 要求が増加し、該当するために、いつでも使用する必要がある数される Srb を事前に定義できません、ため、します。このようなドライバーです。

オペレーティング システムでは、現在、使用されているすべてのリスト内のエントリの割り当てと解放の要求と新しいエントリの使用可能なシステムのプールを動的に追跡するすべてのページおよび非ページのルック アサイド リストの状態を維持します。 割り当ての需要が高いとき、オペレーティング システムは、各ルック アサイド リストを保持するエントリの数を増やします。 要求がもう一度少なくなると、システムのプールに戻す余剰ルック アサイドのエントリを解放します。

ルック アサイド リストは、スレッド セーフです。 ルック アサイド リストが、複数を有効にする組み込みの同期ルック アサイド リストを共有するためのドライバーでスレッドを同時に実行します。 これらのスレッドは、共有ルック アサイド リストからバッファーを割り当てる安全かつ明示的にこれらの操作を同期するドライバーを必要とせず、リストにこれらのバッファーを解放します。 ただし、可能なリークとデータの破損、ルック アサイド リストを共有しているスレッドのセットを回避するために同期する必要がある明示的に初期化し、リストの削除。

## <a name="lookaside-list-interfaces"></a>ルック アサイド リスト インターフェイス


以降、Windows Vista では、 [**ルック アサイド\_一覧\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff554329)構造体には、非ページや段組のバッファーを含むことのできるルック アサイド リストがについて説明します。 場合は、ドライバーは、カスタム*Allocate*と*Free*ルーチンこのルック アサイド リストのこれらのルーチンは、入力パラメーターとしてプライベート コンテキストを受信します。 ドライバーは、このコンテキストを使用して、ルック アサイド リストのプライベート データを収集します。 たとえば、コンテキストは動的に割り当てられ、リストによって解放リスト エントリの数がカウントされる可能性があります。 この方法でコンテキストを使用する方法を示すコード例を参照してください。 [ **ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)します。

次のシステム指定のルーチンによって記述されるルック アサイド リストのサポート、**ルック アサイド\_一覧\_EX**構造体。

[**ExAllocateFromLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544381)

[**ExDeleteLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544563)

[**ExFlushLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544587)

[**ExFreeToLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544597)

[**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)

Windows 2000 以降、 [**ページ\_ルック アサイド\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff558775)構造体には、ページ バッファを含むルック アサイド リストがについて説明します。 場合は、ドライバーは、カスタム*Allocate*と*Free*ルーチンこのルック アサイド リストのこれらのルーチンは受け取りません入力パラメーターとしてプライベート コンテキスト。 このため、ドライバーを Windows Vista および Windows の以降のバージョンでのみ実行する場合は使用を検討して、**ルック アサイド\_一覧\_EX**の代わりに構造体、**ページング\_ルック アサイド\_一覧**ルック アサイド リストの構造体。 次のシステム指定のルーチンによって記述されるルック アサイド リストのサポート、**ページ\_ルック アサイド\_一覧**構造体。

[**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)

[**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)

[**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)

[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)

Windows 2000 以降、 [ **NPAGED\_ルック アサイド\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff556431)構造体には、非ページのバッファーを含むルック アサイド リストがについて説明します。 場合は、ドライバーは、カスタム*Allocate*と*Free*ルーチンこのルック アサイド リストのこれらのルーチンは受け取りません入力パラメーターとしてプライベート コンテキスト。 ここでもには、ドライバーを Windows Vista および Windows の以降のバージョンでのみ実行する場合は使用を検討して、**ルック アサイド\_一覧\_EX**の代わりに構造体、 **NPAGED\_ルック アサイド\_一覧**ルック アサイド リストの構造体。 次のシステム指定のルーチンによって記述されるルック アサイド リストのサポート、 **NPAGED\_ルック アサイド\_一覧**構造体。

[**ExAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544388)

[**ExDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544566)

[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)

[**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)

## <a name="implementation-guidelines"></a>実装ガイドライン


使用するルック アサイド リストを実装するために、**ルック アサイド\_一覧\_EX**構造体をこれらのデザイン ガイドラインに従ってください。

-   呼び出す**ExInitializeLookasideListEx**ルック アサイド リストを設定します。 この呼び出しでは、ルック アサイド リストのエントリがページングがかどうか、または非ページのバッファーを指定します。 ドライバーそのものや、基になるドライバーが渡される、ルック アサイド リストのエントリは、IRQL でこれらのエントリをアクセス可能性がありますいる場合は、非ページのバッファーを使用&gt;= ディスパッチ\_レベル。 ドライバーのルック アサイド リストの項目へのアクセスは、IRQL で常に発生する場合にのみページ バッファを使用して&lt;APC を =\_レベル。

-   **ルック アサイド\_一覧\_EX**ルック アサイド リストは、リストのエントリがページまたは非ページにあるかどうかに関係なく非ページ システム メモリ内で常に存在する必要があるの構造体します。

-   パフォーマンスを向上させるには、渡す**NULL**のポインター、 *Allocate*と*Free*パラメーター **ExInitializeLookasideListEx**しない限り、割り当てと解放のルーチンは、だけで複数の割り当てし、ルック アサイド リストのエントリのメモリを解放しないでください必要があります。 たとえば、これらのルーチンは、動的に割り当てられたバッファーのドライバーの使用状況に関する情報を記録することがあります。

-   ドライバーによって提供される*Allocate*ルーチンは、入力パラメーターを渡すことができます (*PoolType*、*タグ*、および*サイズ*) に直接受信します。[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)または[ **ExAllocatePoolWithQuotaTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544513)新しいバッファーを割り当てルーチン。

-   すべての呼び出しの**ExAllocateFromLookasideListEx**、相互の呼び出しを行う**ExFreeToLookasideListEx**できるだけ早くたびに以前に割り当てられたエントリが使用されていません。

指定*Allocate*と*Free*ルーチンを呼び出すよりも、何もしない[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)と[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)、それぞれ、プロセッサ サイクルを浪費します。 **ExAllocateFromLookasideListEx**に必要な呼び出しを行う**exallocatepoolwithtag に**と**ExFreePool**ドライバーがパスと自動的に**NULL***Allocate*と*Free*へのポインター **ExInitializeLookasideListEx**します。

いずれかのドライバーによって提供される*Allocate*ルーチンはページ プール ルック アサイドの非ページ化リストまたはその逆に保持されることからエントリをメモリを割り当てられませんする必要があります。 後続のすべてのドライバーのため、固定サイズのエントリを割り当てる必要がありますもこと**ExAllocateFromLookasideListEx**リストが空でない限りのルック アサイド リストに現在保持されている最初のエントリを返します。 呼び出しは、 **ExAllocateFromLookasideListEx** 、呼び出し時に、ドライバーによって提供される*Allocate*ルーチンの場合は、特定のルック アサイド リストは空です。 呼び出すたびにそのため、 **ExAllocateFromLookasideListEx**、返されるエントリにルック アサイド リストのすべてのエントリが固定サイズの場合にのみ、ドライバーが必要なサイズになります。 ドライバーによって提供される*Allocate*ルーチンを変更しないでくださいも、*タグ*、ドライバーは、最初に渡された値**ExInitializeLookasideListEx**のためでの変更プール タグの値は、デバッグと難しく、ドライバーのメモリ使用量を追跡します。

呼び出す**ExFreeToLookasideListEx**リストである場合を除き、ルック アサイド リストのエントリがストアによって以前割り当て*完全*(つまり、一覧が含まれていますのシステムで決定された最大数にはエントリの場合)。 パフォーマンスの向上のため、ドライバーが相互の呼び出しを作成します。 **ExFreeToLookasideListEx**にすべての呼び出し可能な限り早く**ExAllocateFromLookasideListEx**します。 ドライバーのルック アサイドにエントリを解放するときにそのドライバーの次回の呼び出しではすぐに、一覧**ExAllocateFromLookasideListEx**を動的に新しいエントリのメモリの割り当てのパフォーマンスの低下を発生させ、はるかに少ない可能性があります。

使用するルック アサイド リストのようなガイドラインが適用されます、**ページ\_ルック アサイド\_一覧**または**NPAGED\_ルック アサイド\_一覧**構造体。

 

 




