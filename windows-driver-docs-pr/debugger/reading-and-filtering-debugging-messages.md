---
title: デバッグ メッセージの読み取りとフィルター処理
description: デバッグ メッセージの読み取りとフィルター処理
ms.assetid: 785469d2-30b8-4f73-b397-80bf89ed20ea
keywords:
- 読み取りとデバッグ メッセージをフィルター処理
- デバッグ メッセージの読み取り、およびフィルター処理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 944f36f07f24e7bb13446a4a078e035ede976d50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387068"
---
# <a name="reading-and-filtering-debugging-messages"></a>デバッグ メッセージの読み取りとフィルター処理


## <span id="ddk_reading_and_filtering_debugging_messages_dbg"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_DBG"></span>


カーネル モード コードを使用して、 **DbgPrintEx**と**KdPrintEx**デバッガーのカーネルへのメッセージを送信するためのルーチンは特定の条件下でだけを転送します。 これによりが必要ないメッセージをフィルター処理できます。

**注**  では、Windows Server 2003 および以前のバージョンの Windows、**による DbgPrint**と**KdPrint**カーネル デバッガーに無条件でメッセージを送信します。 Windows Vista および Windows では、これらのルーチンの送信などの条件付きでは、メッセージの以降のバージョンで**DbgPrintEx**と**KdPrintEx**します。 使用して Windows のどちらのバージョンを使用することをお勧め**DbgPrintEx**と**KdPrintEx**、ため、これらを使用するメッセージを送信する条件を制御できます。

 

これらのルーチンの完全なドキュメントについては、Windows Driver Kit を参照してください。

基本的な手順は次のとおりです。

**デバッグ メッセージをフィルター処理**

1.  デバッガーに送信するメッセージごとに、関数を使用して**DbgPrintEx**または**KdPrintEx**ドライバーのコードにします。 対象の適切なコンポーネント名を渡す、 *ComponentId*パラメーターに値を渡すと、*レベル*重大度またはこのメッセージの性質を反映するパラメーター。 メッセージが渡される、*形式*と*引数*パラメーターとして**printf**します。

2.  適切な値を設定*コンポーネント フィルター マスク*します。 各コンポーネントが別のマスク。マスクの値は、そのコンポーネントのメッセージのどれを表示するを示します。 レジストリ エディターを使用して、レジストリまたはカーネル デバッガーを使用してメモリ内で、コンポーネントのフィルターのマスクを設定できます。

3.  コンピューターにカーネル デバッガーをアタッチします。 毎回、ドライバーにメッセージを渡す**DbgPrintEx**または**KdPrintEx**に渡される値*ComponentId*と*レベル*になります対応するコンポーネントのフィルター マスクの値と比較します。 これらの値は、特定の条件を満たすため、メッセージが、カーネル デバッガーに送信し、表示されます。 それ以外の場合、メッセージは送信されません。

完全な詳細情報に従います。 このページにすべての参照**DbgPrintEx**に同様に適用**KdPrintEx**します。

### <a name="span-ididentifying-the-component-namespanspan-ididentifyingthecomponentnamespanidentifying-the-component-name"></a><span id="identifying-the-component-name"></span><span id="IDENTIFYING_THE_COMPONENT_NAME"></span>コンポーネント名を識別します。

各コンポーネントには、別個のフィルターのマスクがあります。 これにより、デバッガーは個別に各コンポーネントのフィルターを構成できます。

各コンポーネントは、コンテキストに応じて、さまざまな方法で参照されます。 *ComponentId*パラメーターの**DbgPrintEx**、コンポーネントの名前が付いて"DPFLTR\_「とのサフィックスが付いた」\_ID"。 レジストリで、コンポーネントのフィルターのマスクは、コンポーネント自体と同じ名前をが。 デバッガーで、コンポーネントのフィルターのマスクが付きます"Kd\_「とのサフィックスが付いた」\_マスク"。

すべてのコンポーネント名の完全な一覧がある (DPFLTR で\_*XXXX*\_ID の形式) では、Microsoft Windows Driver Kit (WDK) のヘッダー ntddk.h と Windows SDK のヘッダー ntrtl.h します。 これらのコンポーネントの名前のほとんどは、Windows と Microsoft によって作成されたドライバーに予約されています。

独立系ハードウェア ベンダーの予約は 6 つのコンポーネント名です。 Windows コンポーネントの出力とドライバーの出力の混在を回避するには、次のコンポーネント名のいずれかを使用する必要があります。

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
<td align="left"><p><strong>IHVVIDEO</strong></p></td>
<td align="left"><p>ビデオ ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVAUDIO</strong></p></td>
<td align="left"><p>オーディオ ドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVNETWORK</strong></p></td>
<td align="left"><p>ネットワークのドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVSTREAMING</strong></p></td>
<td align="left"><p>カーネル ドライバーをストリーミング</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVBUS</strong></p></td>
<td align="left"><p>バス ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVDRIVER</strong></p></td>
<td align="left"><p>他の種類のドライバー</p></td>
</tr>
</tbody>
</table>

 

たとえば、ビデオ ドライバーを作成する場合を使用する DPFLTR\_IHVVIDEO\_ID として、 *ComponentId*パラメーターの**DbgPrintEx**、値の名前を使用して、 **IHVVIDEO**レジストリを参照してください**Kd\_IHVVIDEO\_マスク**デバッガーでします。

Windows Vista および以降のバージョンの Windows では、すべてのメッセージの送信によって**による DbgPrint**と**KdPrint**に関連付けられている、**既定**コンポーネント。

### <a name="span-idchoosingthecorrectlevelspanspan-idchoosingthecorrectlevelspanchoosing-the-correct-level"></a><span id="choosing_the_correct_level"></span><span id="CHOOSING_THE_CORRECT_LEVEL"></span>適切なレベルを選択します。

*レベル*のパラメーター、 **DbgPrintEx**ルーチン、DWORD 型です。 これは、決定に使用、*重要度のビット フィールド*します。 間の接続、*レベル*パラメーターとこのビット フィールドのサイズに依存*レベル*:

-   場合*レベル*が 0 から 31 まで、ビット シフトとして解釈されるまでの数値と等しい。 重要度のビット フィールドが値 1 に設定されている&lt; &lt; *レベル*します。 0 ~ 31 の値を選択するため*レベル*正確に 1 つのビットが設定されたビット フィールドになります。 場合*レベル*は 0、ビット フィールドは 0x00000001; と同じ場合*レベル*は 31、ビット フィールドは 0x80000000 に相当します。

-   場合*レベル*32 ~ 0 xffffffff の包括的な重要度のビット フィールドがの値に設定されている数値は、*レベル*自体。

したがって、0x00004000 にビット フィールドを設定する場合を指定できます*レベル*0x00004000 または 14 です。 特定のビット フィールドの値がまったくゼロ、ビット フィールドを含む--このシステムによって実現されていないことに注意してください。

次の定数の値を設定する役に立ちます*レベル*します。 これらは、Microsoft Windows Driver Kit (WDK) のヘッダー ntddk.h と Windows SDK のヘッダー ntrtl.h で定義されます。

```cpp
#define   DPFLTR_ERROR_LEVEL     0
#define   DPFLTR_WARNING_LEVEL   1
#define   DPFLTR_TRACE_LEVEL     2
#define   DPFLTR_INFO_LEVEL      3
#define   DPFLTR_MASK    0x8000000
```

簡単な方法を使用して、*レベル*0、1、2、3 DPFLTR によって指定された意味を持つパラメーターが 0 と、bits を使用して - 31 の間の値を常に使用するが\_*XXXX*\_レベル、および他の使用選択したあらゆる項目を意味するビットです。

もう 1 つの簡単な方法を使用する、*レベル*パラメーターは、常に明示的なビット フィールドを使用します。 この方法を選択する場合は、することができます、または値 DPFLTR\_ビット フィールドを持つマスク。 これにより、誤って使用しない 32 未満の値。

重大なエラーが発生した場合は、ドライバーを Windows メッセージ レベルの使用方法に対応するためには、重要度のビット フィールドの最下位ビット (0x1) を設定する必要がありますのみ。 使用する場合*レベル*DPFLTR がこのプロパティの値未満の 32\_エラー\_レベル。 このビットが設定されている場合、メッセージは、ドライバーが実行されているコンピューターに、カーネル デバッガーがアタッチだれかがいつ表示しようとします。

適切な状況では、警告、トレース、および情報のレベルを使用してください。 目的で役立つその他のビットを自由に使用できます。 これにより、さまざまな選択的に表示または非表示にできるメッセージの種類を使用できます。

Windows Vista および以降のバージョンの Windows では、すべてのメッセージの送信によって**による DbgPrint**と**KdPrint**と同様に動作**DbgPrintEx**と**KdPrintEx**を使用してメッセージ*レベル*DPFLTR 等しく\_情報\_レベル。 つまり、これらのメッセージには、設定、重要度のビット フィールドの 3 番目のビットがあります。

### <a name="span-idsetting-the-component-filter-maskspanspan-idsettingthecomponentfiltermaskspansetting-the-component-filter-mask"></a><span id="setting-the-component-filter-mask"></span><span id="SETTING_THE_COMPONENT_FILTER_MASK"></span>コンポーネントのフィルターのマスクを設定

コンポーネントのフィルター マスクを設定する 2 つの方法はあります。

- コンポーネントのフィルターのマスクは、レジストリ キーにアクセスできる**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\デバッグ印刷フィルター**します。 レジストリ エディターを使用して、作成か、このキーを開きます。 このキーの下には、大文字で、必要なコンポーネントの名前と値を作成します。 コンポーネントのフィルター マスクとして使用する DWORD 値を等しく設定します。

- カーネル デバッガーがアクティブな場合は、コンポーネントのフィルターのマスク値シンボルに格納されているアドレスを逆参照によってアクセスできる**Kd\_**<em>XXXX</em>**\_マスク**ここで、 *XXXX*必要なコンポーネントの名前を指定します。 このマスクの値を表示するには WinDbg、KD をまたはに、 **dd (DWORD の表示)** コマンド、またはを新しいコンポーネント フィルター マスクを入力、 **ed (入力 DWORD)** コマンド。 シンボルのあいまいさの危険性がある場合としては、この記号を指定することがあります**nt!Kd\_**<em>XXXX</em>**\_マスク**します。

レジストリに格納されているフィルターのマスクは、ブート時にも反映されます。 デバッガーによって作成されたフィルターのマスクは、即座に有効と、Windows が再起動されるまでに保持されます。 レジストリに設定された値は、デバッガーによってオーバーライドできますが、コンポーネントのフィルターのマスクは、システムが再起動された場合に、レジストリで指定された値に戻ります。

呼ばれるシステム全体のマスクも**WIN2000**します。 これは、機能は、レジストリまたはその他のすべてのコンポーネントと同様に、デバッガーでは、既定では、0x1 と同じです。 各コンポーネントのフィルターのマスクで最初の論理和は、フィルター処理が実行されると、 **WIN2000**マスク。 具体的には、つまり、マスクされていないコンポーネントが 0x1 に既定値を指定すること。

### <a name="span-idcriteria-for-displayingthemessagespanspan-idcriteriafordisplayingthemessagespancriteria-for-displaying-the-message"></a><span id="criteria-for-displaying_the_message"></span><span id="CRITERIA_FOR_DISPLAYING_THE_MESSAGE"></span>メッセージを表示するための条件

ときに**DbgPrintEx**メッセージの重要度のビット フィールドで指定された比較、Windows カーネル モードのコードで呼び出される*レベル*によって指定されたコンポーネントのフィルターのマスクを含む*ComponentId*.

**注**  することを思い出してください、*レベル*パラメーターが 0 ~ 31 の範囲は、重要度のビット フィールドは 1 に等しい&lt; &lt; *レベル*が、 *レベル*パラメーターが 32 以上、重要度のビット フィールドは単に等しく*レベル*します。

 

Windows では、重要度のビット フィールドとコンポーネントのフィルター マスクで AND 演算を実行します。 結果が 0 以外の場合、メッセージは、デバッガーに送信されます。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次に例を示します。

最後の起動前に、次の値を作成するものとします、**デバッグ印刷フィルター**キー。

-   **IHVVIDEO**、DWORD 0x2 に等しい値を持つ

-   **IHVBUS**DWORD 0x7FF と等しく、

カーネル デバッガーで次のコマンドを発行するようになりました。

```dbgcmd
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

この時点では、 **IHVVIDEO** 0x8 のフィルターのマスクがコンポーネントには、 **IHVAUDIO** 0x7 のフィルターのマスクがコンポーネントには、および**IHVBUS**コンポーネントが 0x7FF のフィルターのマスク。

ただし、これらのマスクは自動的に論理和であるために、 **WIN2000** (これは通常 0x1 と等しい) システム全体のマスク、 **IHVVIDEO**マスクは 0x9 を効果的に等しい。 実際には、コンポーネントのフィルターがマスクが設定されていないすべての (たとえば、 **IHVSTREAMING**または**既定**) 0x1 のフィルター マスクする必要があります。

次の関数呼び出しがさまざまなドライバーで発生するものとします。

```cpp
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

最初のメッセージがその*レベル*DPFLTR パラメーター\_情報\_レベルで 3 であります。 これは、32 未満であるために、ビット シフト、0x8 の重要度、ビット フィールドでその結果として扱われます。 この値は、and 演算は有効な**IHVVIDEO** 0x9、0 以外の場合の結果のコンポーネントのフィルター マスク。 したがって、最初のメッセージは、デバッガーに送信されます。

2 番目のメッセージがその*レベル*7 と等しくパラメーター。 ここでも、これは、ビット シフト、0x80 の重要度、ビット フィールドでその結果として扱われます。 これはで and 演算を使用し、 **IHVAUDIO** 0x7、0 の結果のコンポーネントのフィルター マスク。 したがって、2 番目のメッセージは送信されません。

3 番目のメッセージがその*レベル*パラメーターと等しい DPFLTR\_マスク | 0x10。 これは、31 を超えるとそのための重要度のビット フィールドの値と等しく設定*レベル*- つまり、0x80000010 にします。 これはで and 演算を使用し、 **IHVBUS** 0x7FF、0 以外の場合の結果のコンポーネントのフィルター マスク。 したがって、3 番目のメッセージは、デバッガーに送信されます。

4 番目のメッセージに渡された**による DbgPrint**の代わりに**DbgPrintEx**します。 Windows Server 2003、Windows の以前のバージョンでは、このルーチンに渡されたメッセージが常に送信します。 Windows Vista および以降のバージョンの Windows では、このルーチンに渡されたメッセージは、既定のフィルターを常に付与されます。 重要度のビット フィールドは 1 に等しい&lt; &lt; DPFLTR\_情報\_0x00000008 のレベル。 このルーチンのコンポーネントが**既定**します。 設定していないため、**既定**コンポーネント フィルターのマスク値が 0x1 です。 これにより、重要度のビット フィールドを持つ and 演算が、結果は 0 です。 したがって、4 番目のメッセージは送信されません。

### <a name="span-idthe-dbgprint-bufferspanspan-idthedbgprintbufferspanthe-dbgprint-buffer"></a><span id="the-dbgprint-buffer"></span><span id="THE_DBGPRINT_BUFFER"></span>による DbgPrint バッファー

ときに**による DbgPrint**、 **DbgPrintEx**、 **KdPrint**、または**KdPrintEx**はメッセージを送信する書式設定された文字列を送信する、デバッガー、*による DbgPrint バッファー*します。 ほとんどの場合、デバッガー コマンド ウィンドウですぐにこのバッファーの内容が表示されます。 使用して、この表示を無効にすることができます、**バッファーによる DbgPrint 出力**グローバル フラグ ユーティリティ (gflags.exe) のオプション。 この表示は、ローカル カーネル デバッグ中に自動的には表示されません。

この表示は無効になっているローカル カーネル デバッグ、およびその他の時間、中にによる DbgPrint バッファーの内容のみ表示できるを使用して、 [ **! による dbgprint** ](-dbgprint.md)拡張機能コマンド。

任意の 1 への呼び出し**による DbgPrint**、 **DbgPrintEx**、 **KdPrint**、または**KdPrintEx** 512 バイトの情報は送信するだけです。 これは失われますよりも長く出力します。 による DbgPrint バッファー自体は、Windows の無料のビルドで最大 4 KB のデータを保持しを 32 KB のデータをチェックするビルドの Windows できます。 Windows Server 2003 および以降のバージョンの Windows で KDbgCtrl ツールを使用してによる DbgPrint バッファーのサイズを変更することができます。 参照してください[を使用して KDbgCtrl](using-kdbgctrl.md)詳細についてはします。

ため、メッセージがフィルター選択される場合、 *ComponentId*と*レベル*値、これは、デバッグ接続経由で送信されません。 したがって、デバッガーでこのメッセージを表示する方法はありません。

 

 





