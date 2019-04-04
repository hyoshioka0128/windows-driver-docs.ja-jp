---
title: タグを使用したオブジェクト参照トレース
description: タグを使用したオブジェクト参照トレース
ms.assetid: f6c3d7b2-09b1-4055-b066-cce8831efab2
keywords:
- オブジェクトにタグを付ける WDK を参照します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92cd71cca13a7d87fb4e981215cef0f6c593964a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580985"
---
# <a name="object-reference-tracing-with-tags"></a>タグを使用したオブジェクト参照トレース


[カーネル オブジェクト](managing-kernel-objects.md)プリミティブ データ オブジェクトをオペレーティング システムによって管理されているコンピューティング環境のさまざまな部分を表すシステム メモリ内で、Windows カーネルの実装です。 カーネル オブジェクトは、デバイス、ドライバー、ファイル、レジストリ キー、イベント、セマフォ、プロセス、スレッドなどの機能を表します。

ほとんどのカーネル オブジェクトが永続的ではできません。 非永続的カーネル オブジェクトがカーネル モード ドライバーを使用しますが、オブジェクトを削除することを防ぐために、ドライバーは、オブジェクトへの参照をカウントを取得できます。 ドライバーには、オブジェクトが不要、ドライバーは、オブジェクトへの参照を解放します。

ドライバーがオブジェクトへのすべての参照を解放しない場合は、オブジェクトの参照カウントをゼロにデクリメントでことはありませんし、オブジェクトは削除されません。 したがって、オブジェクト (たとえば、システム メモリ) によって使用されているシステム リソースは*リーク*します。 つまり、オペレーティング システムによって開始される次回まで使用できません。

参照エラーの別の型は、ドライバーの場合に発生します。*参照 *オブジェクト。 この場合、ドライバーはドライバーが実際に保持しているよりもオブジェクトを参照を解放します。 このエラーが発生すると、その他のクライアントはオブジェクトへのアクセス試行を続けている途中で、削除するオブジェクト。

リークとカーネル オブジェクトの不足の参照は、難しいバグを追跡するを指定できます。 たとえば、プロセス オブジェクトまたはデバイス オブジェクトは、数万の参照があります。 このような場合は、オブジェクト参照のバグの原因を特定することは難しい。

Windows 7 および Windows の以降のバージョンでは、オブジェクト参照をすると、これらのバグを見つけやすいようにタグ付けできます。 次のルーチンでは、取得とカーネル オブジェクトへの参照の解放とタグを関連付けます。

[**ObDereferenceObjectDeferDeleteWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff557732)

[**ObDereferenceObjectWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff557734)

[**ObReferenceObjectByHandleWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558683)

[**ObReferenceObjectByPointerWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558688)

[**ObReferenceObjectWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff558690)

たとえば、 **ObReferenceObjectWithTag**と**ObDereferenceObjectWithTag**、強化されたバージョンのでは Windows 7、Windows の以降のバージョンで利用可能な[ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)と[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)ルーチンは Windows 2000 以降のバージョンの Windows で利用できます。 これらの強化されたルーチンを使用すると、入力パラメーターとして、4 バイトのカスタム タグ値を指定できます。 呼び出しごとにタグの値に追加、[オブジェクト参照トレース](https://go.microsoft.com/fwlink/p/?linkid=153590)によってアクセスできる、 [Windows デバッグ ツール](https://go.microsoft.com/fwlink/p/?linkid=153599)します。 **ObReferenceObject**と**ObDereferenceObject**カスタム タグを指定する呼び出し元を有効にせずに、Windows 7 および Windows の以降のバージョンでは、これらのルーチンは、トレースを (タグ値"Dflt") を含む既定のタグを追加します。 そのため、呼び出しを**ObReferenceObject**または**ObDereferenceObject**への呼び出しと同じ効果**ObReferenceObjectWithTag**または**ObDereferenceObjectWithTag** "Dflt"のタグ値を指定します。 (プログラムでは、このタグの値として表されます 0x746c6644 または 'tlfD'。)

関連付けられている潜在的なオブジェクト リークや参照の不足を追跡しのセットを識別する**ObReferenceObject*Xxx*WithTag**と**ObDereferenceObject*Xxx*WithTag**をインクリメントおよびデクリメント、特定のオブジェクトの参照カウントは、ドライバーを呼び出します。 このセット内のすべての呼び出しに使用するには、一般的なタグ値 (たとえば、"Lky8") を選択します。 ドライバーが完了したらオブジェクト、デクリメントの数を使用する必要がありますインクリメント数正確に一致します。 これらの番号が一致しない場合、ドライバーは、オブジェクト参照のバグが。 デバッガーは、インクリメントおよびデクリメント各タグの値の数を比較し、一致しないかどうかに通知することができます。 この機能により、参照カウントの不一致の原因をすばやく特定できます。

デバッグ ツールの Windows ではオブジェクト参照のトレースを表示する、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)カーネル モード デバッガーの拡張機能。 Windows 7、Windows の以降のバージョンで、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)オブジェクト参照のトレースが有効になっている場合、拡張機能はオブジェクト参照のタグを表示できます。 既定では、オブジェクト参照のトレースは無効になります。 使用して、[グローバル フラグ エディター](https://go.microsoft.com/fwlink/p/?linkid=153601) (Gflags) オブジェクトの参照のトレースを有効にします。 Gflags の詳細については、[オブジェクト参照トレースの構成](https://go.microsoft.com/fwlink/p/?linkid=153602)を参照してください。

オブジェクト参照のトレースを有効にすると、によって生成される出力、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)拡張機能には、次の例として「タグ」列が含まれています。

```cpp
0: kd> !obtrace 0x8a226130
Object: 8a226130
 Image: leakyapp.exe
Sequence   (+/-)   Tag    Stack
--------   -----   ----   --------------------------------------------
      36    +1     Dflt      nt!ObCreateObject+1c4
                             nt!NtCreateEvent+93
                             nt!KiFastCallEntry+12a

      37    +1     Dflt      nt!ObpCreateHandle+1c1
                             nt!ObInsertObjectEx+d8
                             nt!ObInsertObject+1e
                             nt!NtCreateEvent+ba
                             nt!KiFastCallEntry+12a

      38    -1     Dflt      nt!ObfDereferenceObjectWithTag+22
                             nt!ObInsertObject+1e
                             nt!NtCreateEvent+ba
                             nt!KiFastCallEntry+12a

      39    +1     Lky8      nt!ObReferenceObjectByHandleWithTag+254
                             leakydrv!LeakyCtlDeviceControl+6c
                             nt!IofCallDriver+63
                             nt!IopSynchronousServiceTail+1f8
                             nt!IopXxxControlFile+6aa
                             nt!NtDeviceIoControlFile+2a
                             nt!KiFastCallEntry+12a

      3a    -1     Dflt      nt!ObfDereferenceObjectWithTag+22
                             nt!ObpCloseHandle+7f
                             nt!NtClose+4e
                             nt!KiFastCallEntry+12a
 
--------   -----   ----   --------------------------------------------
References: 3, Dereferences 2
Tag: Lky8 References: 1 Dereferences: 0 Over reference by: 1
```

この例では、最後の行が示す参照とタグが一致しない"Lky8"に関連付けられている数を逆参照し、この不一致の結果、過剰なによって参照されるいずれか (つまり、メモリ リーク)。

結果は、代わりに、過不足の参照の最後の行か、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)出力が次のようにあります。

```cpp
Tag: Lky8 References: 1 Dereferences: 2 Under reference by: 1
```

既定では、オペレーティング システムは、オブジェクトの解放後にオブジェクトのオブジェクト参照のトレースを削除することによってメモリを節約できます。 過小の参照を追跡するには、オブジェクトを解放した後も、トレースがメモリに格納されたままことが必要です。 この目的では、Gflags ツールは、コンピューターがシャット ダウンし、もう一度開始中にメモリ内でトレースを保持する「永続的な」オプションを提供します。

タグなしのオブジェクト参照のトレースは、Windows XP で導入されました。 トレースには、タグが含まれていないが、開発者はあまり便利な手法を使用して、オブジェクト参照のバグを特定する必要があります。 デバッガーは、オブジェクトの種類によって、開発者が選択されているオブジェクトのグループの参照を追跡できます。 開発者がオブジェクト参照のさまざまなソースを識別でき、逆参照は、唯一の方法は、その呼び出し履歴を比較するでした。 以前[! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)例には、特定の種類、プロセスなどのオブジェクトのスタック 5 つのみにはが含まれています ([**」プロセス**](eprocess.md)) オブジェクト、参照される場合が、数千回の逆参照します。 何千もスタックを検査するのでは、タグを使用せず、オブジェクトのリークまたは過小参照のソースを識別するために難しい場合があります。
