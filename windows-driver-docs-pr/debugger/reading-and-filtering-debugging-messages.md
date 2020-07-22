---
title: デバッグ メッセージの読み取りとフィルター処理
description: デバッグ メッセージの読み取りとフィルター処理
ms.assetid: 785469d2-30b8-4f73-b397-80bf89ed20ea
keywords:
- デバッグメッセージの読み取りとフィルター処理
- メッセージのデバッグ, 読み取りとフィルター処理
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 87e943ef9d1e22cea86666817b88f88b55f1e4ed
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873837"
---
# <a name="reading-and-filtering-debugging-messages"></a>デバッグ メッセージの読み取りとフィルター処理

[**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)、 [**vdbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-vdbgprintex)、 [**vdbgprintexwithprefix**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-vdbgprintexwithprefix)、および[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)ルーチンは、指定された条件下でカーネルデバッガーにメッセージを送信します。 この手順では、優先度の低いメッセージを除外できます。

> [!NOTE]
> Microsoft Windows Server 2003 以前のバージョンの Windows では、 [**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)ルーチンと[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)ルーチンは、メッセージを無条件にカーネルデバッガーに送信します。
> Windows Vista 以降のバージョンの Windows では、これらのルーチンは、 **Dbgprintex**や**KdPrintEx**などの条件に応じてメッセージを送信します。
> どちらのバージョンの Windows を使用している場合でも、 **Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、および**KdPrintEx**を使用する必要があります。これらのルーチンを使用すると、メッセージが送信される条件を制御できます。

## <a name="to-filter-debugging-messages"></a>デバッグメッセージをフィルター処理するには

1. デバッガーに送信するメッセージごとに、ドライバーのコードで**Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、または**KdPrintEx**を使用します。 適切なコンポーネント名を*ComponentId*パラメーターに渡し、このメッセージの重大度または性質を反映する*レベル*パラメーターに値を渡します。 メッセージ自体は、 **printf**と同じ構文を使用して、 *Format*パラメーターと*arguments*パラメーターに渡されます。

2. 適切な*コンポーネントフィルターマスク*の値を設定します。 各コンポーネントには異なるマスクがあります。 マスクの値は、そのコンポーネントのメッセージのうち、どれが表示されるかを示します。 レジストリエディターを使用して、またはメモリ内でカーネルデバッガーを使用して、コンポーネントフィルターマスクを設定できます。

3. コンピューターにカーネルデバッガーをアタッチします。 ドライバーが**Dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、または**KdPrintEx**にメッセージを渡すたびに、 *ComponentId*と*Level*に渡される値は、対応するコンポーネントフィルターマスクの値と比較されます。 これらの値が特定の条件を満たしている場合、メッセージはカーネルデバッガーに送信されて表示されます。 それ以外の場合、メッセージは送信されません。

> [!NOTE]
> このページでは、 **Dbgprintex**へのすべての参照が、 **KdPrintEx**、 **vdbgprintex**、および**vdbgprintexwithprefix**にも同様に適用されます。

## <a name="identifying-the-component-name"></a>コンポーネント名の識別

各コンポーネントには、個別のフィルターマスクがあります。 これにより、デバッガーは各コンポーネントのフィルターを個別に構成できます。

各コンポーネントは、コンテキストに応じてさまざまな方法で参照されます。 **Dbgprintex**の*ComponentId*パラメーターでは、コンポーネント名の先頭に "DPFLTR" が付き、"ID" がサフィックスとして付けられ \_ \_ ます。 レジストリのコンポーネントフィルターマスクは、コンポーネント自体と同じ名前になります。 デバッガーでは、コンポーネントフィルターマスクの先頭に "Kd" と "mask" というプレフィックスが付いてい \_ \_ ます。

\_*XXXX* \_ Microsoft WINDOWS Driver Kit (WDK) header DPFLTR のすべてのコンポーネント名 (XXXX ID 形式) の完全な一覧が表示されます。 これらのコンポーネント名の大部分は、Windows 用に予約されており、Microsoft によって作成されたドライバー用です。

独立系ハードウェアベンダー用に予約されているコンポーネント名は6つあります。 ドライバーの出力と Windows コンポーネントの出力が混在しないようにするには、次のコンポーネント名のいずれかを使用する必要があります。

| コンポーネント名 | ドライバーの種類 |
| --- | --- |
| IHVVIDEO | ビデオドライバー |
| IHVAUDIO | オーディオドライバー |
| IHVNETWORK | ネットワークドライバー |
| IHVSTREAMING | カーネルストリーミングドライバー |
| IHVBUS | バスドライバー |
| IHVDRIVER | その他の種類のドライバー |

たとえば、ビデオドライバーを作成する場合は、DPFLTR \_ IHVVIDEO \_ ID を**Dbgprintex**の*ComponentId*パラメーターとして使用し、レジストリで値 name **IHVVIDEO**を使用して、デバッガーで**Kd \_ IHVVIDEO \_ Mask**を参照します。

**Dbgprint**および**KdPrint**によって送信されたすべてのメッセージは、**既定**のコンポーネントに関連付けられています。

### <a name="span-idchoosing_the_correct_levelspanspan-idchoosing_the_correct_levelspanchoosing-the-correct-level"></a><span id="choosing_the_correct_level"></span><span id="CHOOSING_THE_CORRECT_LEVEL"></span>適切なレベルの選択

**Dbgprintex**ルーチンの*Level*パラメーターの型は DWORD です。 *重要度ビットフィールド*を決定するために使用されます。 *レベル*パラメーターとこのビットフィールドの間の接続は、*レベル*のサイズによって異なります。

- *Level*が 0 ~ 31 の数値と等しい場合は、ビットシフトとして解釈されます。 重要度ビットフィールドは、値1レベルに設定され &lt; &lt; *Level*ます。 したがって、 *Level*に対して0から31までの値を選択すると、ビットフィールドに1ビットだけが設定されます。 *Level*が0の場合、ビットフィールドは0x00000001 に相当します。 *level*が31の場合、ビットフィールドは0x80000000 に相当します。

- *Level*が32から0xffffffff の範囲の数値の場合、重要度のビットフィールドは、*レベル*自体の値に設定されます。

したがって、ビットフィールドを0x00004000 に設定する場合は、0x00004000 として、または単に14として*レベル*を指定できます。 このシステムでは特定のビットフィールド値を使用できないことに注意してください。これは、完全にゼロのビットフィールドを含みます。

次の定数は、 *Level*の値を設定するのに役立ちます。 これらは、Microsoft Windows Driver Kit (WDK) ヘッダーで定義されており、Windows SDK ヘッダーです。

```cpp
#define   DPFLTR_ERROR_LEVEL     0
#define   DPFLTR_WARNING_LEVEL   1
#define   DPFLTR_TRACE_LEVEL     2
#define   DPFLTR_INFO_LEVEL      3
#define   DPFLTR_MASK    0x8000000
```

*Level*パラメーターを使用する簡単な方法の1つとして、0 ~ 31 の値を常に使用することができます。ビット0、1、2、3を DPFLTR XXXX レベルで指定された意味で使用し、他のビットを使用して \_ *XXXX* \_ 任意のものを意味します。

*Level*パラメーターを使用するもう1つの簡単な方法は、明示的なビットフィールドを常に使用することです。 この方法を選択した場合は、または DPFLTR MASK 値をビットフィールドに入力することができます。 \_ これにより、誤って32未満の値を使用することがなくなります。

Windows でのメッセージレベルの使用方法とドライバーの互換性を確保するには、重大なエラーが発生した場合にのみ、重要度ビットフィールドの最低ビット (0x1) を設定する必要があります。 32未満の*レベル*値を使用している場合は、DPFLTR \_ エラーレベルに対応し \_ ます。 このビットが設定されている場合は、ドライバーが実行されているコンピューターに他のユーザーがカーネルデバッガーをアタッチするたびに、メッセージが表示されます。

適切な状況では、警告、トレース、および情報の各レベルを使用する必要があります。 他のビットは、役に立つ任意の目的で自由に使用できます。 これにより、さまざまな種類のメッセージを選択して表示または非表示にすることができます。

**Dbgprint**と**KdPrint**によって送信されるすべてのメッセージは、DPFLTR INFO レベルと同じ*レベル*の**dbgprintex**および**KdPrintEx**メッセージのように動作し \_ \_ ます。 つまり、これらのメッセージには、重要度が2番目のビットフィールドが設定されています。

## <a name="setting-the-component-filter-mask"></a>コンポーネントフィルターマスクの設定

コンポーネントフィルターマスクを設定するには、次の2つの方法があります。

- コンポーネントフィルターマスクにアクセスするには、レジストリキー **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ Session Manager \\ デバッグ印刷フィルター**を使用します。 レジストリエディターを使用して、このキーを作成または開きます。 このキーの下に、目的のコンポーネントの名前を大文字で指定して値を作成します。 コンポーネントフィルターマスクとして使用する DWORD 値と同じ値を設定します。

- カーネルデバッガーがアクティブになっている場合は、シンボル**Kd \_ **<em>XXXX</em>** \_ mask**に格納されているアドレスを逆参照することによって、コンポーネントフィルターマスクの値にアクセスできます。ここで、 *XXXX*は目的のコンポーネント名です。 このマスクの値を WinDbg または KD で表示するには、 **dd (表示 dword)** コマンドを使用するか、 **ED (enter dword)** コマンドで新しいコンポーネントフィルターマスクを入力します。 シンボルがあいまいになる危険性がある場合は、このシンボルを nt! として指定することもできます **。Kd \_ **<em>XXXX</em>** \_ マスク**。

レジストリに格納されているフィルターマスクは、ブート中に有効になります。 デバッガーによって作成されたフィルターマスクはすぐに有効になり、Windows が再起動されるまで保持されます。 レジストリに設定されている値はデバッガーによってオーバーライドできますが、システムを再起動すると、コンポーネントフィルターマスクはレジストリに指定された値に戻ります。

また、 **WIN2000**というシステム全体のマスクもあります。 既定では、これは0x1 と同じですが、レジストリまたはデバッガーを使用して他のすべてのコンポーネントと同様に変更できます。 フィルター処理を実行すると、各コンポーネントのフィルターマスクは、まず**WIN2000**マスクと共に使用されます。 特に、マスクが指定されていないコンポーネントは、既定で0x1 に設定されています。

## <a name="criteria-for-displaying-the-message"></a>メッセージを表示するための条件

**Dbgprintex**がカーネルモードコードで呼び出されると、Windows は、*レベル*で指定されたメッセージの重要度のビットフィールドと、 *ComponentId*で指定されたコンポーネントのフィルターマスクを比較します。

> [!NOTE]
> *Level*パラメーターが 0 ~ 31 の場合、重要度ビットフィールドは 1 << *レベル*と同じであることを思い出してください。 しかし、 *level*パラメーターが32以上の場合、重要度ビットフィールドは単に*level*と等しくなります。

Windows は、重要度ビットフィールドとコンポーネントフィルターマスクに対して AND 演算を実行します。 結果が0以外の場合は、メッセージがデバッガーに送信されます。

## <a name="debug-filter-example"></a>デバッグフィルターの例

最後に起動する前に、**デバッグ印刷フィルター**キーに次の値を作成したとします。

- **IHVVIDEO**(DWORD 0x2 と等しい値)

- **IHVBUS**(DWORD 0x7ff と等しい)

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

最初のメッセージの*レベル*パラメーターは \_ 、DPFLTR INFO \_ level (3) と同じです。 これは32未満であるため、ビットシフトとして扱われ、その結果、0x8 のビットフィールドが重要になります。 この値は、0x9 の有効な**IHVVIDEO**コンポーネントフィルターマスクを使用して連結され、0以外の結果が返されます。 そのため、最初のメッセージがデバッガーに送信されます。

2番目のメッセージの*レベル*パラメーターは7です。 ここでも、これはビットシフトとして扱われ、その結果、0x80 という重要度のビットフィールドになります。 次に、0x7 の**IHVAUDIO**コンポーネントフィルターマスクを使用して and 演算を行い、結果を0にします。 そのため、2番目のメッセージは転送されません。

3番目のメッセージには、DPFLTR MASK | 0x10 と等しい*レベル*パラメーターがあり \_ ます。 これは31を超えるため、重要度ビットのフィールドは、0x80000010 に*レベル*の値 (つまり、) に等しい値に設定されます。 次に、0x7FF の**IHVBUS**コンポーネントフィルターマスクを使用して and 演算を行い、0以外の結果を提供します。 そのため、3番目のメッセージがデバッガーに送信されます。

4番目のメッセージは、 **Dbgprintex**ではなく、 **dbgprint**に渡されました。 Windows Server 2003 以前のバージョンの Windows では、このルーチンに渡されるメッセージは常に転送されます。 Windows Vista 以降のバージョンの Windows では、このルーチンに渡されるメッセージには常に既定のフィルターが付与されます。 重要度ビットフィールドは、1 &lt; &lt; DPFLTR \_ INFO \_ レベル (0x00000008) に相当します。 このルーチンのコンポーネントは、**既定値**です。 **既定**のコンポーネントのフィルターマスクを設定していないため、値は0x1 です。 この値が "重要度" のビットフィールドと連結されている場合、結果は0になります。 4番目のメッセージは転送されません。

## <a name="dbgprint-buffer-and-the-debugger"></a>DbgPrint バッファーとデバッガー

**Dbgprint**、 **dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、 **KdPrint**、または**KdPrintEx**ルーチンがメッセージをデバッガーに送信すると、書式設定された文字列が**dbgprint**バッファーに送信されます。 このバッファーの内容は、GFlags の**バッファー DbgPrint 出力**オプションを使用してこの表示を無効にしていない限り、デバッガーコマンドウィンドウに直ちに表示されます。

ローカルカーネルデバッグ中、およびこの表示が無効になっている場合、DbgPrint バッファーの内容を表示するには、 [**! dbgprint**](-dbgprint.md)拡張コマンドを使用する必要があります。

**Dbgprint**、 **dbgprintex**、 **vdbgprintex**、 **vdbgprintexwithprefix**、 **KdPrint**、または**KdPrintEx**を1回呼び出すと、512バイトの情報のみが転送されます。 512バイトより長い出力は失われます。 DbgPrint バッファー自体は、Windows の無料ビルドで最大 4 KB のデータを保持でき、Windows のチェックされたビルドで最大 32 KB のデータを保持できます。 Windows Server 2003 以降のバージョンの Windows では、KDbgCtrl ツールを使用して、DbgPrint バッファーのサイズを変更できます。 このツールは、Windows 用デバッグツールの一部です。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

*ComponentId*と*Level*の値によってメッセージがフィルターで除外される場合、そのメッセージはデバッグ接続を介して送信されません。 このため、このメッセージをデバッガーで表示する方法はありません。
