---
title: Windows ドライバーへの WPP ソフトウェア トレースの追加
description: カーネルモードドライバーやユーザーモードアプリケーションなど、トレースプロバイダーで WPP ソフトウェアトレースを使用するには、ドライバーのソースファイルを追加し、ドライバープロジェクトを変更する必要があります。 ここでは、これらの手順について説明します。
ms.assetid: 487BA8AA-950A-4F3C-9E3E-EBE1DA35D4B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2e8fadc5ae9983cd2bd40b8a1215a6812e8355
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840304"
---
# <a name="adding-wpp-software-tracing-to-a-windows-driver"></a>Windows ドライバーへの WPP ソフトウェア トレースの追加

カーネルモードドライバーやユーザーモードアプリケーションなど、トレースプロバイダーで WPP ソフトウェアトレースを使用する*には、* ドライバーのソースファイルを追加し、ドライバープロジェクトを変更する必要があります。 ここでは、これらの手順について説明します。

**ヒント** ドライバーに WPP トレースを追加する最も簡単な方法は、Visual Studio で KMDF または UMDF ドライバーテンプレートのいずれかを使用することです。 テンプレートを使用する場合、追加する必要があるコードの多くは既に実行されています。 Visual Studio で、[**ファイル &gt; 新しい &gt; プロジェクト**] をクリックし、[Windows ドライバー (ユーザーモードまたはカーネルモード)] WDF プロジェクトを選択します。 WPP マクロは、プロジェクトの一部として含まれている Trace .h ヘッダーファイルで定義されています。 いずれかのテンプレートを使用する場合は、[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points). に進むことができます。 

-   [手順 1: コントロールの GUID とトレースフラグを定義する](#step-1-define-the-control-guid-and-trace-flags)
-   [手順 2: 使用するトレースメッセージ関数を選択し、それらの関数の WPP マクロを定義する](#step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions)
-   [手順 3: 関連するトレースヘッダーファイル (.h および tmh) を C またはC++ソースファイルに含める](#step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files)
-   [手順 4: 適切なコールバック関数にマクロを追加して、WPP を初期化してクリーンアップする](#step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp)
-   [手順 5: 適切なポイントでトレースメッセージを生成するためのドライバーコードのインストルメント化](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)
-   [手順 6: WPP プリプロセッサを実行し、ソリューションをビルドするように Visual Studio プロジェクトを変更する](#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)
-   [手順 7: トレースセッションを開始してトレースメッセージをキャプチャし、検証する](#step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages)

## <a name="step-1-define-the-control-guid-and-trace-flags"></a>手順 1: コントロールの GUID とトレースフラグを定義する

すべてのトレースプロバイダー (ドライバー、ユーザーモードアプリなど) は一意に定義する必要があります。 これを行うには、コントロールの GUID、識別子、およびトレースフラグを定義する、 [WPP\_control\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロを追加します。 これにより、いつ、どのようなトレースを行うかを特定して制御できるようになります。 通常、各ドライバーには個別のコントロール GUID がありますが、ドライバーは複数のコントロール guid を持つことができます。または、複数のドライバーが1つのコントロール GUID を共有できます。

便宜上、 [WPP\_制御\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロは、一般的なヘッダーファイルで定義されています。 トレース用にインストルメント化するソースファイルには、ヘッダーファイル (\#インクルード) を含める必要があります。

**WPP\_CONTROL\_GUID マクロをドライバーに追加するには、次のようにします。**

1.  WPP トレースマクロC++の定義に使用できる新しいヘッダーファイルを Visual Studio プロジェクトに追加します。 たとえば、ソリューションエクスプローラーでドライバーを右クリックし、[ **&gt; 新しい項目の追加**] をクリックします。 (たとえば、トレース .h として) ファイルを保存します。

2.  [WPP\_制御\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロを追加して、トレースプロバイダーのフレンドリ名を指定し、コントロールの GUID を定義し、特定のトレースメッセージを修飾するために使用できるトレースフラグを定義します。

    [WPP\_CONTROL\_guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロには、次の構文があります。

    **WPP\_制御\_GUID の構文**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS \
        WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
            WPP_DEFINE_BIT(NameOfTraceFlag1)  \
            WPP_DEFINE_BIT(NameOfTraceFlag2)  \
            .............................   \
            .............................   \
            WPP_DEFINE_BIT(NameOfTraceFlag31) 
    ```

    たとえば、次のコードでは、Guid *friendlyname*として myDriverTraceGuid を使用しています。 *Controlguid*は、32桁の16進数の guid の標準形式とは少し異なる形式であることに注意してください。 *Controlguid*には5つのフィールドがありますが、通常のハイフンや中かっこではなく、コンマで区切り、かっこで囲まれています。 たとえば、{84bdb2e9-829e-41b3-b891-02f454bc2bd7} ではなく (**84 bdb2e9、829e、41b3、b891、02f454bc2bd7)** を指定します。

    **WPP\_制御\_GUID ステートメントの例**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS                                              \
        WPP_DEFINE_CONTROL_GUID(                                           \
            myDriverTraceGuid, (84bdb2e9,829e,41b3,b891,02f454bc2bd7), \
            WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)        /* bit  0 = 0x00000001 */ \
            WPP_DEFINE_BIT(TRACE_DRIVER)             /* bit  1 = 0x00000002 */ \
            WPP_DEFINE_BIT(TRACE_DEVICE)             /* bit  2 = 0x00000004 */ \
            WPP_DEFINE_BIT(TRACE_QUEUE)              /* bit  3 = 0x00000008 */ \
            )                             
    ```

    **ヒント** このコードスニペットをヘッダーファイルにコピーできます。 コントロールの GUID とフレンドリ名を必ず変更してください。 Guidgen.exe を使用して、コントロールの GUID を生成できます。 Guidgen.exe は、Visual Studio に含まれています (**ツール &gt; 作成 GUID**)。 また、Visual Studio のコマンドプロンプトウィンドウから使用できる Uuidgen.exe ツールを使用することもできます (「 **uuigen/?」と**入力します。 を参照してください)。



3.  トレースプロバイダーの[トレースフラグ](trace-flags.md)を定義します。

    WPP\_は、WPP\_コントロール\_GUID マクロの\_ビット要素を定義して、トレースプロバイダーのトレースフラグを定義します。 通常、フラグは、より詳細なレポートレベルを表しますが、トレースメッセージを生成する条件として、フラグを使用することもできます。 WPP\_制御\_GUID の例では、WPP\_で\_ビットを定義すると、4つのトレースフラグ (MYDRIVER\_すべての\_情報、トレース\_ドライバー、トレース\_デバイス、トレース\_キュー) が定義されます。

    最大31個のトレースフラグを定義できます。 WPP では、ビット値が表示される順序で要素に割り当てられます。たとえば、ビット 0 (0x1)、ビット 1 (0x2)、ビット 2 (0x4)、ビット 3 (0x8) などです。 トレースフラグは、トレースメッセージ関数をソースコードに追加するときに使用します (詳細については、「[手順 5: ドライバーコードをインストルメント化してトレースメッセージを適切な場所に生成する](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)」を参照してください)。

    **メモ** トレースフラグを使用すると、特定のコンポーネント (特定の i/o 要求、デバイスまたはドライバーオブジェクトのアクティビティなど) をトレースするタイミングを制御できます。 トレースフラグは、トレースメッセージステートメント (`DoTraceMessage (TRACE_DRIVER, "Hello World!\n")`など) に追加します。 トレースコントローラー ( [Tracelog](tracelog.md)など) を使用してトレースセッションを作成する場合は、そのセッションでトレースプロバイダーに使用する **-flag**オプションを指定します。この場合、フラグはビット 1 (0x1) です。これは、trace\_DRIVER フラグに対応します。 トレースセッションを開始すると、そのトレースフラグを指定するすべてのトレースメッセージがログに書き込まれます。



## <a name="step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions"></a>手順 2: 使用するトレースメッセージ関数を選択し、それらの関数の WPP マクロを定義する


デバッグ印刷関数と同様に、トレースメッセージ関数は、トレースメッセージを記述するためにコードに追加する関数 (またはマクロ) です。

**トレースメッセージ関数の選択**

1.  既定のトレースメッセージ関数は、 [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロです。 既定の関数を使用する場合は、プロバイダーの[トレースフラグ](trace-level.md)値を使用してメッセージを生成するタイミングを制御できます。 トレースフラグの値は、手順 1. でコントロール GUID を作成したときに定義したフラグです。 **DoTraceMessage**を使用すると、既定の wpp マクロが既に定義されています (WPP\_LEVEL\_ENABLED および WPP\_LEVEL\_LOGGER)。そのため、この手順の残りの部分をスキップして、[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points). に進むことができます。

2.  KMDF テンプレートまたは UMDF テンプレートのいずれかを使用している場合は、 **Traceevents**関数と必要な WPP マクロが既に定義されているので、その関数を有効にするため、[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points). に進むことができます。

3.  独自のトレースメッセージ関数を作成する場合、または既存のデバッグ印刷関数を変換する場合は、この手順の残りの部分を続行します。

**トレースメッセージ関数の作成またはカスタマイズ**

1.  カスタムトレースメッセージ関数を使用する場合、またはデバッグ印刷関数 ( [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)など) を変換してトレースメッセージを生成する場合は、トレースプロバイダーでトレースメッセージ関数を識別および有効にする WPP マクロを定義する必要があります。 プロジェクトに追加した Trace .h ヘッダーファイルにこれらのマクロを配置します。

2.  WPP マクロを定義して、trace 関数を有効にします。

    使用する各トレースメッセージ関数には、対応するマクロペアが必要です。 これらのマクロは、トレースプロバイダーを識別し、メッセージを生成する条件を指定します。 通常、既定の WPP\_レベル&lt;ENABLED および WPP&gt;LEVEL\_LOGGER マクロの観点では、\_LOGGER および Wpp の **\_ *&lt;条件&gt;* logger**および wpp **\_\_*条件*\_有効**にするマクロのペアを定義します。\_

使用する各トレースメッセージ関数には、対応するマクロペアが必要です。 これらのマクロは、トレースプロバイダーを識別し、メッセージを生成する条件を指定します。 通常、既定の WPP\_レベル&lt;ENABLED および WPP&gt;LEVEL\_LOGGER マクロの観点では、\_LOGGER および Wpp の **\_ *&lt;条件&gt;* logger**および wpp **\_\_*条件*\_有効**にするマクロのペアを定義します。\_

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="WPP_CONDITIONS_LOGGER"></span><span id="wpp_conditions_logger"></span>LOGGER<em><strong>WPP_<em>条件</em></strong></p></td>
<td align="left"><p>プロバイダーに関連付けられているトレースセッションを検索し、セッションへのハンドルを返すために使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="WPP_CONDITIONS_ENABLED"></span><span id="wpp_conditions_enabled"></span><strong>WPP</em><em>条件</em>_ENABLED</strong></p></td>
<td align="left"><p>指定された条件でログ記録が有効かどうかを判断するために使用されます。</p></td>
</tr>
</tbody>
</table>



定義する WPP マクロでは、*条件*は、関数のパラメーターリストに表示される順序で、トレースメッセージ関数がサポートする条件をアンダースコアで区切って表します。 たとえば、既定のトレースメッセージ関数[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))では、[トレースフラグ](trace-level.md)のみが条件としてサポートされているので、マクロ名にはパラメーターが1つだけ存在します (WPP\_レベル\_有効)。

**メモ** 残念ながら、既定のマクロ (WPP\_レベル\_ENABLED および WPP\_レベル\_LOGGER) の名前は、[トレースレベル](trace-level.md)パラメーターを示していますが、実際にはトレースフラグを参照しています。



カスタムトレースメッセージ関数を使用する場合は、[トレースレベル](trace-level.md)などの追加の修飾子を設定できます。 トレースレベルは Evntrace ファイルで定義されており、トレースレベルは、エラー、警告、および情報メッセージとしてトレースメッセージを分類するための便利な方法を提供します。

たとえば、プロジェクトに追加したヘッダーファイルに次のコードスニペットを追加できます。 トレースメッセージを生成する条件としてトレース[レベル](trace-level.md)とトレースフラグパラメーターの両方をサポートするトレースメッセージ関数のカスタム WPP マクロを定義するコードを次に示します。 指定されたフラグの値に対してログ記録が有効になっていて、enabled レベルの値がトレースメッセージの関数呼び出しで使用されているレベルの引数以上の場合、 **WPP\_LEVEL\_flags\_ENABLED**マクロは TRUE を返します。

```ManagedCPlusPlus
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

次に、WPP 構成ブロック (**begin\_wpp config**と**end\_wpp**) でカスタムトレース関数を指定する必要があります。たとえば、Visual Studio で UMDF または kmdf ドライバープロジェクトのテンプレートを使用する場合、テンプレートは**traceevents**というカスタムトレースメッセージ関数の WPP マクロを定義します。 **Traceevents**マクロ関数は、メッセージを生成するための条件として[トレースレベル](trace-level.md)とトレースフラグを使用します。 **\_レベルの\_FLAGS\_ENABLED**マクロをトレース .h ヘッダーファイルに定義している場合は、次のマクロ定義を追加できます。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define the 
// TraceEvents function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// end_wpp
//
```

また、WPP 構成ブロックに同様の**FUNC**宣言を追加することによって、既存のデバッグ印刷ステートメントをトレースメッセージステートメントに変換することもできます。 たとえば、次の例では、既存の[**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)ステートメントを変換するコードを追加します。 また、 **FUNC**宣言は、指定されたトレースレベルとフラグ {LEVEL = TRACE\_LEVEL\_INFORMATION, FLAGS = TRACE\_DRIVER} を使用するように、グローバルに**定義します**。 デバッガーに出力を送信する代わりに、デバッグ印刷ステートメントがトレースログに送信されます。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define the
// TraceEvents function and conversion for KdPrint. Note the double parentheses for the KdPrint message, for compatiblility with the KdPrint function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC KdPrint{LEVEL=TRACE_LEVEL_INFORMATION, FLAGS=TRACE_DRIVER}((MSG, ...));
// end_wpp
//
```

**メモ** [**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)をトレースメッセージ関数に変換する場合は、いくつかの追加の手順を実行する必要があります。 [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)と比較した場合、 **KdPrintEx**関数は2つの追加の引数を受け取ります。 **KdPrintEx**関数を変換するには、 *ComponentID*に対して **\_ビットを定義**し、カスタムの**wpp\_ *&lt;条件*** &gt;\_LOGGER および WPP\_&lt;&gt;**有効になっている**マクロを定義\_必要があります。\_ **KdPrintEx**の2番目のパラメーターは、のレベルが[トレースレベル](trace-level.md)の値に似ていることを指定します。そのため、必ずしもそれらを再定義する必要はありません。



```ManagedCPlusPlus

#define WPP_CONTROL_GUIDS                                              \
    WPP_DEFINE_CONTROL_GUID(\
    myDriverTraceGuid, (11C3AAE4, 0D88, 41b3, 43BD, AC38BF747E19), \    /* change GUID for your provider */
        WPP_DEFINE_BIT(MYDRIVER_ALL_INFO)        /* bit  0 = 0x00000001 */ \
        WPP_DEFINE_BIT(TRACE_DRIVER)             /* bit  1 = 0x00000002 */ \
        WPP_DEFINE_BIT(TRACE_DEVICE)             /* bit  2 = 0x00000004 */ \
        WPP_DEFINE_BIT(TRACE_QUEUE)              /* bit  3 = 0x00000008 */ \
        WPP_DEFINE_BIT(DPFLTR_IHVDRIVER_ID)      /* bit  4 = 0x00000010 */\         /* Added for the ComponentID param of KdPrintEx */
    )

#define WPP_Flags_LEVEL_LOGGER(Flags, level)                                  \
    WPP_LEVEL_LOGGER(Flags)

#define WPP_Flags_LEVEL_ENABLED(Flags, level)                                 \
    (WPP_LEVEL_ENABLED(Flags) && \
    WPP_CONTROL(WPP_BIT_ ## Flags).Level >= level)



//
// This comment block is scanned by the trace preprocessor to convert the KdPrintEx function.
// Note the double parentheses for the KdPrint message, for compatiblility with the KdPrintEx function.
//
// begin_wpp config
// FUNC KdPrintEx((Flags, LEVEL, MSG, ...));   
// end_wpp
//
```

## <a name="step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files"></a>手順 3: 関連するトレースヘッダーファイル (.h および tmh) を C またはC++ソースファイルに含める


ドライバーのコントロール GUID とトレースフラグをヘッダーファイル (たとえば、trace) で定義した場合は、WPP を初期化およびアンロードするソースファイルにヘッダーファイルを含める必要があります (手順 4.)。または、トレースメッセージ関数を呼び出します。

さらに、[トレースメッセージヘッダーファイル](trace-message-header-file.md)(tmh) の **\#include**ステートメントを追加する必要があります。 ドライバーまたはアプリケーションをビルドすると、WPP プリプロセッサによって、トレースメッセージ関数を含む各ソースファイルのトレースメッセージヘッダーファイル (tmh) が生成されます。

```ManagedCPlusPlus
/* -- driver.c  - include the *.tmh file that is generated by WPP --*/

#include "trace.h"     /* file that defines WPP_CONFIG_GUIDS and trace flags */
#include "driver.tmh"  /* this file is auto-generated */
```

## <a name="step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp"></a>手順 4: 適切なコールバック関数にマクロを追加して、WPP を初期化してクリーンアップする


**ドライバーエントリで WPP を初期化するには**

-   [WPP\_INIT\_TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを、カーネルモードドライバーまたは umdf 2.0 ドライバーの*driverentry*ルーチン、またはユーザーモードドライバー (umdf 1.x) またはアプリケーションの*DLLMain*ルーチンに追加します。

**ドライバーの終了時に WPP リソースをクリーンアップするには**

-   カーネルモードドライバーまたは UMDF 2.0 ドライバーのドライバーのアンロードルーチン ( *Drivercontextcleanup* 、 *driverunload*など) に、 [WPP\_CLEANUP](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロを追加します。

    ユーザーモードドライバー (UMDF 1.x) またはアプリケーションの場合*は、* WPP ルーチンに[WPP\_CLEANUP](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロを追加します。

    また、 *Driverentry*が失敗した場合に備えて、 *Driverentry*ルーチンに[WPP\_CLEANUP](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロを追加する必要があります。 たとえば、 *Driverentry*が失敗した場合、ドライバーのアンロードルーチンは呼び出されません。 次の例の[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)の呼び出しを参照してください。

WPP を使用したカーネルモードドライバーの例\_INIT\_TRACING と WPP\_*Driverentry*でのクリーンアップ

```ManagedCPlusPlus

NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT  DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{  

          //  ... 

                //
    // Initialize WPP Tracing in DriverEntry
    //
    WPP_INIT_TRACING( DriverObject, RegistryPath );

                //  ...


 //
    // Create a framework driver object to represent our driver.
    //
    status = WdfDriverCreate(
        DriverObject,
        RegistryPath,
        &attributes, // Driver Object Attributes
        &config,          // Driver Config Info
        WDF_NO_HANDLE // hDriver
        );

    if (!NT_SUCCESS(status)) {

        TraceEvents(TRACE_LEVEL_ERROR, DBG_INIT,
                "WdfDriverCreate failed with status 0x%x\n", status);
        //
        // Cleanup tracing here because DriverContextCleanup will not be called
        // as we have failed to create WDFDRIVER object itself.
        // Please note that if you return failure from DriverEntry after the
        // WDFDRIVER object is created successfully, you don't have to
        // call WPP cleanup because in those cases DriverContextCleanup
        // will be executed when the framework deletes the DriverObject.
        //
        WPP_CLEANUP(DriverObject);

    }

                return status;

}
```

DriverContextCleanup での WPP\_クリーンアップを使用したカーネルモードドライバーの例

```ManagedCPlusPlus


VOID
DriverContextCleanup(
       PDRIVER_OBJECT DriverObject
       )
{
    // ...

    // Clean up WPP resources on unload
    //
    WPP_CLEANUP(DriverObject);

   // ...

}
```

WPP を使用した UMDF 2.0 ドライバーの例\_INIT\_DriverEntry のトレース

```ManagedCPlusPlus

/
// Driver specific #defines in trace header file (trace.h)
//
#define MYDRIVER_TRACING_ID      L"Microsoft\\UMDF2.0\\UMDF2_0Driver1 V1.0"
```

```ManagedCPlusPlus

 // Initialize WPP Tracing in the DriverEntry routine
 //
    WPP_INIT_TRACING( MYDRIVER_TRACING_ID );
```

UMDF 1.0 ドライバーでの WPP の使用例\_INIT\_トレースおよび WPP\_クリーンアップマクロ (DLLMain)

```ManagedCPlusPlus
/
// Driver specific #defines in trace header file (for example, trace.h)
//
#define MYDRIVER_TRACING_ID      L"Microsoft\\UMDF1.X\\UMDF1_XDriver1"


//
// DLL Entry Point - UMDF 1.0 example in the source file where you implement the DLL exports.
// 

extern "C"
BOOL
WINAPI
DllMain(
    HINSTANCE hInstance,
    DWORD dwReason,
    LPVOID lpReserved
    )
{
    if (dwReason == DLL_PROCESS_ATTACH) {
        WPP_INIT_TRACING(MYDRIVER_TRACING_ID);              // Initialize WPP tracing

        g_hInstance = hInstance;
        DisableThreadLibraryCalls(hInstance);

    } else if (dwReason == DLL_PROCESS_DETACH) {
        WPP_CLEANUP();                                                                                                              // Deactivate and cleanup WPP tracing
    }

    return _AtlModule.DllMain(dwReason, lpReserved);
}
```

## <a name="step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points"></a>手順 5: 適切なポイントでトレースメッセージを生成するためのドライバーコードのインストルメント化


トレースメッセージ関数、トレースフラグ、およびレベルが適切に定義されていれば、選択したトレースメッセージ関数を使用できます。 既定のトレースメッセージ関数は、 [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロです。 このマクロをコードに追加して、ログファイルにメッセージを書き込むことができます。 次の表に、トレースメッセージの作成に使用できる定義済みのトレースメッセージ関数とデバッグ印刷関数の一覧を示します。

<table>
<colgroup>
<col width="50%" />

<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トレースメッセージ関数の例</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a></td>
<td align="left"><p>これは、既定のトレースメッセージ関数です。 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a>を使用する利点は、関数が既に定義されていることです。 WPP_CONFIG_GUIDS マクロで指定するトレースフラグを使用できます。 <strong>DoTraceMessage</strong>を使用する場合の欠点は、関数が1つの条件付きパラメーター (つまり、トレースフラグ) のみを受け取ることです。 トレースレベルを使用する場合、エラーメッセージまたは警告メッセージだけを記録するには、 <strong>Dodebugtrace</strong>マクロを使用するか、トレースフラグとトレースレベルの両方を使用する<strong>traceevents</strong>を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceEvents</strong></td>
<td align="left"><p>Visual Studio で WDF テンプレートを使用してドライバーを作成する場合は、これが既定のトレースメッセージ関数になります。 <strong>Traceevents</strong>を使用する利点は、トレースメッセージ関数、トレースフラグ、および<a href="trace-level.md" data-raw-source="[Trace Level](trace-level.md)">トレースレベル</a>が既に定義されていることです。 また、テンプレートには、関数の開始時と終了時にログファイルにメッセージを書き込むインストルメンテーションも含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint" data-raw-source="[&lt;strong&gt;KdPrint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)"><strong>KdPrint</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex" data-raw-source="[&lt;strong&gt;KdPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)"><strong>KdPrintEx</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint" data-raw-source="[&lt;strong&gt;DbgPrint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)"><strong>dbgprint</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex" data-raw-source="[&lt;strong&gt;DbgPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)"><strong>dbgprintex</strong></a></td>
<td align="left"><p>デバッグ印刷関数を使用する利点は、既存のデバッグ印刷ステートメントを変更する必要がないことです。 デバッガーでのメッセージの表示から簡単に切り替えて、トレースメッセージをファイルに記録することができます。 トレースメッセージ関数をカスタマイズして、いずれかのデバッグ印刷関数を含める場合は、それ以上の作業を行う必要はありません。 Logman または<a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a>または別のトレースコントローラーでトレースセッションを作成する場合は、プロバイダーのフラグとレベルを指定するだけです。 指定した条件を満たすすべてのデバッグ印刷ステートメントがログに出力されます。</p></td>
</tr>
</tbody>
</table>



<span id="using_dotracemessage"></span><span id="USING_DOTRACEMESSAGE"></span>

**DoTraceMessage ステートメントの使用**

1.  追加、 [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) マクロ コード デバッグ印刷ルーチンの場合と同様にします。 **DoTraceMessage**マクロは、3つのパラメーターを受け取ります。フラグレベル (*traceflagname*) は、トレースメッセージが書き込まれるときの条件、*メッセージ*文字列、および省略可能な変数リストを定義します。

    ```
    DoTraceMessage(TraceFlagName, Message, [VariableList... ]
    ```

    たとえば、次 [**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) ステートメントを含む関数の名前を書き込み、 **DoTraceMessage** ステートメントとトレース\_ドライバー フラグ、WPP で定義されている\_コントロール\_トレース セッションの GUID が有効になっています。

    ```ManagedCPlusPlus
         DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

    ```

    この例では、現在実行中の関数 (% FUNC!) のに定義済みの文字列を使用します。 WPP に定義された書式指定文字列の詳細については、「 [wpp 拡張書式指定文字列とは](what-are-the-wpp-extended-format-specification-strings-.md)」を参照してください。

2.  トレースメッセージを生成するには、Logman または[Tracelog](tracelog.md)を使用してトレースプロバイダーのトレースセッションを作成し、トレース\_ドライバーフラグ (ビット1、0x2) を設定するトレースフラグを指定します。

```ManagedCPlusPlus
//
//  DoTraceMessage examples
// 

     ...

// writes the name of the function that contains the trace statement when the flag, TRACE_DRIVER (bit 1, 0x2), 
// as defined in WPP_CONTROL_GUIDS, is enabled for the trace session.

     DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

     ...

// writes the name of the function, the line number, and the error code 

      DoTraceMessage(
            TRACE_DRIVER,
            "[%s] Failed at %d (error code= %d)\n",
            __FUNCTION__,
            __LINE__,
            dwLastError);
```

<span id="using_traceevents"></span><span id="USING_TRACEEVENTS"></span>Visual Studio で Windows ドライバーテンプレートを使用している場合、 **Traceevents**マクロはトレース .h ヘッダーファイルに定義されています。

**TraceEvents ステートメントの使用**

1.  デバッグ印刷ルーチンの場合と同様に、 **Traceevents**マクロをコードに追加します。 **Traceevents**マクロは、トレースレベル (*レベル*) とトレースフラグ (*Flags*) のパラメーターを受け取ります。このフラグは、トレースメッセージが書き込まれるときの条件、*メッセージ*文字列、および省略可能な変数リストを定義します。

    ```
    TraceEvents(Level, Flags, Message, [VariableList... ]
    ```

    たとえば、次の**traceevents**ステートメントは、[トレースレベル](trace-level.md)およびトレースフラグパラメーターで指定された条件が満たされた場合に、 **traceevents**ステートメントを含む関数の名前を書き込みます。 トレースレベルは整数値です。トレースセッションに対して指定されたトレースレベル以下のすべてのものがトレースされます。 トレース\_レベルの\_情報は Evntrace で定義され、値は4です。 トレース\_ドライバフラグ (ビット1、0x2) は、WPP\_制御\_GUID で定義されます。 トレースセッションに対してこのトレース\_ドライバービットが設定されており、トレースレベルが4以上の場合、 **Traceevents**はトレースメッセージを書き込みます。

    ```ManagedCPlusPlus
            TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    ```

    この例では、現在実行中の関数 (% FUNC!) のに定義済みの文字列を使用します。 WPP に定義された書式指定文字列の詳細については、「 [wpp 拡張書式指定文字列とは](what-are-the-wpp-extended-format-specification-strings-.md)」を参照してください。

2.  トレースメッセージを生成するには、Logman または[Tracelog](tracelog.md)を使用して、トレースプロバイダーのトレースセッションを作成します。 トレースレベルを指定して\_レベル\_情報 (4) 以上をトレースし、トレース\_ドライバービット (ビット1、0x2) を設定するトレースレベルを指定します。

```ManagedCPlusPlus
//
//  TraceEvents examples
// 


    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

//


    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_INIT,
                       "OSRUSBFX2 Driver Sample - Driver Framework Edition.\n");

    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_INIT,
                "Built %s %s\n", __DATE__, __TIME__);
```

## <a name="step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution"></a>手順 6: WPP プリプロセッサを実行し、ソリューションをビルドするように Visual Studio プロジェクトを変更する


WDK は、 [WPP プリプロセッサ](wpp-preprocessor.md)をサポートしているので、Visual Studio と MSBuild 環境を使用してプリプロセッサを実行できます。

**WPP プリプロセッサを実行するには**

1.  ソリューションエクスプローラーでドライバープロジェクトを右クリックし、[プロパティ] をクリックし**ます。**
2.  プロジェクトのプロパティページで、 **[構成プロパティ]** をクリックし、 **[WPP トレース]** をクリックします。
3.  **[全般]** で、 **[実行する WPP]** オプションを **[はい]** に設定します。
4.  **[コマンドライン]** で、トレース動作をカスタマイズするためのオプションを追加します。 追加できる内容の詳細については、「 [WPP プリプロセッサ](wpp-preprocessor.md)」を参照してください。
5.  ターゲットの構成とプラットフォームに合わせて、プロジェクトまたはソリューションをビルドします。 「 [WDK を使用](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)したドライバーの構築」を参照してください。

ビルドプロセスの詳細については、「 [Tracewpp タスク](tracewpp-task.md)」と「 [WDK と Visual Studio のビルド環境](wdk-and-visual-studio-build-environment.md)」を参照してください。

また、TraceWPP ツール (TraceWPP) を使用して、ビルド環境とは別にプリプロセッサを実行することもできます。 このツールは、WDK の bin/x86 および bin/x64 サブディレクトリにあります。

## <a name="step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages"></a>手順 7: トレースセッションを開始してトレースメッセージをキャプチャし、検証する


WPP トレースを正しく設定したことを確認するには、ドライバーまたはアプリケーションをテストコンピューターにインストールし、トレースセッションを作成してトレースメッセージをキャプチャする必要があります。 Logman、 [Tracelog](tracelog.md)、 [tracelog](traceview.md)などの任意のトレースコントローラーを使用して、トレースプロバイダーのトレースセッションを作成できます。 メッセージをログファイルに書き込むか、またはカーネルデバッガーに送信することができます。 使用するトレースメッセージ関数によっては、メッセージを生成するトレースフラグとトレースレベルを必ず指定してください。

たとえば、Evntrace で定義されているトレースレベルを使用していて、トレース\_レベル\_情報 (4) 以上をキャプチャする場合は、レベルを4に設定する必要があります。 トレースセッションのレベルを4に設定すると、トレースフラグなどの他の条件が満たされている場合に、すべての情報 (4)、警告 (3)、エラー (2)、および重大 (1) メッセージもキャプチャされます。

すべてのメッセージが生成されたことを確認するには、トレースレベルとトレースフラグを最大値に設定して、すべてのメッセージが生成されるようにします。 トレースフラグは、ビットマスク (ULONG) を使用するので、すべてのビット (たとえば 0xFFFFFFFF) を設定できます。 トレースレベルは、バイト値で表されます。 たとえば、Logman を使用している場合は、すべてのレベルをカバーするために、0xFF を指定できます。

ようLogman を使用したトレースセッションの開始

```
logman create trace "myWPP_session" -p {11C3AAE4-0D88-41b3-43BD-AC38BF747E19} 0xffffffff 0xff -o c:\DriverTest\TraceFile.etl 

logman start "myWPP_session"

logman stop "myWPP_session"
```

ようTraceLog を使用したトレースセッションの開始

```
tracelog -start MyTrace -guid  MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

[Tracelog](tracelog.md)コマンドには、イベントトレースログファイルの名前と場所を指定する **-f**パラメーターが含まれています。 フラグの設定を指定する **-flag**パラメーターと、レベルの設定を指定する **-level**パラメーターが含まれています。 これらのパラメーターは省略できますが、フラグまたはレベルを設定しない限り、トレースプロバイダーによってはトレースメッセージが生成されません。 トレース[レベル](trace-level.md)は Evntrace ファイルで定義されており、トレースレベルは、重要、エラー、警告、および情報メッセージとしてトレースメッセージを分類するための便利な方法を提供します。









