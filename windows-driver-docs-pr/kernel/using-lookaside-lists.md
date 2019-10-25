---
title: ルックアサイドリストの使用
description: ルックアサイドリストの使用
ms.assetid: 07a75b8b-04b9-48ea-bda4-53889dd661a9
keywords:
- メモリ管理 WDK カーネル、ルックアサイドリスト
- ルックアサイドリスト WDK カーネル
- 固定サイズのバッファー割り当ての WDK カーネル
- Exxxx Look Aside リストルーチン WDK
- WDK ルックアサイドのエントリ
- 非ページルックアサイドの一覧 WDK カーネル
- ページルックアサイドリスト WDK カーネル
- 日常的な WDK メモリの割り当て
- フリールーチン WDK メモリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a38e7117e9fc13a3f3a37a1680158739e7a87e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838348"
---
# <a name="using-lookaside-lists"></a>ルックアサイドリストの使用





オンデマンド i/o 操作を実行するために、固定サイズのバッファーを動的に割り当てる必要があるドライバーは、" ***xxx*ルック asi"** または " **ex*xxx*** " の各リストサポートルーチンを使用できます。 このようなドライバーがルックアサイドリストを初期化した後、オペレーティングシステムは、ドライバーのルックアサイドリストに指定されたサイズの動的に割り当てられたバッファーをいくつか保持し、ドライバーに対して再利用可能な固定サイズのバッファーのセットを効果的に予約します。 ルックアサイドリスト内のドライバーの固定サイズバッファー (*エントリ*とも呼ばれます) の形式と内容は、ドライバーによって決定されます。

たとえば、基になる SCSI ポート/ミニポートドライバーに SCSI 要求ブロック (SRBs) を設定する必要がある記憶域クラスドライバーでは、ルックアサイドリストを使用します。 このようなクラスドライバーは、ルックアサイドリストから必要に応じて SRBs のバッファーを割り当て、完了した IRP のクラスドライバーに SRB が返されるたびに、ルックアサイドリストを再利用するために、各 SRB バッファーをルックアサイドリストに戻します。 ストレージクラスドライバーは、ドライバーに対する i/o 要求の増加と増加に応じて、いつでも SRBs を使用する必要があることを事前に確認できないので、ルックアサイドリストは、固定サイズの SRBs のバッファーの割り当てと解放を管理するための便利で経済的な方法です。このようなドライバーでは、

オペレーティングシステムは、現在使用されているすべてのページ表示および非表示のルックアサイドリストに関する状態を保持し、すべてのリストのエントリの割り当てと割り当て解除の要求を動的に追跡し、新しいエントリに使用できるシステムプールを動的に追跡します。 割り当ての需要が高い場合、オペレーティングシステムは各ルックアサイドリストに含まれるエントリの数を増やします。 要求が再度実行されると、余剰ルックアサイドエントリがシステムプールに再び解放されます。

ルックアサイドリストはスレッドセーフです。 ルックアサイドリストには、ドライバー内で同時に実行される複数のスレッドで、ルックアサイドリストを共有できるようにするための同期が組み込まれています。 これらのスレッドは、共有ルックアサイドリストからバッファーを安全に割り当て、これらの操作をドライバーが明示的に同期せずに、これらのバッファーをリストに解放することができます。 ただし、リークやデータの破損を回避するために、ルックアサイドリストを共有する一連のスレッドでは、リストの初期化と削除を明示的に同期する必要があります。

## <a name="lookaside-list-interfaces"></a>ルックアサイドリストインターフェイス


Windows Vista 以降では、[**ルックアサイド\_list\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体は、ページングされていないバッファーまたは非ページバッファーを含めることができるルックアサイドリストを記述します。 ドライバーがこのルックアサイドリストに対してカスタムの*割り当て*および*フリー*ルーチンを提供する場合、これらのルーチンは、入力パラメーターとしてプライベートコンテキストを受け取ります。 ドライバーは、このコンテキストを使用して、ルックアサイドリストのプライベートデータを収集できます。 たとえば、コンテキストは、リストによって動的に割り当てられ解放されるリストエントリの数をカウントするために使用される場合があります。 この方法でコンテキストを使用する方法を示すコード例については[ **、「」を参照して**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)ください。

次のシステム提供のルーチンは、**ルック\_アサイド\_EX**構造体で記述されているルックアサイドリストをサポートしています。

[**Exallocatefromlook Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromlookasidelistex)

[**Exdeletelook Asiststex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletelookasidelistex)

[**Exflushstasiアス Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exflushlookasidelistex)

[**Exfreetolook Asifrostex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetolookasidelistex)

[**Exststokasiアス Stex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializelookasidelistex)

Windows 2000 以降、ページングされた[ **\_ルックアサイド\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造は、ページングされたバッファーを含むルックアサイドリストを記述します。 ドライバーがこのルックアサイドリストに対してカスタムの*割り当て*および*フリー*ルーチンを提供する場合、これらのルーチンは、入力パラメーターとしてプライベートコンテキストを受け取りません。 このため、ドライバーを Windows Vista 以降のバージョンの Windows でのみ実行することを想定している場合は、ページ分割された **\_ルックアサイド\_リスト**の構造ではなく、**ルックアサイド\_リスト\_EX**構造体を使用することを検討してください。ルックアサイドリスト。 次のシステム指定ルーチンは、ページングされた **\_ルックアサイド\_リスト**構造体によって記述されるルックアサイドリストをサポートしています。

[**Exallocatefrompagedlook のリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)

[**ExDeletePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)

[**Exfreetopagedlook のリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)

[**ExInitializePagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)

Windows 2000 以降、Npaged された[ **\_ルックアサイド\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造は、非ページバッファーを含むルックアサイドリストを記述します。 ドライバーがこのルックアサイドリストに対してカスタムの*割り当て*および*フリー*ルーチンを提供する場合、これらのルーチンは、入力パラメーターとしてプライベートコンテキストを受け取りません。 ここでも、ドライバーを Windows Vista 以降のバージョンの Windows でのみ実行することを想定している場合は、 **Npaged\_ルックアサイド\_リスト**構造ではなく、**ルックアサイド\_リスト\_EX**構造体を使用することを検討してください。ルックアサイドリスト。 次のシステム指定ルーチンは、 **Npaged\_ルックアサイド\_リスト**構造体によって記述されたルックアサイドリストをサポートしています。

[**ExAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefromnpagedlookasidelist)

[**ExDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)

[**ExFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)

[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)

## <a name="implementation-guidelines"></a>実装ガイダンス


**ルックアサイド\_list\_EX**構造体を使用するルックアサイドリストを実装するには、次の設計ガイドラインに従います。

-   ルックアサイドを呼び出して、ルックアサイド**リストを設定**します。 この呼び出しで、ルックアサイドリスト内のエントリをページングバッファーと非ページバッファーのどちらにするかを指定します。 ドライバー自体またはそのルックアサイドリストエントリを渡す基になるドライバーが、IRQL &gt;= ディスパッチ\_レベルでこれらのエントリにアクセスする場合は、非ページバッファーを使用します。 ドライバーのルックアサイドリストエントリへのアクセスが常に IRQL &lt;= APC\_レベルで発生する場合にのみ、ページングされたバッファーを使用します。

-   リスト内のエントリがページングされているかどうかに関係なく、ルックアサイドリストの**ルック\_list\_EX**構造体は、常に非ページシステムメモリ内に存在する必要があります。

-   パフォーマンスを向上させるには *、割り当てと* *解放*のルーチンが割り当てと**解放を行う**だけではなく、割り当てと解放のパラメーターに対して**NULL**ポインターを渡す必要があります。ルックアサイドリストエントリ。 たとえば、これらのルーチンは、ドライバーによって動的に割り当てられたバッファーの使用状況に関する情報を記録する場合があります。

-   ドライバーによって提供される*割り当て*ルーチンは、 [**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)または[**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)割り当てのために直接受信する入力パラメーター (*pooltype*、 *Tag*、および*Size*) を渡すことができます。新しいバッファー。

-   以前に割り当てられたエントリが使用されなくなるたびに、 **Exallocatefromlook Asifrostex**への呼び出しごとに、できるだけ早く**Exfreetolook asifrostex**への呼び出しを行います。

*割り当て*および*フリー*ルーチンを提供すると、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)と[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出すだけではなく、プロセッササイクルが浪費されます。 **Exallocatefromlookasidelistex**を使用すると、ドライバーが**NULL**の*割り当て*および*フリー*ポインターを渡したときに、 **Exallocatepoolwithtag**と**exfreepool**に必要な呼び出しを自動的に行うことができるよう**になります。** このようにしてください。

ドライバーによって提供される*割り当て*ルーチンでは、ページプールからのエントリを非ページのルックアサイドリストに保持するために、メモリを割り当てないようにする必要があります。 また、固定サイズのエントリも割り当てる必要があります。これは、 **Exallocatefromlook Stex**への後続のドライバー呼び出しによって、リストが空でない限り、ルックアサイドリストに現在保持されている最初のエントリが返されるためです。 つまり、指定されたルックアサイドリストが現在空の場合にのみ、ドライバー**によって**提供される*割り当て*ルーチンが呼び出されます。 このため、 **Exallocatefromstasiアット**を呼び出すたびに、返されるエントリは、ルックアサイドリスト内のすべてのエントリのサイズが固定されている場合にのみ、ドライバーが必要とするサイズと正確に一致します。 また、ドライバーによって提供される*割り当て*ルーチンでは、ドライバーが最初に実行した*タグ*値を変更しないようにする必要が**あります。** これは、プールタグの値の変更によってドライバーのメモリがデバッグおよび追跡されるためです。使用が難しくなります。

リストが既に*いっぱい*になっていない限り、以前に割り当てられたエントリ (リストには、システムによって決定されたエントリの最大数が含まれている) を除いて、以前に割り当てられた**エントリを格納**します。 パフォーマンスを向上させるために、ドライバーは、 **Exallocatefromstasifrostex**に対して行われるすべての呼び出しに対して可能な限り迅速に、 **Exfreetolook asifrostex**に対する相互呼び出しを行う必要があります。 ドライバーがエントリをルックアサイドリストにすばやく戻すと、そのドライバーが次に**Exallocatefromlook Stex**を呼び出したときに、新しいエントリにメモリを動的に割り当てることによってパフォーマンスが低下する可能性がはるかに低くなります。

同様のガイドラインは、ページングされた **\_ルックアサイド\_リスト**または**NPAGED\_ルックアサイド\_リスト**構造を使用するルックアサイドリストにも当てはまります。

 

 




