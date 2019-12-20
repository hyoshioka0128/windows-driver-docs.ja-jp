---
title: デバッグ メッセージの読み取りとフィルター処理
description: デバッグ メッセージの読み取りとフィルター処理
ms.assetid: 785469d2-30b8-4f73-b397-80bf89ed20ea
keywords:
- デバッグメッセージの読み取りとフィルター処理
- メッセージのデバッグ, 読み取りとフィルター処理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2c96f433ada8feb655e06b4f5a5089eded1bd4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209802"
---
# <a name="reading-and-filtering-debugging-messages"></a>デバッグ メッセージの読み取りとフィルター処理


## <span id="ddk_reading_and_filtering_debugging_messages_dbg"></span><span id="DDK_READING_AND_FILTERING_DEBUGGING_MESSAGES_DBG"></span>


カーネルモードのコードでは、 **Dbgprintex**ルーチンと**KdPrintEx**ルーチンを使用して、特定の条件下でのみ転送されるメッセージをカーネルデバッガーに送信できます。 これにより、関心のないメッセージを除外できます。

**注**   windows Server 2003 以前のバージョンの windows では、 **Dbgprint**と**KdPrint**は、無条件でカーネルデバッガーにメッセージを送信します。 Windows Vista 以降のバージョンの Windows では、これらのルーチンは、 **Dbgprintex**や**KdPrintEx**などの条件に応じてメッセージを送信します。 どのバージョンの Windows を使用している場合でも、 **Dbgprintex**と**KdPrintEx**を使用することをお勧めします。これにより、メッセージが送信される条件を制御できるためです。

 

これらのルーチンの完全なドキュメントについては、「Windows Driver Kit」を参照してください。

基本的な手順は次のとおりです。

**デバッグメッセージをフィルター処理するには**

1.  デバッガーに送信する各メッセージについて、ドライバーのコードで**Dbgprintex**関数または**KdPrintEx**関数を使用します。 適切なコンポーネント名を*ComponentId*パラメーターに渡し、このメッセージの重大度または性質を反映する*レベル*パラメーターに値を渡します。 メッセージ自体は、 **printf**と同様に、*形式*と*引数*のパラメーターに渡されます。

2.  適切な*コンポーネントフィルターマスク*の値を設定します。 各コンポーネントには異なるマスクがあります。マスクの値は、そのコンポーネントのメッセージのうち、どれが表示されるかを示します。 コンポーネントフィルターマスクは、レジストリエディターを使用するか、カーネルデバッガーを使用してメモリ内で設定できます。

3.  コンピューターにカーネルデバッガーをアタッチします。 ドライバーが**Dbgprintex**または**KdPrintEx**にメッセージを渡すたびに、 *ComponentId*と*Level*に渡される値は、対応するコンポーネントフィルターマスクの値と比較されます。 これらの値が特定の条件を満たしている場合、メッセージはカーネルデバッガーに送信されて表示されます。 それ以外の場合、メッセージは送信されません。

詳細については、こちらをご覧ください。 このページでは、 **Dbgprintex**へのすべての参照が**KdPrintEx**にも同様に適用されます。

### <a name="span-ididentifying-the-component-namespanspan-ididentifying_the_component_namespanidentifying-the-component-name"></a><span id="identifying-the-component-name"></span><span id="IDENTIFYING_THE_COMPONENT_NAME"></span>コンポーネント名の識別

各コンポーネントには、個別のフィルターマスクがあります。 これにより、デバッガーは各コンポーネントのフィルターを個別に構成できます。

各コンポーネントは、コンテキストに応じてさまざまな方法で参照されます。 **Dbgprintex**の*ComponentId*パラメーターでは、コンポーネント名の先頭に "DPFLTR\_" と "\_ID" が付加されます。 レジストリのコンポーネントフィルターマスクは、コンポーネント自体と同じ名前になります。 デバッガーでは、コンポーネントフィルターマスクの先頭に "Kd\_" と "\_Mask" というプレフィックスが付いています。

Microsoft Windows Driver Kit (WDK) ヘッダー ntddk と Windows SDK ヘッダー ntrtl. h のすべてのコンポーネント名 (DPFLTR\_*XXXX*\_ID 形式) の完全な一覧が表示されます。 これらのコンポーネント名の大部分は、Windows 用に予約されており、Microsoft によって作成されたドライバー用です。

独立系ハードウェアベンダー用に予約されているコンポーネント名は6つあります。 ドライバーの出力と Windows コンポーネントの出力が混在しないようにするには、次のコンポーネント名のいずれかを使用する必要があります。

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
<td align="left"><p>ビデオドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVAUDIO</strong></p></td>
<td align="left"><p>オーディオドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVNETWORK</strong></p></td>
<td align="left"><p>ネットワークドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVSTREAMING</strong></p></td>
<td align="left"><p>カーネルストリーミングドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IHVBUS</strong></p></td>
<td align="left"><p>バスドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IHVDRIVER</strong></p></td>
<td align="left"><p>その他の種類のドライバー</p></td>
</tr>
</tbody>
</table>

 

たとえば、ビデオドライバーを作成する場合は、DPFLTR\_IHVVIDEO\_ID を**Dbgprintex**の*ComponentId*パラメーターとして使用し、レジストリで値 name **IHVVIDEO**を使用して、デバッガーで**Kd\_IHVVIDEO\_Mask**を参照します。

Windows Vista 以降のバージョンの Windows では、 **Dbgprint**および**KdPrint**によって送信されたすべてのメッセージが、**既定**のコンポーネントに関連付けられています。

### <a name="span-idchoosing_the_correct_levelspanspan-idchoosing_the_correct_levelspanchoosing-the-correct-level"></a><span id="choosing_the_correct_level"></span><span id="CHOOSING_THE_CORRECT_LEVEL"></span>適切なレベルの選択

**Dbgprintex**ルーチンの*Level*パラメーターの型は DWORD です。 *重要度ビットフィールド*を決定するために使用されます。 *レベル*パラメーターとこのビットフィールドの間の接続は、*レベル*のサイズによって異なります。

-   *Level*が 0 ~ 31 の数値と等しい場合は、ビットシフトとして解釈されます。 重要度ビットフィールドは、値 1 &lt;&lt;*レベル*に設定されます。 したがって、 *Level*に対して0から31までの値を選択すると、ビットフィールドに1ビットだけが設定されます。 *Level*が0の場合、ビットフィールドは0x00000001 に相当します。 *level*が31の場合、ビットフィールドは0x80000000 に相当します。

-   *Level*が32から0xffffffff の範囲の数値の場合、重要度のビットフィールドは、*レベル*自体の値に設定されます。

したがって、ビットフィールドを0x00004000 に設定する場合は、0x00004000 として、または単に14として*レベル*を指定できます。 このシステムでは特定のビットフィールド値を使用できないことに注意してください。これは、完全にゼロのビットフィールドを含みます。

次の定数は、 *Level*の値を設定するのに役立ちます。 これらは、Microsoft Windows Driver Kit (WDK) ヘッダー ntddk および Windows SDK ヘッダーで定義されています。

```cpp
#define   DPFLTR_ERROR_LEVEL     0
#define   DPFLTR_WARNING_LEVEL   1
#define   DPFLTR_TRACE_LEVEL     2
#define   DPFLTR_INFO_LEVEL      3
#define   DPFLTR_MASK    0x8000000
```

*Level*パラメーターを使用する簡単な方法の1つは、0 ~ 31 の値を常に使用することです。ビット0、1、2、3を DPFLTR\_*XXXX*\_レベルで指定された意味で使用し、他のビットを使用して任意の内容を意味します。

*Level*パラメーターを使用するもう1つの簡単な方法は、明示的なビットフィールドを常に使用することです。 この方法を選択した場合は、または値 DPFLTR\_MASK をビットフィールドと共に使用することができます。これにより、誤って32未満の値を使用することがなくなります。

Windows でのメッセージレベルの使用方法とドライバーの互換性を確保するには、重大なエラーが発生した場合にのみ、重要度ビットフィールドの最低ビット (0x1) を設定する必要があります。 32未満の*レベル*値を使用している場合は、DPFLTR\_ERROR\_level に相当します。 このビットが設定されている場合は、ドライバーが実行されているコンピューターに他のユーザーがカーネルデバッガーをアタッチするたびに、メッセージが表示されます。

適切な状況では、警告、トレース、および情報の各レベルを使用する必要があります。 他のビットは、役に立つ任意の目的で自由に使用できます。 これにより、さまざまな種類のメッセージを選択して表示または非表示にすることができます。

Windows Vista 以降のバージョンの Windows では、 **Dbgprint**および**KdPrint**によって送信されたすべてのメッセージは、DPFLTR\_INFO\_レベルと同じ*レベル*の**dbgprintex**および**KdPrintEx**メッセージのように動作します。 つまり、これらのメッセージには、重要度が2番目のビットフィールドが設定されています。

### <a name="span-idsetting-the-component-filter-maskspanspan-idsetting_the_component_filter_maskspansetting-the-component-filter-mask"></a><span id="setting-the-component-filter-mask"></span><span id="SETTING_THE_COMPONENT_FILTER_MASK"></span>コンポーネントフィルターマスクの設定

コンポーネントフィルターマスクを設定するには、次の2つの方法があります。

- コンポーネントフィルターマスクは、レジストリキー **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\デバッグ印刷フィルター**にアクセスできます。 レジストリエディターを使用して、このキーを作成または開きます。 このキーの下に、目的のコンポーネントの名前を大文字で指定して値を作成します。 コンポーネントフィルターマスクとして使用する DWORD 値と同じ値を設定します。

- カーネルデバッガーがアクティブな場合は、 **Kd\_** <em>xxxx</em> **\_mask**という記号に格納されているアドレスを逆参照することによって、コンポーネントフィルターマスクの値にアクセスできます。ここで、 *xxxx*は目的のコンポーネント名です。 このマスクの値を WinDbg または KD で表示するには、 **dd (表示 dword)** コマンドを使用するか、 **ED (enter dword)** コマンドで新しいコンポーネントフィルターマスクを入力します。 シンボルがあいまいになる危険性がある場合は、このシンボルを nt! として指定することもできます **。Kd\_** <em>XXXX</em> **\_Mask**です。

レジストリに格納されているフィルターマスクは、ブート中に有効になります。 デバッガーによって作成されたフィルターマスクはすぐに有効になり、Windows が再起動されるまで保持されます。 レジストリに設定されている値はデバッガーによってオーバーライドできますが、システムを再起動すると、コンポーネントフィルターマスクはレジストリに指定された値に戻ります。

また、 **WIN2000**というシステム全体のマスクもあります。 既定では、これは0x1 と同じですが、レジストリまたはデバッガーを使用して他のすべてのコンポーネントと同様に変更できます。 フィルター処理を実行すると、各コンポーネントのフィルターマスクは、まず**WIN2000**マスクと共に使用されます。 特に、マスクが指定されていないコンポーネントは、既定で0x1 に設定されています。

### <a name="span-idcriteria-for-displaying_the_messagespanspan-idcriteria_for_displaying_the_messagespancriteria-for-displaying-the-message"></a><span id="criteria-for-displaying_the_message"></span><span id="CRITERIA_FOR_DISPLAYING_THE_MESSAGE"></span>メッセージを表示するための条件

**Dbgprintex**がカーネルモードコードで呼び出されると、Windows は、*レベル*で指定されたメッセージの重要度のビットフィールドと、 *ComponentId*で指定されたコンポーネントのフィルターマスクを比較します。

**注**  *レベル*パラメーターが 0 ~ 31 の場合、重要度ビットフィールドは 1 &lt;&lt;*レベル*と等しくなりますが、 *level*パラメーターが32以上の場合、重要度ビットフィールドは単に*level*と同じになります。

 

Windows は、重要度ビットフィールドとコンポーネントフィルターマスクに対して AND 演算を実行します。 結果が0以外の場合は、メッセージがデバッガーに送信されます。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

次に例を示します。

最後に起動する前に、**デバッグ印刷フィルター**キーに次の値を作成したとします。

-   **IHVVIDEO**(DWORD 0x2 と等しい値)

-   **IHVBUS**(DWORD 0x7ff と等しい)

ここで、カーネルデバッガーで次のコマンドを発行します。

```dbgcmd
kd> ed Kd_IHVVIDEO_Mask 0x8 
kd> ed Kd_IHVAUDIO_Mask 0x7 
```

この時点で、 **IHVVIDEO**コンポーネントのフィルターマスクは0x8 で、 **IHVAUDIO**コンポーネントのフィルターマスクは0x7 で、 **IHVBUS**コンポーネントのフィルターマスクは0x7ff です。

ただし、これらのマスクは、 **WIN2000**システム全体のマスク (通常は0x1 と同じ) に自動的に設定されるため、 **IHVVIDEO** mask は実質的に0x9 と同じになります。 実際には、フィルターマスクがまったく設定されていないコンポーネント (たとえば、 **IHVSTREAMING**または**DEFAULT**) は、フィルターマスクが0x1 になります。

ここで、次の関数呼び出しがさまざまなドライバーで発生するとします。

```cpp
DbgPrintEx( DPFLTR_IHVVIDEO_ID,  DPFLTR_INFO_LEVEL,   "First message.\n");
DbgPrintEx( DPFLTR_IHVAUDIO_ID,  7,                   "Second message.\n");
DbgPrintEx( DPFLTR_IHVBUS_ID,    DPFLTR_MASK | 0x10,  "Third message.\n");
DbgPrint( "Fourth message.\n");
```

最初のメッセージの*レベル*パラメーターは、DPFLTR\_INFO\_level に等しいレベルです (3)。 これは32未満であるため、ビットシフトとして扱われ、その結果、0x8 のビットフィールドが重要になります。 この値は、0x9 の有効な**IHVVIDEO**コンポーネントフィルターマスクを使用して連結され、0以外の結果が返されます。 そのため、最初のメッセージがデバッガーに送信されます。

2番目のメッセージの*レベル*パラメーターは7です。 ここでも、これはビットシフトとして扱われ、その結果、0x80 という重要度のビットフィールドになります。 次に、0x7 の**IHVAUDIO**コンポーネントフィルターマスクを使用して and 演算を行い、結果を0にします。 そのため、2番目のメッセージは転送されません。

3番目のメッセージには、DPFLTR\_MASK | と等しい*レベル*パラメーターがあります。0x10. これは31を超えるため、重要度ビットのフィールドは、0x80000010 に*レベル*の値 (つまり、) に等しい値に設定されます。 次に、0x7FF の**IHVBUS**コンポーネントフィルターマスクを使用して and 演算を行い、0以外の結果を提供します。 そのため、3番目のメッセージがデバッガーに送信されます。

4番目のメッセージは、 **Dbgprintex**ではなく、 **dbgprint**に渡されました。 Windows Server 2003 以前のバージョンの Windows では、このルーチンに渡されるメッセージは常に転送されます。 Windows Vista 以降のバージョンの Windows では、このルーチンに渡されるメッセージには常に既定のフィルターが付与されます。 重要度ビットフィールドは、1 &lt;&lt; DPFLTR\_INFO\_レベル (0x00000008) に相当します。 このルーチンのコンポーネントは、**既定値**です。 **既定**のコンポーネントのフィルターマスクを設定していないため、値は0x1 です。 この値が "重要度" のビットフィールドと連結されている場合、結果は0になります。 4番目のメッセージは転送されません。

### <a name="span-idthe-dbgprint-bufferspanspan-idthe_dbgprint_bufferspanthe-dbgprint-buffer"></a><span id="the-dbgprint-buffer"></span><span id="THE_DBGPRINT_BUFFER"></span>DbgPrint バッファー

**Dbgprint**、 **dbgprintex**、 **KdPrint**、または**KdPrintEx**がメッセージをデバッガーに送信すると、書式設定された文字列が*dbgprint バッファー*に送信されます。 ほとんどの場合、このバッファーの内容は、デバッガーコマンドウィンドウに直ちに表示されます。 この表示は、グローバルフラグユーティリティ (gflags) の**バッファー DbgPrint 出力**オプションを使用して無効にすることができます。 この表示は、ローカルカーネルデバッグ中に自動的には表示されません。

ローカルカーネルデバッグ中、およびこの表示が無効になっている場合、DbgPrint バッファーの内容を表示するには、 [**! dbgprint**](-dbgprint.md)拡張コマンドを使用する必要があります。

**Dbgprint**、 **dbgprintex**、 **KdPrint**、または**KdPrintEx**を1回呼び出すだけで、512バイトの情報が送信されます。 この値よりも長い出力は失われます。 DbgPrint バッファー自体は、Windows の無料ビルドで最大 4 KB のデータを保持できます。 Windows Server 2003 以降のバージョンの Windows では、KDbgCtrl ツールを使用して、DbgPrint バッファーのサイズを変更できます。 詳細については、「 [KDbgCtrl の使用](using-kdbgctrl.md)」を参照してください。

*ComponentId*と*Level*の値によってメッセージがフィルターで除外される場合、そのメッセージはデバッグ接続を介して送信されません。 このため、このメッセージをデバッガーで表示する方法はありません。
