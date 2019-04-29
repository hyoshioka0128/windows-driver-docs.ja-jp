---
title: 片方向および双方向リンク リスト
description: 片方向および双方向リンク リスト
ms.assetid: 3a305f54-7866-4163-a3e4-e078d1927adc
keywords:
- シングル リンク リストの WDK カーネル
- ダブルリンク リスト WDK カーネル
- シングル リンク リストの WDK カーネルをシーケンス処理
- SINGLE_LIST_ENTRY
- LIST_ENTRY
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c36c7b617e22035e0ec52df045ddf14b3c37332
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331994"
---
# <a name="singly-and-doubly-linked-lists"></a>片方向および双方向リンク リスト





### <a name="singly-linked-lists"></a>シングル リンク リスト

オペレーティング システムを使用して、シングル リンク リストの組み込みサポートを提供する[**単一\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff563799)構造体。 シングル リンク リストは、リストの先頭といくつかの一覧のエントリで構成されます。 (一覧のエントリの数は 0、リストが空の場合) です。リストの各エントリとして表される、**単一\_一覧\_エントリ**構造体。 リストの先頭としても表される、**単一\_一覧\_エントリ**構造体。

各**単一\_一覧\_エントリ**構造に含まれる、 **[次へ]** メンバーを指す別**単一\_一覧\_エントリ**構造体。 **単一\_一覧\_エントリ**リストの先頭を表す構造体、 **[次へ]** メンバーの一覧で、最初のエントリが指すまたはリストが空の場合は NULL です。 **単一\_一覧\_エントリ**、リスト内のエントリを表す構造体、 **[次へ]** メンバー リストの次のエントリをポイントまたはこのエントリは、内の最後の場合は NULL に、リスト。

シングル リンク リストを操作するルーチンへのポインターを使用する、 [**単一\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff563799)リストの先頭を表します。 更新すること、**次**ことが操作の完了後の一覧の最初のエントリを指すポインター。

ものとします、 *ListHead*変数がへのポインター、**単一\_一覧\_エントリ**リストの先頭を表す構造体です。 ドライバー操作*ListHead*次のようにします。

-   空としてリストを初期化するには、次のように設定します。 *ListHead * * *-&gt;次** する**NULL**します。

-   一覧に新しいエントリを追加するには、割り当て、**単一\_一覧\_エントリ**を新しいエントリを表し、呼び出して[ **PushEntryList** ](https://msdn.microsoft.com/library/windows/hardware/ff559964)を追加する、リストの先頭のエントリ。

-   使用して、一覧から最初のエントリをポップ[ **PopEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff559712)します。

A**単一\_一覧\_エントリ**、単独でのみが、 **[次へ]** メンバー。 埋め込みのリストでは、独自のデータを格納する、**単一\_一覧\_エントリ**一覧のエントリを次のように記述する構造体のメンバーとして。

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

一覧に新しいエントリを追加するには、割り当て、 **XXX\_エントリ**構造体、しへのポインターを渡す、 **SingleListEntry**メンバー [ **PushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff559964). ポインターに変換する、**単一\_一覧\_エントリ**に戻す、 **XXX\_エントリ**を使用して、 [**含まれている\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff542043)します。 挿入し、シングル リンク リストからエントリのドライバーの定義を削除するルーチンの例を示します。

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

システムは、リストの操作の分割不可能なバージョンも用意されています[ **ExInterlockedPopEntryList** ](https://msdn.microsoft.com/library/windows/hardware/ff545408)と[ **ExInterlockedPushEntryList** ](https://msdn.microsoft.com/library/windows/hardware/ff545418). 各は、追加のスピン ロック パラメーターです。 ルーチンは、一覧を更新し、ルーチンはスピン ロックを解放の操作が完了したら、前に、スピン ロックを取得します。 ロックが保持されている間は、割り込みが無効です。 リストの各操作は、その他のすべての操作を一覧にこのような各操作が同期されていることを確認するのに同じスピン ロックを使用する必要があります。 これらでのみ、スピン ロックを使用する必要があります**ExInterlocked*Xxx*一覧**ルーチン。 その他の目的は、スピン ロックを使用しないでください。 ドライバーは、複数のリストの同じロックを使用することができますが、ドライバーは、これを避ける必要がありますので、この動作はロックの競合を増加します。

たとえば、 **ExInterlockedPopEntryList**と**ExInterlockedPushEntryList**ルーチンが IRQL で実行されているドライバーのスレッドによってシングル リンク リストの共有をサポートすることができます = パッシブ\_レベルDIRQL で実行されている ISR を選択します。 これらのルーチンは、スピン ロックが保持されているときに割り込みを無効にします。 したがって、ISR とドライバー スレッド安全に使用できる同じスピン ロックには、これらの呼び出しで**ExInterlocked*Xxx*一覧**デッドロック ルーチン。

同じリストにリスト操作の原子性と非アトミックなトランザクションのバージョンへの呼び出しを混在させないでください。 データ構造体が壊れている可能性になる場合は、アトミックと非アトミックなトランザクションのバージョンは、同じリストで同時に実行と、コンピューターが応答を停止する可能性がありますまたはバグのチェック (つまり、*クラッシュ*)。 (リスト操作の原子性と非アトミックなトランザクションのバージョンへの呼び出しを混在する代わりに非アトミック ルーチンの呼び出し中に、スピン ロックを取得できません。 スピン ロックを使用して、この方法ではサポートされていませんし、一覧の破損が発生する可能性がありますもします。)

システムには、効率的なアトミック シングル リンク リストの代替実装も提供します。 詳細については、次を参照してください。 [Sequenced シングル リンク リスト](#sequenced-singly-linked-lists)します。

### <a name="doubly-linked-lists"></a>ダブルリンク リスト

オペレーティング システムを使用して二重リンク リストの組み込みのサポートを提供します[**一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff554296)構造体。 ダブルリンク リストは、リストの先頭といくつかの一覧のエントリで構成されます。 (一覧のエントリの数は 0、リストが空の場合) です。リストの各エントリとして表される、**一覧\_エントリ**構造体。 リストの先頭としても表される、**一覧\_エントリ**構造体。

各**一覧\_エントリ**構造に含まれる、 **Flink**メンバーと**点滅**メンバー。 メンバーは両方ともへのポインター**一覧\_エントリ**構造体。

**一覧\_エントリ**リストの先頭を表す構造体、 **Flink**メンバーの一覧の最初のエントリが指す、**点滅**へのポインター、一覧の最後のエントリ。 リストが、空の場合**Flink**と**点滅**リストにリストのヘッド ポイントのヘッド自体。

**一覧\_エントリ**、リスト内のエントリを表す構造体、 **Flink**メンバーの一覧で、次のエントリが指す、**点滅**メンバー ポイント一覧の前のエントリ。 (エントリが一覧で、最後の 1 つである場合**Flink**リストの先頭を指します。 同様に、エントリが一覧で、1 つ目の場合、**点滅**リストの先頭を指します)。

(これらの規則は、一見驚くかもしれません、中に、許可一覧挿入と削除の操作を実装しない条件付きコードの分岐がある。)

ダブルリンク リストを操作するルーチンへのポインターを使用する、 [**一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff554296)リストの先頭を表します。 これらのルーチンを更新、 **Flink**と**点滅**をこれらのメンバーが、結果リストで最初と最後のエントリを指すようにリスト内のメンバーが移動します。

ものとします、 *ListHead*変数がへのポインター、**一覧\_エントリ**リストの先頭を表す構造体です。 ドライバー操作*ListHead*次のようにします。

-   空としてリストを初期化するために使用[ **InitializeListHead**](https://msdn.microsoft.com/library/windows/hardware/ff547799)、どの初期化*ListHead * * *-&gt;Flink** と*ListHead * * *-&gt;点滅** を指す*ListHead*します。

-   一覧の先頭に新しいエントリを挿入するには、割り当て、**一覧\_エントリ**を新しいエントリを表し、呼び出して[ **InsertHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff547820)でエントリを挿入するにはリストの先頭。

-   リストの末尾に新しいエントリを追加するには、割り当て、**一覧\_エントリ**を新しいエントリを表し、呼び出して[ **InsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff547823)でエントリを挿入するにはリストの末尾。

-   一覧から最初のエントリを削除するには使用[ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)します。 一覧から、または削除されたエントリへのポインターを返しますこれ*ListHead*リストが空の場合。

-   一覧から、最後のエントリを削除するには、使用[ **RemoveTailList**](https://msdn.microsoft.com/library/windows/hardware/ff561036)します。 一覧から、または削除されたエントリへのポインターを返しますこれ*ListHead*リストが空の場合。

-   一覧から指定されたエントリを削除するには使用[ **RemoveEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff561029)します。

-   リストが空かどうかを確認するには、使用[ **IsListEmpty**](https://msdn.microsoft.com/library/windows/hardware/ff551789)します。

-   一覧を別のリストの末尾に追加するには、使用[ **AppendTailList**](https://msdn.microsoft.com/library/windows/hardware/jj673018)します。

A [**一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff554296)、単独でのみが**点滅**と**Flink**メンバー。 埋め込みのリストでは、独自のデータを格納する、**一覧\_エントリ**一覧のエントリを次のように記述する構造体のメンバーとして。

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

一覧には、新しいエントリを追加するには、割り当て、 **XXX\_エントリ**構造体、しへのポインターを渡す、 **ListEntry**メンバー **InsertHeadList**または**InsertTailList**します。 ポインターに変換する、**一覧\_エントリ**に戻す、 **XXX\_エントリ**を使用して、 [**含まれている\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff542043). シングル リンク リストを使用して、この方法の例は、シングル リンク リスト上記を参照してください。

システムは、リストの操作の分割不可能なバージョンも用意されています[ **ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)、 [ **ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402)。、および[ **ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)します。 (アトミック版がないことに注意してください**RemoveTailList**または**RemoveEntryList**。)。各ルーチンでは、追加のスピン ロック パラメーターを受け取ります。 ルーチンは、一覧を更新する前に、スピン ロックを取得し、操作が完了したら、スピン ロックを解放します。 ロックが保持されている間は、割り込みが無効です。 リストの各操作は、他のすべてのリストに対してこのような各操作が同期されていることを確認するのに同じスピン ロックを使用する必要があります。 これらでのみ、スピン ロックを使用する必要があります**ExInterlocked*Xxx*一覧**ルーチン。 その他の目的は、スピン ロックを使用しないでください。 ドライバーは、複数のリストの同じロックを使用することができますが、ドライバーは、これを避ける必要がありますので、この動作はロックの競合を増加します。

たとえば、 **ExInterlockedInsertHeadList**、 **ExInterlockedInsertTailList**、および**ExInterlockedRemoveHeadList**ルーチンがの共有をサポートすることができます、二重IRQL で実行されているドライバーのスレッドでのリンクのリスト = パッシブ\_レベルと DIRQL で実行されている ISR します。 これらのルーチンは、スピン ロックが保持されているときに割り込みを無効にします。 したがって、ISR とドライバー スレッド安全に使用できる同じスピン ロックには、これらの呼び出しで**ExInterlocked*Xxx*一覧**デッドロック ルーチン。

同じリストにリスト操作の原子性と非アトミックなトランザクションのバージョンへの呼び出しを混在させないでください。 データ構造体が壊れて、アトミックと非アトミックなトランザクションのバージョンは、同じリストで同時に実行が場合と、コンピューターが応答を停止する可能性がありますまたはバグのチェック (つまり、*クラッシュ*)。 (作業することはできません、リスト操作の原子性と非アトミックなトランザクションのバージョンへの呼び出しの混在を回避するために非アトミック ルーチンの呼び出し中に、スピン ロックを取得します。 スピン ロックを使用して、この方法ではサポートされていませんし、一覧の破損が発生する可能性がありますもします。)

### <a name="sequenced-singly-linked-lists"></a>シングル リンク リストをシーケンス処理

シーケンス処理されたシングル リンク リストは、アトミックの操作をサポートするシングル リンク リストの実装です。 説明されているシングル リンク リストの実装よりもアトミック操作の方が効率的です[シングル リンク リスト](#singly-linked-lists)します。

[ **SLIST\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff563810)構造体を使用してシーケンス番号付きのシングル リンク リストの先頭を記述するときに[ **SLIST\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff563805)リスト内のエントリを記述するために使用します。

ドライバーでは、一覧を次のように操作します。

-   初期化するために、 **SLIST\_ヘッダー**構造体を使用して[ **ExInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff545321)します。

-   一覧に新しいエントリを追加するには、割り当て、 **SLIST\_エントリ**を新しいエントリを表し、呼び出して[ **ExInterlockedPushEntrySList** ](https://msdn.microsoft.com/library/windows/hardware/ff545422)にエントリを追加するにはリストの先頭。

-   使用して、一覧から最初のエントリをポップ[ **ExInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545414)します。

-   使用して一覧を完全に消去する[ **ExInterlockedFlushSList**](https://msdn.microsoft.com/library/windows/hardware/ff545379)します。

-   一覧のエントリの数を調べるには[ **ExQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff545502)します。

A [ **SLIST\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff563805)、単独でのみが、**次**メンバー。 埋め込みのリストでは、独自のデータを格納する、 **SLIST\_エントリ**一覧のエントリを次のように記述する構造体のメンバーとして。

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

一覧に新しいエントリを追加するには、割り当て、 **XXX\_エントリ**構造体、しへのポインターを渡す、 **SListEntry**メンバー **ExInterlockedPushEntrySList**. ポインターに変換する、 **SLIST\_エントリ**に戻す、 **XXX\_エントリ**を使用して、 [**含まれている\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff542043). 単独 非シーケンス処理を使用して、この手法の例では、リストがリンクされたを参照してください。[シングル リンク リスト](#singly-linked-lists)します。

**警告**   64 ビット用の Microsoft Windows オペレーティング システム、 [ **SLIST\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff563805)構造体は 16 バイトでアラインである必要があります。

 

Windows XP および Windows の以降のバージョンは、Windows 2000 では使用できないシングル リンク リストをシーケンス処理された関数の最適化されたバージョンを提供します。 場合は、ドライバーは、これらの関数を使用しも、Windows 2000 で実行する必要があります、ドライバーを定義する必要があります、 \_WIN2K\_COMPAT\_SLIST\_使用法フラグの次のようにします。

```cpp
#define _WIN2K_COMPAT_SLIST_USAGE
```

X86 ベースのプロセッサでは、このフラグとコンパイラ バージョンの Windows 2000 と互換性があるシーケンス処理されたシングル リンク リスト関数を使用します。

 

 




