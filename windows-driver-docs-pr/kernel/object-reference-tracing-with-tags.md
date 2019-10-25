---
title: タグを使用したオブジェクト参照のトレース
description: タグを使用したオブジェクト参照のトレース
ms.assetid: f6c3d7b2-09b1-4055-b066-cce8831efab2
keywords:
- タグを使用して参照するオブジェクト (WDK)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f35ef50124cb09b18dea3111b8402a4d9f39879
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838531"
---
# <a name="object-reference-tracing-with-tags"></a>タグを使用したオブジェクト参照のトレース


[カーネルオブジェクト](managing-kernel-objects.md)は、オペレーティングシステムによって管理されるコンピューティング環境のさまざまな部分を表すために、Windows カーネルがシステムメモリに実装するプリミティブデータオブジェクトです。 カーネルオブジェクトは、デバイス、ドライバー、ファイル、レジストリキー、イベント、セマフォ、プロセス、スレッドなどの機能を表します。

ほとんどのカーネルオブジェクトは永続的ではありません。 カーネルモードドライバーがオブジェクトを使用している間に非永続的 kernel オブジェクトが削除されないようにするために、ドライバーはオブジェクトへのカウントされた参照を取得できます。 ドライバーがオブジェクトを必要としなくなった場合、ドライバーはオブジェクトへの参照を解放します。

ドライバーがオブジェクトへのすべての参照を解放しない場合、オブジェクトの参照カウントは0まで減少せず、オブジェクトは削除されません。 そのため、オブジェクトによって使用されているシステムリソース (システムメモリなど) が*リーク*しています。 つまり、次にオペレーティングシステムが起動するまで使用できません。

の下のドライバーがオブジェクトを*参照*している場合は、別の種類の参照エラーが発生します。 この場合、ドライバーは、ドライバーが実際に保持しているよりも多くの参照を解放します。 このエラーが発生すると、他のクライアントが引き続きオブジェクトにアクセスしようとしている間に、オブジェクトが途中で削除される可能性があります。

カーネルオブジェクトのリークや参照が原因で、バグを追跡するのが困難な場合があります。 たとえば、プロセスオブジェクトまたはデバイスオブジェクトには、数十の参照が含まれている場合があります。 このような状況では、オブジェクト参照のバグの原因を特定することが困難な場合があります。

Windows 7 以降のバージョンの Windows では、オブジェクト参照をタグ付けして、これらのバグを簡単に見つけられるようにすることができます。 次のルーチンは、カーネルオブジェクトへの参照の取得と解放にタグを関連付けます。

[**ObDereferenceObjectDeferDeleteWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectdeferdeletewithtag)

[**ObDereferenceObjectWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectwithtag)

[**ObReferenceObjectByHandleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandlewithtag)

[**Obreferenceobjectbyポインター Withtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointerwithtag)

[**ObReferenceObjectWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectwithtag)

たとえば、Windows 7 以降のバージョンの Windows で使用できる**Obreferenceobjectwithtag**と**ObDereferenceObjectWithTag**は、 [**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)および[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)ルーチンの拡張バージョンです。 windows 2000 以降のバージョンの Windows で使用できます。 これらの拡張ルーチンを使用すると、入力パラメーターとして4バイトのカスタムタグ値を指定できます。 各呼び出しのタグ値は、 [Windows デバッグツール](https://go.microsoft.com/fwlink/p/?linkid=153599)によってアクセスできる[オブジェクト参照トレース](https://go.microsoft.com/fwlink/p/?linkid=153590)に追加されます。 **Obreferenceobject**と**ObDereferenceObject**は、呼び出し元がカスタムタグを指定することを有効にしませんが、windows 7 以降のバージョンの windows では、これらのルーチンによって、既定のタグ (タグ値 "Dflt") がトレースに追加されます。 このため、 **Obreferenceobject**または**ObDereferenceObject**の呼び出しは、"Dflt" というタグ値を指定する**Obreferenceobjectwithtag**または**ObDereferenceObjectWithTag**の呼び出しと同じ効果があります。 (プログラムでは、このタグ値は0x746c6644 または ' tlfD ' として表されます)。

潜在的なオブジェクトリークまたは参照下を追跡するには、関連付けられている**Obreferenceobject*Xxx*Withtag**呼び出しと**ObDereferenceObject*Xxx*withtag**呼び出しのセットをドライバー内で識別して、参照をインクリメントおよびデクリメントします。特定のオブジェクトの数。 このセット内のすべての呼び出しに使用する共通のタグ値 (たとえば、"Lky8") を選択します。 オブジェクトを使用してドライバーが終了した後、デクリメントの数は、インクリメントの数と正確に一致している必要があります。 これらの数値が一致しない場合、ドライバーにはオブジェクト参照のバグがあります。 デバッガーでは、各タグ値のインクリメントとデクリメントの数を比較し、一致していないかどうかを通知できます。 この機能を使用すると、参照カウントの不一致の原因をすばやく特定できます。

Windows デバッグツールでオブジェクト参照のトレースを表示するには、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)カーネルモードのデバッガー拡張機能を使用します。 Windows 7 以降のバージョンの Windows では、オブジェクト参照トレースが有効になっている場合、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)拡張機能でオブジェクト参照タグを表示できます。 既定では、オブジェクト参照のトレースは無効になっています。 [グローバルフラグエディター](https://go.microsoft.com/fwlink/p/?linkid=153601) (Gflags) を使用して、オブジェクト参照のトレースを有効にします。 Gflags の詳細については、「[オブジェクト参照トレースの構成](https://go.microsoft.com/fwlink/p/?linkid=153602)」を参照してください。

オブジェクト参照のトレースを有効にすると、次の例に示すように、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)拡張機能によって生成される出力には、"Tag" 列が含まれます。

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

この例の最後の行は、"Lky8" タグに関連付けられている参照と逆参照の数が一致しないこと、およびこの不一致の結果が 1 (リーク) で参照されていることを示しています。

結果が代わりに参照された場合、 [! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)出力の最後の行は次のようになります。

```cpp
Tag: Lky8 References: 1 Dereferences: 2 Under reference by: 1
```

既定では、オブジェクトが解放された後にオブジェクトのオブジェクト参照トレースを削除することによって、メモリが節約されます。 参照下を追跡するには、オブジェクトが解放された後もトレースがメモリに格納されたままになっている必要があります。 この目的のために、Gflags ツールには "永続的" オプションが用意されています。このオプションは、コンピューターのシャットダウン中にトレースをメモリ内に保持し、再起動します。

タグのないオブジェクト参照のトレースは、Windows XP で導入されました。 トレースにはタグが含まれていなかったため、開発者はオブジェクト参照のバグを識別するために、より簡単な手法を使用する必要がありました。 デバッガーは、オブジェクトの種類によって選択された開発者がオブジェクトのグループの参照を追跡できます。 開発者がオブジェクト参照と逆参照のさまざまなソースを特定する唯一の方法は、呼び出し履歴を比較することでした。 前の[! obtrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/-obtrace)の例には5つのスタックしか含まれていませんが、Process ([**eprocess**](eprocess.md)) オブジェクトなど、特定の種類のオブジェクトが参照され、何千も逆参照される可能性があります。 何千ものスタックを検査することで、タグを使用せずにオブジェクトのリークの原因や参照下を特定することが困難になる場合があります。
