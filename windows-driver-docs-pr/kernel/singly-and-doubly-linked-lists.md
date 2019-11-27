---
title: 片方向および双方向リンク リスト
description: 片方向および双方向リンク リスト
ms.assetid: 3a305f54-7866-4163-a3e4-e078d1927adc
keywords:
- シングルリンクリスト WDK カーネル
- ダブルリンクリスト WDK カーネル
- シーケンスされた単一のリンクリスト WDK カーネル
- SINGLE_LIST_ENTRY
- LIST_ENTRY
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b545baa9f64be63e5778961a2d97a71a0187f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836311"
---
# <a name="singly-and-doubly-linked-lists"></a>片方向および双方向リンク リスト





### <a name="singly-linked-lists"></a>シングルリンクリスト

オペレーティングシステムには、[**単一の\_リスト\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry)構造を使用する、単一のリンクリストの組み込みサポートが用意されています。 シングルリンクリストは、リストの先頭にいくつかのリストエントリを加えたもので構成されます。 リストが空の場合は、リストエントリの数が0になります。各リストエントリは、エントリ構造 **\_単一の\_リスト**として表されます。 また、リストの先頭は、 **1 つの\_リスト\_エントリ**の構造として表されます。

各**単一\_リスト\_エントリ**構造には、**次**のメンバーが含まれています。このメンバーは、別の**単一\_リスト\_エントリ**構造を指します。 リストの先頭を表す**1 つの\_リスト\_エントリ**の構造では、**次**のメンバーがリストの最初のエントリを指します。リストが空の場合、は NULL になります。 リスト内のエントリを表す**1 つの\_リスト\_エントリ**構造では、**次**のメンバーがリストの次のエントリを指しています。または、このエントリがリストの最後にある場合は NULL になります。

シングルリンクリストを操作するルーチンは、リストの先頭を表す[**単一の\_リスト\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry)へのポインターを取得します。 **次**のポインターを更新して、操作後のリストの最初のエントリを指すようにします。

*ListHead*変数が、リストの先頭を表す**単一の\_リスト\_エントリ**の構造体へのポインターであるとします。 ドライバーは、次のように*ListHead*を操作します。

-   リストを空として初期化するには、 *ListHead * * *-&gt;Next** を**NULL**に設定します。

-   新しいエントリを一覧に追加するには、新しいエントリを表す**単一の\_リスト\_エントリ**を割り当ててから、 [**pushentrylist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pushentrylist)を呼び出してリストの先頭にエントリを追加します。

-   [**Popentrylist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-popentrylist)を使用して、リストの最初のエントリをポップします。

**1 つの\_リスト\_エントリ**自体には、**次**のメンバーのみが含まれます。 リストに独自のデータを格納するには、次のように、リストエントリを記述する構造体のメンバーとして、**単一の\_リスト\_エントリ**を埋め込みます。

```cpp
typedef struct {
  // driver-defined members
  .
  .
  .
  SINGLE_LIST_ENTRY SingleListEntry;
 
  // other driver-defined members
  .
  .
  .
} XXX_ENTRY;
```

リストに新しいエントリを追加するには、 **XXX\_エントリ**構造を割り当て、 **SingleListEntry**メンバーへのポインターを[**pushentrylist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pushentrylist)に渡します。 **1 つの\_リスト**にポインターを変換し\_**XXX\_エントリ**に戻すには、[**包含\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用します。 次に、単一のリンクリストからドライバー定義のエントリを挿入または削除するルーチンの例を示します。

```cpp
typedef struct {
  PVOID DriverData1;
  SINGLE_LIST_ENTRY SingleListEntry;
  ULONG DriverData2;
} XXX_ENTRY, *PXXX_ENTRY;

void
PushXxxEntry(PSINGLE_LIST_ENTRY ListHead, PXXX_ENTRY Entry)
{
    PushEntryList(ListHead, &(Entry->SingleListEntry));
}

PXXX_ENTRY
PopXxxEntry(PSINGLE_LIST_ENTRY ListHead)
{
    PSINGLE_LIST_ENTRY SingleListEntry;
    SingleListEntry = PopEntryList(ListHead);
    return CONTAINING_RECORD(SingleListEntry, XXX_ENTRY, SingleListEntry);
}
```

また、システムでは、リスト操作、 [**ExInterlockedPopEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545408) 、および[**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)のアトミックバージョンも提供されます。 各は、追加のスピンロックパラメーターを受け取ります。 ルーチンは、リストを更新する前にスピンロックを取得した後、操作の完了後にスピンロックを解放します。 ロックが保持されている間、割り込みは無効になります。 リストに対する各操作は、同じスピンロックを使用して、リストに対する各操作が他のすべての操作と同期されるようにする必要があります。 スピンロックは、これらの**Exinterlocked ロック*Xxx*リスト**ルーチンでのみ使用する必要があります。 その他の目的では、スピンロックを使用しないでください。 ドライバーは複数のリストに対して同じロックを使用できますが、この動作によってロックの競合が増加するため、ドライバーはこれを回避する必要があります。

たとえば、 **ExInterlockedPopEntryList**ルーチンと**ExInterlockedPushEntryList**ルーチンは、IRQL = パッシブ\_レベルで実行されるドライバースレッドと dirql で実行される ISR によって、単一のリンクリストの共有をサポートできます。 これらのルーチンは、スピンロックが保持されているときに割り込みを無効にします。 したがって、ISR とドライバーのスレッドは、デッドロックを損なうことなく、これらの**Exinterlocked ロック*Xxx*リスト**ルーチンへの呼び出しで同じスピンロックを安全に使用できます。

リスト操作のアトミックバージョンと非アトミックバージョンの呼び出しを同じリストに混在させないでください。 アトミックバージョンと非アトミックバージョンが同じリストで同時に実行されると、データ構造が破損し、コンピューターが応答を停止したり、バグチェック (*クラッシュ*) したりする可能性があります。 (アトミックおよび非アトミックバージョンのリスト操作の呼び出しを混在させる代わりに、非アトミックルーチンの呼び出し中にスピンロックを取得することはできません。 この方法でのスピンロックの使用はサポートされていないため、リストが破損する可能性があります)。

システムでは、アトミックの単一リンクリストをより効率的に実装することもできます。 詳細については、「シーケンス化された[単一のリンクリスト](#sequenced-singly-linked-lists)」を参照してください。

### <a name="doubly-linked-lists"></a>ダブルリンクリスト

オペレーティングシステムには、[**リスト\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)構造を使用するダブルリンクリストのサポートが組み込まれています。 ダブルリンクリストは、リストの先頭といくつかのリストエントリで構成されます。 リストが空の場合は、リストエントリの数が0になります。各リストエントリは、エントリ構造 **\_リスト**として表されます。 また、リストの先頭は **\_エントリ**の構造体のリストとして表されます。

各**リスト\_エントリ**構造には、 **flink**メンバーと**点滅**メンバーが含まれています。 両方のメンバーは **\_エントリ構造を一覧表示**するポインターです。

リストの先頭を表す**リスト\_エントリ**の構造体では、 **flink**メンバーがリストの最初のエントリを指し、**点滅**メンバーがリストの最後のエントリを指しています。 リストが空の場合は、リストの先頭がリストの先頭になるように**Flink**と**点滅**します。

一覧のエントリを表す**リスト\_エントリ**の構造では、 **flink**メンバーはリスト内の次のエントリを指し、**点滅**メンバーはリスト内の前のエントリを指します。 (エントリがリスト内の最後のエントリである場合、 **Flink**はリストの先頭を指します。 同様に、エントリがリスト内の最初のエントリである場合、**点滅**はリストの先頭を指します)。

(これらのルールは一見すると驚くかもしれませんが、条件付きのコード分岐を使用せずにリストの挿入と削除の操作を実装できます)。

ダブルリンクリストを操作するルーチンは、リストの先頭を表す[**リスト\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)へのポインターを取得します。 これらのルーチンは、リストの先頭の**Flink**メンバーと**点滅**メンバーを更新して、これらのメンバーが結果のリストの最初と最後のエントリを指すようにします。

*ListHead*変数が、リストの先頭を表す**リスト\_エントリ**の構造体へのポインターであるとします。 ドライバーは、次のように*ListHead*を操作します。

-   リストを空として初期化するには、 [**InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)を使用します。これに*より、ListHead * * *-&gt;flink** と*ListHead * * *-&gt;点滅** が*ListHead*を指すように初期化されます。

-   リストの先頭に新しいエントリを挿入するには、新しいエントリを表す**リスト\_エントリ**を割り当ててから、挿入された[**エントリをリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist)の先頭に挿入します。

-   新しいエントリをリストの末尾に追加するには、新しいエントリを表す**リスト\_エントリ**を割り当ててから、 [**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)を呼び出してリストの末尾にエントリを挿入します。

-   リストから最初のエントリを削除するには、[ [**Removeヘッドホン list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)] を使用します。 この値は、リストから削除されたエントリへのポインターを返すか、リストが空の場合は*ListHead*に戻ります。

-   リストから最後のエントリを削除するには、 [**Removetthe list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removetaillist)を使用します。 この値は、リストから削除されたエントリへのポインターを返すか、リストが空の場合は*ListHead*に戻ります。

-   指定されたエントリを一覧から削除するには、 [**Removeentrylist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeentrylist)を使用します。

-   リストが空かどうかを確認するには、 [**Islistempty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-islistempty)を使用します。

-   リストを別のリストの末尾に追加するには、 [**AppendTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-appendtaillist)を使用します。

[**リスト\_エントリ**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)自体には、**点滅**および**flink**メンバーのみが含まれます。 リストに独自のデータを格納するには、リストエントリを記述する構造体のメンバーとして**リスト\_エントリ**を次のように埋め込みます。

```cpp
typedef struct {
  // driver-defined members
  .
  .
  .
  LIST_ENTRY ListEntry;
 
  // other driver-defined members.
  .
  .
  .
} XXX_ENTRY;
```

リストに新しいエントリを追加するには、 **XXX\_エントリ**の構造を割り当ててから、 **ListEntry**メンバーへのポインターを、挿入された **@ list**または**InsertTailList**に渡します。 ポインターをリストに変換して、 **XXX\_エントリ**に戻すには **\_** を[**含む\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用します。 この手法の例については、単一のリンクリストを使用して、上記の「シングルリンクリスト」を参照してください。

システムには、リスト操作、 [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)、 [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)、および[**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)のアトミックバージョンも用意されています。 ( **Removetlist**または**removeentrylist**の atomic バージョンがないことに注意してください)。各ルーチンは、追加のスピンロックパラメーターを受け取ります。 ルーチンは、リストを更新する前にスピンロックを取得し、操作の完了後にスピンロックを解放します。 ロックが保持されている間、割り込みは無効になります。 リストに対する各操作は、同じスピンロックを使用して、リストに対する各操作が互いに同期されるようにする必要があります。 スピンロックは、これらの**Exinterlocked ロック*Xxx*リスト**ルーチンでのみ使用する必要があります。 その他の目的では、スピンロックを使用しないでください。 ドライバーは複数のリストに対して同じロックを使用できますが、この動作によってロックの競合が増加するため、ドライバーはこれを回避する必要があります。

たとえば、 **ExInterlockedInsertHeadList**、 **ExInterlockedInsertTailList**、および**ExInterlockedRemoveHeadList**ルーチンは、IRQL = パッシブ\_レベルで実行されているドライバースレッドによって、ダブルリンクリストの共有をサポートできます。DIRQL で実行されている ISR。 これらのルーチンは、スピンロックが保持されているときに割り込みを無効にします。 したがって、ISR とドライバーのスレッドは、デッドロックを損なうことなく、これらの**Exinterlocked ロック*Xxx*リスト**ルーチンへの呼び出しで同じスピンロックを安全に使用できます。

リスト操作のアトミックバージョンと非アトミックバージョンの呼び出しを同じリストに混在させないでください。 アトミックバージョンと非アトミックバージョンが同じリストで同時に実行されると、データ構造が破損し、コンピューターが応答を停止したり、バグチェック (*クラッシュ*) したりする可能性があります。 非アトミックルーチンの呼び出し中にスピンロックを取得することはできません。これにより、リスト操作のアトミックおよび非アトミックバージョンへの呼び出しが混在するのを回避できます。 この方法でのスピンロックの使用はサポートされていないため、リストが破損する可能性があります)。

### <a name="sequenced-singly-linked-lists"></a>シーケンスされた単一のリンクリスト

シーケンスされたシングルリンクリストは、アトミックな操作をサポートする単一のリンクリストを実装したものです。 Atomic 操作では、[単一](#singly-linked-lists)リンクリストに記述されている単一リンクリストの実装よりも効率的です。

配列形式の単一リンクリストの先頭を説明するために、また、一覧のエントリを説明するために使用されるのは、表示[ **\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)の[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)です。

ドライバーは、次のようにリストを操作します。

-   ExInitializeSListHead ヘッダーの構造を **\_** 初期化するには、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)を使用します。

-   一覧に新しいエントリを追加するには、新しいエントリを表すために、ExInterlockedPushEntrySList**エントリ\_** を割り当ててから、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)を呼び出してリストの先頭にエントリを追加します。

-   [**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)を使用して、リストの最初のエントリをポップします。

-   一覧を完全にクリアするには、 [**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedflushslist)を使用します。

-   リスト内のエントリの数を確認するには、 [**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerydepthslist)を使用します。

**次**のメンバーのみが含まれている、 [ **\_のエントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)。 リストに独自のデータを格納するには、次のように、リストエントリを記述する構造体のメンバーとして、表示 **\_エントリ**を埋め込みます。

```cpp
typedef struct 
{
  // driver-defined members
  .
  .
  .
  SLIST_ENTRY SListEntry;
  // other driver-defined members
  .
  .
  .

} XXX_ENTRY;
```

リストに新しいエントリを追加するには、 **XXX\_エントリ**構造を割り当ててから、 **SListEntry**メンバーへのポインターを**ExInterlockedPushEntrySList**に渡します。 **\_エントリ**へのポインターを、 **XXX\_エントリ**に変換するには、[**包含\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用します。 この手法の例として、シーケンス処理されていない単一のリンクリストを使用する方法については、「[単一リンクリスト](#singly-linked-lists)」を参照してください。

64ビットの Microsoft Windows オペレーティングシステムでは**警告**  、 [ **\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)構造は16バイトでアラインされている必要があります。

 

Windows XP 以降のバージョンの windows では、Windows 2000 では使用できない、シーケンスされた単一リンクリスト関数の最適化されたバージョンを提供しています。 ドライバーがこれらの機能を使用し、Windows 2000 でも実行する必要がある場合は、次のように、ドライバーで \_WIN2K\_COMPAT\_\_の使用フラグが設定されている必要があります。

```cpp
#define _WIN2K_COMPAT_SLIST_USAGE
```

X86 ベースのプロセッサの場合、このフラグを使用すると、コンパイラは Windows 2000 と互換性のある、シーケンスされた単一のリンクリスト関数のバージョンを使用します。

 

 




