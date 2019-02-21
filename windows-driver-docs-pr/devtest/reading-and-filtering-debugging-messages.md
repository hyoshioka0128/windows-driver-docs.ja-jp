---
title: 読み取りとデバッグ メッセージをフィルター処理
description: 読み取りとデバッグ メッセージをフィルター処理
ms.assetid: 2ad320f6-596d-4b4c-bfad-d570c856bcc7
keywords:
- メッセージを読み取る WDK コードのデバッグ
- メッセージのフィルタ リング WDK コードのデバッグ
- デバッグ メッセージの読み取り
- WDK のデバッグ メッセージをフィルター処理
- WDK のデバッグ ルーチン、メッセージのフィルター処理
- フィルターは、WDK のデバッグをマスク
- コンポーネント名の WDK のデバッグ
- 重要度のビット フィールドの WDK のデバッグ
- レベル WDK のデバッグ
- レベル パラメーター
- デバッグ メッセージを表示します。
- WDK のデバッグ メッセージの優先順位付け
- による DbgPrint バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07e170eb85e507cd893ed3b86dbdc23b3722f216
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535379"
---
# <a name="reading-and-filtering-debugging-messages"></a>読み取りとデバッグ メッセージをフィルター処理


## <span id="ddk_reading_and_filtering_debugging_messages_tools"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_TOOLS"></span>


[ **DbgPrintEx**](https://msdn.microsoft.com/library/windows/hardware/ff543634)、 [ **vDbgPrintEx**](https://msdn.microsoft.com/library/windows/hardware/ff556075)、 [ **vDbgPrintExWithPrefix** ](https://msdn.microsoft.com/library/windows/hardware/ff556076)、および[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)ルーチンでは、指定した条件下でカーネル デバッガーにメッセージを送信します。 この手順では、優先順位の低いメッセージをフィルター処理することができます。

**注**   Microsoft Windows Server 2003、Windows の以前のバージョン、 [**による DbgPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff543632)と[ **KdPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff548092)ルーチンのメッセージからカーネル デバッガーの無条件に送信します。 Windows Vista および Windows では、これらのルーチンの送信などの条件付きでは、メッセージの以降のバージョンで**DbgPrintEx**と**KdPrintEx**します。 Windows のどちらのバージョンを使用する必要がありますを使用する**DbgPrintEx**、 **vDbgPrintEx**、 **vDbgPrintExWithPrefix**、および**KdPrintEx**これらのルーチンでは、メッセージを送信する条件を制御できるようにするためです。

 

**デバッグ メッセージをフィルター処理**

1.  デバッガーに送信するメッセージごとに、使用**DbgPrintEx**、 **vDbgPrintEx**、 **vDbgPrintExWithPrefix**、または**KdPrintEx**ドライバーのコード。 対象の適切なコンポーネント名を渡す、 *ComponentId*パラメーターに値を渡すと、*レベル*重大度またはこのメッセージの性質を反映するパラメーター。 メッセージが渡される、*形式*と*引数*パラメーターと同じ構文を使用して**printf**します。

2.  適切な値を設定*コンポーネント フィルター マスク*します。 各コンポーネントには、別のマスクがあります。 マスクの値は、そのコンポーネントのメッセージの表示を示します。 できますマスクを設定する、コンポーネント フィルター レジストリにレジストリ エディターを使用して、またはメモリのカーネル デバッガーを使用しています。

3.  コンピューターにカーネル デバッガーをアタッチします。 ドライバーへのメッセージを通過するたびに**DbgPrintEx**、 **vDbgPrintEx**、 **vDbgPrintExWithPrefix**、または**KdPrintEx**、渡される値*ComponentId*と*レベル*対応するコンポーネントのフィルター マスクの値と比較されます。 これらの値は、特定の条件を満たすため、メッセージは、カーネル デバッガーに送信し、表示されます。 それ以外の場合、メッセージは送信されません。

詳細については、次のセクションを参照してください。

**注**  このページにすべての参照**DbgPrintEx**に同様に適用**KdPrintEx**、 **vDbgPrintEx**、および**vDbgPrintExWithPrefix**します。

 

-   [コンポーネント名を識別します。](#identifying-the-component-name)
-   [適切なレベルを選択します。](#choosing-the-correct-level)
-   [コンポーネントのフィルターのマスクを設定](#setting-the-component-filter-mask)
-   [メッセージを表示するための条件](#criteria-for-displaying-the-message)
-   [例](#example)
-   [による DbgPrint バッファーとデバッガー](#dbgprint-buffer-and-the-debugger)

### <a name="identifying-the-component-name"></a>コンポーネント名を識別します。

各コンポーネントには、別個のフィルターのマスクがあります。 このマスクは、個別に各コンポーネントのフィルターを構成するデバッガーを使用できます。

各コンポーネントは、コンテキストに応じて、さまざまな方法で参照されます。 *ComponentId*パラメーターの**DbgPrintEx**、コンポーネントの名前が付いて"DPFLTR\_「とのサフィックスが付いた」\_ID"。 レジストリで、コンポーネントのフィルターのマスクは、コンポーネント自体と同じ名前をが。 デバッガーで、コンポーネントのフィルターのマスクが付きます"Kd\_「とのサフィックスが付いた」\_マスク"。

コンポーネント名の完全な一覧がある (DPFLTR で\_*XXXX*\_ID の形式) Dpfilter.h ヘッダー ファイルで Windows Driver Kit (WDK) にします。 これらのコンポーネントの名前のほとんどは、Windows と Microsoft によって書き込まれるドライバーに予約されています。

独立系ハードウェア ベンダーに予約されている 6 つのコンポーネント名があります。 Windows コンポーネントの出力とドライバーの出力の混在を回避するには、次のコンポーネント名のいずれかを使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネント名</th>
<th align="left">ドライバーの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IHVVIDEO</p></td>
<td align="left"><p>ビデオ ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVAUDIO</p></td>
<td align="left"><p>オーディオ ドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVNETWORK</p></td>
<td align="left"><p>ネットワークのドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVSTREAMING</p></td>
<td align="left"><p>カーネル ドライバーをストリーミング</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHVBUS</p></td>
<td align="left"><p>バス ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHVDRIVER</p></td>
<td align="left"><p>他の種類のドライバー</p></td>
</tr>
</tbody>
</table>

 

たとえば、ビデオ ドライバーを作成する場合を使用する DPFLTR\_IHVVIDEO\_ID として、 *ComponentId*パラメーターの**DbgPrintEx**値で IHVVIDEO の名前を使用します、レジストリを参照してください**Kd\_IHVVIDEO\_マスク**デバッガーでします。

Windows Vista および以降のバージョンの Windows では、すべてのメッセージを**による DbgPrint**と**KdPrint**送信は、既定のコンポーネントに関連付けられます (DPFLTR\_既定\_ID)。

### <a name="choosing-the-correct-level"></a>適切なレベルを選択します。

*レベル*のパラメーター、 **DbgPrintEx**ルーチン、DWORD 型です。 これは、決定に使用、*重要度のビット フィールド*します。 間の接続、*レベル*パラメーターとこのビット フィールドのサイズに依存*レベル*:

-   場合*レベル*が 0 から 31 まで、重要度のビット フィールドは、ビット シフトとして解釈されるまでの数値と等しい。 重要度のビット フィールドが値 1 に設定されている&lt; &lt; *レベル*します。 したがって、0 ~ 31 の値を選択するかどうかは*レベル*、ビット フィールドが正確に 1 つのビットが設定されます。 場合*レベル*が 0 のビット フィールドは、0x00000001 に相当場合、します。 場合*レベル*は 31、ビット フィールドは 0x80000000 に相当します。

-   場合*レベル*32 ~ 0 xffffffff の包括的な重要度のビット フィールドの値が設定されている数値は、*レベル*自体。

したがって、0x00004000 に、ビット フィールドを設定する場合を指定できます*レベル*0x00004000 または 14 です。 このシステムでは、その完全 0 ビット フィールドを含む--いくつかのビット フィールドの値を生成できないことです。

次の定数の値を設定する役に立ちます*レベル*します。 Dpfilter.h WDK のヘッダー ファイルで定義されています。

```ManagedCPlusPlus
#define DPFLTR_ERROR_LEVEL 0
#define DPFLTR_WARNING_LEVEL 1
#define DPFLTR_TRACE_LEVEL 2
#define DPFLTR_INFO_LEVEL 3
#define DPFLTR_MASK 0x80000000
```

簡単な方法を使用して、*レベル*パラメーターは、常に 0 ~ 31--DPFLTR で指定された意味を持つビット 0、1、2、および 3 を使用して値を使用する\_*XXXX*\_を使用して、レベル、選択したあらゆる項目を意味するビットが他のです。

もう 1 つの簡単な方法を使用する、*レベル*パラメーターは、常に明示的なビット フィールドを使用します。 この方法を選択する場合は、DPFLTR 値のビットごとの OR を使用する可能性がある\_ビット フィールドをマスクします。 この値はにより、誤って使用しない 32 未満の値。

ドライバーを Windows がメッセージ レベルを使用する方法と互換性のあるさせるには、重大なエラーが発生した場合にだけ、最下位ビット (0x1) の重要度のビット フィールドを設定してください。 使用する場合*レベル*値 32 よりも小さいか、この値は、DPFLTR に対応して\_エラー\_レベル。 重要度のビット フィールドが設定されている場合、メッセージには、カーネル デバッガーをアタッチします、ドライバーが実行されているコンピューターにだれかが、必ずが表示します。

適切な状況で、警告、トレース、および情報のレベルを使用します。 目的で役立つその他のビットを使用できます。 この機能を使用すると、さまざまな選択的に表示または非表示にできるメッセージの種類があることができます。

Windows Vista および以降のバージョンの Windows では、すべてのメッセージの送信によって**による DbgPrint**と**KdPrint**と同様に動作**DbgPrintEx**と**KdPrintEx**を使用してメッセージ*レベル*DPFLTR 等しく\_情報\_レベル。 つまり、これらのメッセージには、設定、重要度のビット フィールドの 3 番目のビットがあります。

### <a name="setting-the-component-filter-mask"></a>コンポーネントのフィルターのマスクを設定

コンポーネントのフィルター マスクを設定する 2 つの方法はあります。

- 対象のコンピューターにはコンポーネントのフィルター マスクのレジストリ キーにアクセスできる**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\印刷フィルターをデバッグ**します。 レジストリ エディターを使用して、作成か、このキーを開きます。 このキーの下、大文字で、必要なコンポーネントの名前と値を作成します (たとえば、**既定**または**IHVDRIVER**)。 この値をコンポーネントのフィルター マスクとして使用する DWORD の値に設定 (DPFLTR を表示するなど、0x8\_情報\_DPFLTR だけでなく、レベルのメッセージ\_エラー\_レベルを 0 xf にマスクを設定またはすべてのメッセージを表示)。

- カーネル デバッガーがアクティブな場合は、コンポーネントのフィルターのマスク値シンボルに格納されているアドレスを逆参照によってアクセスできる**Kd\_**<em>XXXX</em>  **\_マスク**ここで、 *XXXX*必要なコンポーネントの名前を指定します。 このマスクの値を表示するには WinDbg、KD をまたはに、 **dd (DWORD の表示)** コマンド、またはを新しいコンポーネント フィルター マスクを入力、 **ed (入力 DWORD)** コマンド。 シンボルのあいまいさの危険性がある場合としては、この記号を指定する場合があります**nt!Kd\_**<em>XXXX</em>**\_マスク**します。

レジストリに格納されているフィルター マスクは、ブート時にも反映されます。 デバッガーによって作成されるフィルターのマスクは、すぐに有効と、ターゲット コンピューターが再起動されるまでに保持されます。 デバッガーは、レジストリで設定されている値をオーバーライドできますが、ターゲット コンピューターを再起動した場合、レジストリで指定されている値に、コンポーネントのフィルターのマスクを返します。

WIN2000 と呼ばれるシステム全体のマスクもあります。 既定では、このマスクが 0x1 と等しいが、レジストリやその他のすべてのコンポーネントのようにデバッガーを変更することができます。 フィルター処理が実行されると、各コンポーネントのフィルターのマスクは WIN2000 マスクとビットごとの OR を使用して最初に組み合わされます。 具体的には、この組み合わせはマスクされていないコンポーネントが 0x1 に既定値を指定することを意味します。

### <a name="criteria-for-displaying-the-message"></a>メッセージを表示するための条件

ときに**DbgPrintEx**と呼ばれるは、Windows カーネル モードのコードで指定されたメッセージの重要度のビット フィールドを比較します*レベル*で指定されているコンポーネントのフィルターのマスクを含む*ComponentId*します。

**注**  することを思い出してください、*レベル*パラメーターが 0 ~ 31 の範囲は、重要度のビット フィールドは 1 に等しい&lt; &lt; *レベル*します。 しかし、*レベル*パラメーターが 32 以上、重要度のビット フィールドは単に等しく*レベル*します。

 

Windows では、重要度のビット フィールドとコンポーネントのフィルター マスクで AND 演算を実行します。 結果が 0 以外の場合、メッセージは、デバッガーに送信されます。

### <a name="example"></a>例

最後の起動前に、次の値を作成するものとします、**デバッグ印刷フィルター**キー。

-   IHVVIDEO、DWORD 0x2 に等しい値が使用されます。

-   IHVBUS、DWORD 0x7FF を等しくします。

カーネル デバッガーで次のコマンドを発行するようになりました。

```
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

この時点では、IHVVIDEO コンポーネントが 0x8 のフィルターのマスク、IHVAUDIO コンポーネントには、0x7 のフィルターのマスクおよび IHVBUS コンポーネントが 0x7FF のフィルターのマスク。

ただし、これらのマスクは、ビットごとの OR を使用して (これは通常 0x1 と等しい) WIN2000 システム全体のマスクと組み合わせて自動的には、ので、IHVVIDEO マスクは効果的に 0x9 です。 コンポーネントのフィルターがマスクがすべての設定されていない (たとえば、IHVSTREAMING または既定の) 0x1 のフィルターのマスクを持ちます。

次の関数呼び出しがさまざまなドライバーで発生するものとします。

```
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

最初のメッセージがその*レベル*DPFLTR パラメーター\_情報\_レベルで 3 であります。 この値は、32 未満であるため、重要度のビット フィールド 0x8 の結果として、ビット シフトとして扱われます。 0x9 の効果的な IHVVIDEO コンポーネント フィルター マスクとは、この値は 0 以外の場合の結果、AND 演算を使用して結合されます。 したがって、最初のメッセージは、デバッガーに送信されます。

2 番目のメッセージがその*レベル*7 と等しくパラメーター。 ここでも、この値は、ビット シフト、0x80 の重要度のビット フィールドでその結果として扱われます。 この値は、0 の結果、AND 演算を使用して、0x7 の IHVAUDIO コンポーネント フィルター マスクと組み合わされます。 したがって、2 番目のメッセージは送信されません。

3 番目のメッセージがその*レベル*パラメーターと等しい DPFLTR\_マスク | 0x10。 この値は 31 より大きいと、そのための重要度のビット フィールドの値と等しく設定*レベル*-つまり、0x80000010 にします。 この値は、0 以外の場合の結果、AND 演算を使用して、0x7FF の IHVBUS コンポーネント フィルター マスクと結合されています。 したがって、3 番目のメッセージは、デバッガーに送信されます。

4 番目のメッセージに渡された、**による DbgPrint**ルーチンの代わりに、 **DbgPrintEx**ルーチン。 Windows Server 2003 および Windows に渡されるメッセージの以前のバージョンで**による DbgPrint**は常に送信されます。 Windows Vista および Windows に渡されるメッセージの以降のバージョンで**による DbgPrint**は常に既定のフィルターを指定します。 重要度のビット フィールドは 1 に等しい&lt; &lt; DPFLTR\_情報\_0x00000008 のレベル。 このルーチンのコンポーネントは、既定値です。 既定のコンポーネントのフィルターのマスクを設定していないために、0x1 の値を持ちます。 このマスクは、AND 演算を使用して重要度のビット フィールドと組み合わせて、結果は 0 です。 したがって、4 番目のメッセージは送信されません。

### <a name="dbgprint-buffer-and-the-debugger"></a>による DbgPrint バッファーとデバッガー

ときに、**による DbgPrint**、 **DbgPrintEx**、 **vDbgPrintEx**、 **vDbgPrintExWithPrefix**、 **KdPrint**、または**KdPrintEx**ルーチンでは、デバッガーに、メッセージを送信、書式設定された文字列を送信する、**による DbgPrint**バッファー。 このバッファーの内容に直ちに反映されますデバッガー コマンド ウィンドウを使用してこの表示を無効にしない限り、**バッファーによる DbgPrint 出力**GFlags のオプション。

使用してのみによる DbgPrint バッファーの内容を表示するにはこの表示を無効にした場合、 **! による dbgprint**拡張機能コマンド。 デバッガーの拡張機能については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

任意の 1 への呼び出し**による DbgPrint**、 **DbgPrintEx**、 **vDbgPrintEx**、 **vDbgPrintExWithPrefix**、 **KdPrint**、または**KdPrintEx** 512 バイトのみの情報を送信します。 すべての出力 512 バイトを超えるは失われます。 による DbgPrint バッファー自体は、Windows の無料のビルドで最大 4 KB のデータを保持しを 32 KB のデータをチェックするビルドの Windows できます。 Windows Server 2003 および以降のバージョンの Windows で KDbgCtrl ツールを使用してによる DbgPrint バッファーのサイズを変更することができます。 このツールは、Windows のツールのデバッグの一部です。

ため、メッセージがフィルター選択される場合、 *ComponentId*と*レベル*値、これは、デバッグ接続経由で送信されません。 そのため、デバッガーでこのメッセージを表示する方法はありません。

 

 





