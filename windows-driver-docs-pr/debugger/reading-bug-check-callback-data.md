---
title: バグ チェック コールバック データの読み取り
description: バグ チェック コールバック データの読み取り
ms.assetid: 638074bb-5133-4edc-86c5-33aafa837a0c
keywords:
- バグ チェックのコールバック データ
- コールバック データのバグ チェック、コールバックのデータを表示します。
- セカンダリのデータを表示する、バグのコールバック データを確認します
- セカンダリのバグ チェック コールバック データ
- バグ チェックでは、コールバック ルーチン
- IDebugDataSpaces3 dbgeng.h ヘッダー ファイル
- ReadTagged dbgeng.h ヘッダー ファイル
- StartEnumTagged dbgeng.h ヘッダー ファイル
- GetNextTagged dbgeng.h ヘッダー ファイル
ms.date: 10/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6803969949d640b9ac5215ce6014d9d7ea9070f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388570"
---
# <a name="reading-bug-check-callback-data"></a>バグ チェック コールバック データの読み取り


多くのドライバーを指定*バグ チェック コールバック ルーチン*します。 Windows のバグ チェックが問題と、システムのシャット ダウンする前にこれらのルーチンを呼び出します。 これらのルーチンを指定しと呼ばれるメモリ領域への書き込み*コールバック データ*と*セカンダリ コールバック データ*します。

<span id="BugCheckCallback"></span><span id="bugcheckcallback"></span><span id="BUGCHECKCALLBACK"></span>[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)  
このルーチンによって書き込まれたデータでは、コールバックのデータの一部になります。 クラッシュ ダンプ ファイルには、データが含まれていません。 

<span id="BugCheckSecondaryDumpDataCallback"></span><span id="bugchecksecondarydumpdatacallback"></span><span id="BUGCHECKSECONDARYDUMPDATACALLBACK"></span>[BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)  
このルーチンによって書き込まれたデータでは、セカンダリのコールバック データの一部になります。 クラッシュ ダンプ ファイルには、データが含まれます。

<span id="BugCheckAddPagesCallback"></span><span id="bugcheckaddpagescallback"></span><span id="BUGCHECKADDPAGESCALLBACK"></span>[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)  
このルーチンで指定したページでは、コールバックのデータの一部になります。 クラッシュ ダンプ ファイルには、これらのページ内のデータが含まれます。

コールバックとデバッガーの使用可能なセカンダリのコールバック データの量は、いくつかの要因によって異なります。

-   クラッシュしたシステムでは、によって既に書き込まれているコールバック データのライブ デバッグを実行している場合[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)またはで指定[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)使用できなくなります。 セカンダリ コールバック データはない固定メモリの任意の場所に格納されているため、できません。

-   コールバック データがで指定された完全メモリ ダンプまたはカーネル メモリ ダンプをデバッグする場合[BugCheckAddPagesCallback](https://go.microsoft.com/fwlink/p/?LinkID=254480)によって書き込まれたデータをセカンダリのコールバックと[BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)使用できます。 によって書き込まれたコールバック データ[BugCheckCallback](https://go.microsoft.com/fwlink/p/?LinkID=254479)は使用できません。 

-   最小メモリ ダンプをデバッグする場合、コールバック データは利用できません。 セカンダリのコールバック データが提供されます。

参照してください[カーネル モードのダンプ ファイルの変形](varieties-of-kernel-mode-dump-files.md)これら複数のダンプ ファイルのサイズの詳細についてはします。


## <span id="ddk_reading_bug_check_callback_data_dbg"></span><span id="DDK_READING_BUG_CHECK_CALLBACK_DATA_DBG"></span>


### <a name="span-iddisplaying-callback-dataspanspan-iddisplaying-callback-dataspandisplaying-callback-data"></a><span id="displaying-callback-data"></span><span id="DISPLAYING-CALLBACK-DATA"></span>コールバック データを表示します。

バグ チェック コールバック データを表示するには、使用することができます、 [ **! bugdump** ](-bugdump.md)拡張機能。

任意のパラメーターを指定せず[ **! bugdump** ](-bugdump.md)のすべてのコールバックのデータが表示されます。

特定のコールバック ルーチンを 1 つのデータを表示する使用[ **! bugdump**](-bugdump.md)*コンポーネント*ここで、*コンポーネント*いたのと同じパラメーターは、渡される**KeRegisterBugCheckCallback**ルーチンの登録時にします。

### <a name="span-iddisplaying-secondary-callback-dataspanspan-iddisplaying-secondary-callback-dataspandisplaying-secondary-callback-data"></a><span id="displaying-secondary-callback-data"></span><span id="DISPLAYING-SECONDARY-CALLBACK-DATA"></span>セカンダリのコールバック データを表示します。

セカンダリのコールバック データを表示するための 2 つの方法はあります。 使用することができます、 **.enumtag**コマンドは、独自のデバッガー拡張機能を記述できます。

セカンダリのコールバック データの各ブロックは、GUID タグによって識別されます。 このタグがで指定された、 **Guid**のフィールド、 **(KBUGCHECK\_セカンダリ\_ダンプ\_データ) ReasonSpecificData**に渡されるパラメーター [BugCheckSecondaryDumpDataCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)します。

[ **.Enumtag (セカンダリ コールバック データを列挙する)** ](-enumtag--enumerate-secondary-callback-data-.md)コマンドは、非常に正確な方法ではありません。 タグを表示して、16 進形式と ASCII 形式でデータを表示し、各セカンダリ データ ブロックが表示されます。 一般に、どのようなタグが実際に使用されているセカンダリのデータ ブロックの特定にのみ便利です。

このデータを使用して、実用的な方法で、独自のデバッガー拡張機能を記述することをお勧めします。 この拡張機能は、dbgeng.h ヘッダー ファイルでメソッドを呼び出す必要があります。 詳細については、次を参照してください。[デバッガー拡張機能の新規作成](writing-new-debugger-extensions.md)です。

セカンダリ データ ブロックのタグを GUID がわかっている場合、拡張機能がメソッドを使用する必要があります**IDebugDataSpaces3::ReadTagged**データにアクセスします。 そのプロトタイプは次のとおりです。

```cpp
STDMETHOD(ReadTagged)(
    THIS_
    IN LPGUID Tag,
    IN ULONG Offset,
    OUT OPTIONAL PVOID Buffer,
    IN ULONG BufferSize,
    OUT OPTIONAL PULONG TotalSize
    ) PURE; 
```

このメソッドを使用する方法の例を次に示します。

```cpp
UCHAR RawData[MY_DATA_SIZE];
GUID MyGuid = .... ;

Success = DataSpaces->ReadTagged(  &MyGuid,  0,  RawData,
                                   sizeof(RawData),  NULL); 
```

指定した場合、 *BufferSize*が小さすぎる**ReadTagged**は成功しますが、要求のバイト数ののみを記述*バッファー*します。 指定した場合、 *BufferSize*が大きすぎたりしたため**ReadTagged**は成功しますが、実際のブロック サイズのみを記述*バッファー*します。 ポインターを指定する場合*TotalSize*、 **ReadTagged**実際のブロックのサイズを返すに使用されます。 ブロックにアクセスできない場合**ReadTagged**はエラー状態コードを返します。

2 つのブロックには、同じ GUID のタグがある、最初の一致するブロックが返されます、2 番目のブロックにアクセスできなくなります。

使用することができます、ブロックの GUID のタグの確信できない場合、 **IDebugDataSpaces3::StartEnumTagged**、 **IDebugDataSpaces3::GetNextTagged**、および**IDebugDataSpaces3::EndEnumTagged**タグが付けられた要素を列挙するメソッド。 プロトタイプは次のとおりです。

```cpp
STDMETHOD(StartEnumTagged)(
    THIS_
    OUT PULONG64 Handle
    ) PURE;

STDMETHOD(GetNextTagged)(
    THIS_
    IN ULONG64 Handle,
    OUT LPGUID Tag,
    OUT PULONG Size
    ) PURE;

STDMETHOD(EndEnumTagged)(
    THIS_
    IN ULONG64 Handle
    ) PURE; 
```

### <a name="span-iddebugging-callback-routinesspanspan-iddebugging-callback-routinesspandebugging-callback-routines"></a><span id="debugging-callback-routines"></span><span id="DEBUGGING-CALLBACK-ROUTINES"></span>コールバック ルーチンのデバッグ

コールバック ルーチン自体をデバッグすることもできます。 コールバック ルーチン内のブレークポイントは、他のすべてのブレークポイントと同じように機能します。

コールバック ルーチンでは、2 番目のバグ チェックが発生する場合は、この新しいバグ チェックが最初に処理されます。 ただし、Windows では停止プロセスの特定の部分を繰り返されない — たとえば、2 番目のクラッシュ ダンプ ファイル書き込まれません。 ブルー スクリーンに表示される停止のコードは、2 番目のバグ チェックのコードになります。 カーネル デバッガーがアタッチされている場合両方のバグ チェックに関するメッセージは、通常は表示されます。

 

 





