---
title: Windows ドライバーへの WPP ソフトウェア トレースの追加
description: カーネル モード ドライバーなど、ユーザー モード アプリケーションのトレース プロバイダーを使用して、WPP ソフトウェア トレースを使用するにはコード (またはインストルメント化) ドライバーのソース ファイルを追加およびドライバーのプロジェクトを変更する必要があります。 このセクションでは、これらの手順を説明します。
ms.assetid: 487BA8AA-950A-4F3C-9E3E-EBE1DA35D4B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0755dd805032549faaca00bfb4185fac858ffc5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332054"
---
# <a name="adding-wpp-software-tracing-to-a-windows-driver"></a>Windows ドライバーへの WPP ソフトウェア トレースの追加

カーネル モード ドライバーなど、ユーザー モード アプリケーションのトレース プロバイダーを使用して、WPP ソフトウェア トレースを使用するにはコードを追加する必要があります (または*インストルメント化*) ドライバーのソース ファイルとドライバーのプロジェクトを変更します。 このセクションでは、これらの手順を説明します。

**ヒント:** WPP トレースには、ドライバーを追加する最も簡単な方法は、Visual Studio で KMDF または UMDF ドライバー テンプレートのいずれかを使用します。 テンプレートを使用する場合に追加する必要があるコードの多くは既にが行われます。 Visual Studio で、次のようにクリックします。**ファイル&gt;新規&gt;プロジェクト**、Windows Driver (ユーザー モードまたはカーネル モード) WDF プロジェクトを選択します。 WPP マクロは、プロジェクトの一部として含まれている Trace.h ヘッダー ファイルで定義されます。 テンプレートのいずれかを使用する場合に進んでかまいません[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)します。 

-   [ステップ 1: コントロールの GUID とトレース フラグを定義します。](#step-1-define-the-control-guid-and-trace-flags)
-   [手順 2:使用してこれらの関数の WPP マクロを定義するトレース メッセージ機能を選択します。](#step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions)
-   [手順 3:C または C++ ソース ファイルに関連付けられているトレースのヘッダー ファイル (.h および .tmh) を含める](#step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files)
-   [手順 4:WPP を初期化してクリーンアップするには、適切なコールバック関数にマクロを追加します。](#step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp)
-   [手順 5:適切な時点でのトレース メッセージを生成するドライバーのコードをインストルメント化](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)
-   [手順 6:WPP プリプロセッサを実行し、ソリューションを構築するには、Visual Studio プロジェクトを変更します。](#step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution)
-   [手順 7:キャプチャし、トレース メッセージを確認します。 トレース セッションを開始します。](#step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages)

## <a name="step-1-define-the-control-guid-and-trace-flags"></a>手順 1:コントロールの GUID とトレース フラグを定義します。

(ドライバー、またはユーザー モード アプリケーションの場合) などのすべてのトレース プロバイダーを一意に定義する必要があります。 追加することで、これを行う、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)コントロールの GUID、識別子、およびトレース フラグを定義するマクロです。 これは、識別して、何をトレースするときに制御できるようにします。 各ドライバーには、通常は別のコントロールの GUID が、ドライバーは Guid では、複数のコントロールがある可能性があります。 または複数のドライバーが 1 つのコントロールの GUID を共有できます。

便宜上、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロは通常、共通のヘッダー ファイルで定義されています。 ヘッダー ファイルを含める必要があります (\#が含まれます) のトレースをインストルメント化する任意のソース ファイル。

**WPP を追加する\_コントロール\_ドライバーにマクロを GUID:**

1.  新しい C++ ヘッダー ファイルを WPP トレース マクロを定義するために使用できる Visual Studio プロジェクトに追加します。 たとえば、ソリューション エクスプ ローラーで、ドライバーを右クリックし、クリックして**追加&gt;新しい項目の**します。 (たとえば、Trace.h) として保存します。

2.  追加、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロと特定のトレース メッセージを修飾するために使用できるトレース フラグを定義するトレース プロバイダーのフレンドリ名を指定するには、GUID、コントロールを定義します。

    [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロには、次の構文。

    **WPP 構文\_コントロール\_GUID**

    ```ManagedCPlusPlus
    #define WPP_CONTROL_GUIDS \
        WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
            WPP_DEFINE_BIT(NameOfTraceFlag1)  \
            WPP_DEFINE_BIT(NameOfTraceFlag2)  \
            .............................   \
            .............................   \
            WPP_DEFINE_BIT(NameOfTraceFlag31) 
    ```

    たとえば、次のコードが myDriverTraceGuid としてを使用して、 *GUIDFriendlyName*します。 なお*ControlGUID* 32 桁の 16 進数の GUID の標準の形式よりもわずかに異なる形式にします。 *ControlGUID*は 5 つのフィールドがありますが、コンマで区切られた、通常ハイフンと中かっこの代わりに、かっこで囲まれています。 たとえば、指定 ( **(84bdb2e9、829e、41b3、b891、02f454bc2bd7)** {84bdb2e9-829e-41b3-b891-02f454bc2bd7} の代わりにします。

    **例、WPP の\_コントロール\_GUID ステートメント**

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

    **ヒント:** ヘッダー ファイルに次のコード スニペットをコピーすることができます。 コントロールの GUID とフレンドリ名を変更することを確認します。 GUIDgen.exe を使用して、コントロールの GUID を生成することができます。 Guidgen.exe は Visual Studio に含まれている (**ツール&gt;GUID の作成**)。 Visual Studio コマンド プロンプト ウィンドウからアクセスできる Uuidgen.exe ツールを使用することもできます (型**uuigen.exe/でしょうか。** 詳細については)。



3.  定義、[トレース フラグ](trace-flags.md)トレース プロバイダー。

    WPP\_定義\_WPP のビット要素\_コントロール\_GUID マクロは、トレース プロバイダーのトレース フラグを定義します。 通常、フラグがしだいに詳細レポートのレベルを表しますが、トレース メッセージを生成するための条件として任意の方法としてフラグを使用することができます。 WPP\_コントロール\_GUID など、WPP\_定義\_ビットは 4 つのトレース フラグを定義します (MYDRIVER\_すべて\_情報、トレース\_ドライバーでは、トレース\_デバイス、およびトレース\_キュー)。

    最大 31 個のトレース フラグを定義することができます。 WPP が表示される順序、たとえば内の要素をビット値を割り当てます、ビット 0 (0x1)、ビット 1 (0x2)、ビット 2 (0x4)、ビット 3 (0x8) がこれにします。 ソース コードにトレース メッセージの関数を追加すると、トレース フラグを使用する (で説明されている[手順 5。適切な時点でのトレース メッセージを生成するドライバーのコードをインストルメント化](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points))。

    **注**トレース フラグの使用を制御できます (I/O 要求、またはデバイスまたはドライバーのオブジェクトのアクティビティの特定など) の特定のコンポーネントをトレースするときにします。 トレース メッセージの明細書に、トレース フラグを追加する (たとえば、`DoTraceMessage (TRACE_DRIVER, "Hello World!\n")`します。 トレース コント ローラーでトレース セッションを作成するときのような[Tracelog](tracelog.md)を指定する、 **-フラグ**そのセッションで、この場合、フラグ、トレース プロバイダーを使用するオプションは、ビット 1 (0x1)、対応します。トレースに\_ドライバー フラグ。 トレース セッションを開始するときに、トレース フラグを指定するすべてのトレース メッセージは、ログに書き込まれます。



## <a name="step-2-choose-which-trace-message-functions-you-intend-to-use-and-define-the-wpp-macros-for-those-functions"></a>手順 2:使用してこれらの関数の WPP マクロを定義するトレース メッセージ機能を選択します。


デバッグは、関数を印刷するようにトレース メッセージの関数は、トレース メッセージを記述するコードを追加する関数 (またはマクロ)。

**トレース メッセージの関数を選択します。**

1.  既定のトレース メッセージの関数は、 [ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)マクロ。 使用してメッセージを生成するタイミングを制御することができます、既定の関数を使用する場合、[トレース フラグ](trace-level.md)プロバイダーの値。 トレース フラグの値は、手順 1. でコントロールの GUID を作成するときに定義するフラグです。 使用する場合**DoTraceMessage**、既定の WPP マクロが既に定義した (WPP\_レベル\_有効] と [WPP\_レベル\_ロガー) ので、この手順の残りの部分をスキップしてに移動することができます[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)します。

2.  KMDF または UMDF のテンプレートのいずれかを使用している場合、 **TraceEvents**にスキップできるように、この関数を有効にする関数と必要な WPP マクロが定義済み[手順 5](#step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points)します。

3.  独自のトレース メッセージの関数を作成する、または既存のデバッグを変換する関数を印刷は、この手順の残りの部分を続行します。

**作成またはトレース メッセージの関数のカスタマイズ**

1.  カスタム トレース メッセージの関数を使用している場合、またはデバッグ出力関数を変換する場合 (たとえば、 [ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)) トレース メッセージを生成するには、識別を有効にする WPP マクロを定義する必要があります、トレース プロバイダーでのトレース メッセージの関数。 Trace.h ヘッダー ファイルをプロジェクトに追加するには、これらのマクロを配置します。

2.  トレース機能を有効にする WPP マクロを定義します。

    使用する各トレース メッセージの関数は、対応するマクロのペアが必要です。 これらのマクロでは、トレース プロバイダーを識別し、メッセージを生成する条件を指定します。 通常、マクロのペアを定義する**WPP\_ *&lt;条件&gt;* \_ロガー**と**WPP\_ *&lt;条件&gt;* \_有効**既定 WPP の観点から\_レベル\_有効] と [WPP\_レベル\_ロガー マクロ。

使用する各トレース メッセージの関数は、対応するマクロのペアが必要です。 これらのマクロでは、トレース プロバイダーを識別し、メッセージを生成する条件を指定します。 通常、マクロのペアを定義する**WPP\_ *&lt;条件&gt;* \_ロガー**と**WPP\_ *&lt;条件&gt;* \_有効**既定 WPP の観点から\_レベル\_有効] と [WPP\_レベル\_ロガー マクロ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="WPP_CONDITIONS_LOGGER"></span><span id="wpp_conditions_logger"></span><strong>WPP_<em>条件</em><em>ロガー</strong></p></td>
<td align="left"><p>トレース セッションのプロバイダーに関連付けられているし、セッション ハンドルを返しますを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="WPP_CONDITIONS_ENABLED"></span><span id="wpp_conditions_enabled"></span><strong>WPP</em><em>条件</em>_ENABLED</strong></p></td>
<td align="left"><p>指定した条件でログ記録が有効になっているかどうかを判断するために使用します。</p></td>
</tr>
</tbody>
</table>



WPP マクロを定義する、*条件*トレース メッセージの関数をサポートするアンダー スコアで区切られた、関数のパラメーター リストに表示される順序で条件を表します。 たとえば、既定トレース メッセージの関数、 [ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)、のみをサポートする[トレース フラグ](trace-level.md)条件としてためがのみ 1 つのパラメーター (WPP マクロ名\_レベル\_有効)。

**注**残念ながら、デフォルトのマクロの名前 (WPP\_レベル\_有効] と [WPP\_レベル\_ロガー) ように、[トレース レベル](trace-level.md)パラメーターが、実際には、トレース フラグを参照してください。



カスタム トレース メッセージの関数を使用する場合、追加の修飾子をなど設定できます、[トレース レベル](trace-level.md)します。 トレース レベルは Evntrace.h ファイルで定義され、トレース レベルは、エラー、警告、および情報メッセージとして、トレース メッセージを分類するのに便利な方法を提供します。

たとえば、プロジェクトに追加するヘッダー ファイルに次のコード スニペットを追加できます。 次のコードは、トレース メッセージ関数の両方をサポートするカスタム WPP マクロを定義します。[トレース レベル](trace-level.md)とトレース メッセージを生成する条件としてトレース フラグ パラメーター。 **WPP\_レベル\_フラグ\_有効**マクロは、指定したフラグの値のログ記録が有効になっているしが有効なレベルの値がで使用されるレベルの引数以上の場合に TRUE を返します、トレース メッセージの関数呼び出し。

```ManagedCPlusPlus
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)
```

次に、WPP 構成ブロックで、カスタム トレース関数を指定する必要があります (**開始\_wpp config**と**エンド\_wpp**) の例では、UMDF または KMDF、テンプレートを使用する場合Visual Studio でのドライバーのプロジェクト、テンプレートが呼び出されるカスタムのトレース メッセージの関数の WPP マクロを定義する**TraceEvents**します。 **TraceEvents**マクロ関数を使用して[トレース レベル](trace-level.md)およびメッセージを生成するための条件としてトレース フラグ。 定義している場合、 **WPP\_レベル\_フラグ\_有効**マクロ、Trace.h ヘッダー ファイルで、次のマクロ定義を追加することができます。

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

既存のデバッグの print ステートメントをトレースに変換することもできますステートメント同様、追加されたメッセージ**FUNC** WPP 構成ブロックで宣言します。 たとえば、次の例は既存を変換するコードを追加します。 [ **KdPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff548092)ステートメント。 **FUNC**もグローバルに宣言を定義、 **KdPrint** 、指定されたトレース レベルとフラグを使用する {0} レベル トレースを =\_レベル\_情報、フラグ = トレース\_ドライバー}。 デバッガーに出力を送信する代わりに、デバッグの print ステートメントは、トレース ログに送信されます。

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

**注**変換したい場合[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)トレース メッセージの関数には、いくつかの余分な手順を実行する必要があります。 比較して[ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)、 **KdPrintEx**関数は 2 つの引数を受け取ります。 変換する、 **KdPrintEx**関数を定義する必要があります、 **WPP\_定義\_ビット**の*ComponentID*、カスタム定義と**WPP\_ *&lt;条件&gt;* \_ロガー**と**WPP\_  *&lt;条件&gt;* \_有効**マクロ。 2 番目のパラメーターを**KdPrintEx**指定のレベルに似ていますが、[トレース レベル](trace-level.md)これらを再定義は必ずしも必要であるため、値します。



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

## <a name="step-3-include-the-associated-trace-header-files-h-and-tmh-in-your-c-or-c-source-files"></a>手順 3:C または C++ ソース ファイルに関連付けられているトレースのヘッダー ファイル (.h および .tmh) を含める


ヘッダー ファイル (たとえば、trace.h) で、ドライバーのコントロールの GUID とトレース フラグを定義する場合は、場所を初期化し、WPP (ステップ 4) をアンロードまたはトレース メッセージの関数、ソース ファイルのヘッダー ファイルをインクルードする必要があります。

さらに、追加する必要があります、 **\#含める**ステートメント[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)(.tmh)。 ドライバーまたはアプリケーションをビルドすると、プリプロセッサ WPP は各トレース メッセージの関数を含むソース ファイルのトレース メッセージのヘッダー ファイル (.tmh) を生成します。

```ManagedCPlusPlus
/* -- driver.c  - include the *.tmh file that is generated by WPP --*/

#include "trace.h"     /* file that defines WPP_CONFIG_GUIDS and trace flags */
#include "driver.tmh"  /* this file is auto-generated */
```

## <a name="step-4-add-macros-to-the-appropriate-callback-functions-to-initialize-and-clean-up-wpp"></a>手順 4:WPP を初期化してクリーンアップするには、適切なコールバック関数にマクロを追加します。


**ドライバーのエントリで WPP を初期化するには**

-   追加、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロを*DriverEntry*またはカーネル モード ドライバーまたは UMDF 2.0 のドライバーの日常的な*DLLMain*ユーザー モード ドライバーの日常的な (UMDF 1.x) またはアプリケーション。

**ドライバーの WPP リソースの終了をクリーンアップするには**

-   追加、 [WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)マクロ、ドライバーをアンロード ルーチン (たとえば、 *DriverContextCleanup*または*DriverUnload*) のカーネル モード ドライバーまたは UMDF 2.0ドライバー。

    ユーザー モード ドライバー (UMDF 1.x) またはアプリケーションを追加、 [WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)マクロを*DLLMain*ルーチン。

    追加することも必要があります、 [WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)マクロを*DriverEntry*ルーチンの場合、 *DriverEntry*が失敗しました。 たとえば場合、 *DriverEntry*失敗した場合、ドライバーのアンロード ルーチンは呼び出されません。 呼び出しが[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)次の例です。

WPP を使用して、カーネル モード ドライバーの使用例\_INIT\_トレースと WPP\_でクリーンアップ*DriverEntry*

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

WPP を使用して、カーネル モード ドライバーの使用例\_DriverContextCleanup でクリーンアップ

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

WPP を使用して UMDF 2.0 ドライバーの使用例\_INIT\_DriverEntry でのトレース

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

WPP の 1.0 の UMDF ドライバーの使用例\_INIT\_トレースと WPP\_DLLMain のクリーンアップ マクロ

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

## <a name="step-5-instrument-the-driver-code-to-generate-trace-messages-at-appropriate-points"></a>手順 5:適切な時点でのトレース メッセージを生成するドライバーのコードをインストルメント化


トレース メッセージの関数では、トレース フラグ、およびレベルが適切に定義されている提供された、選択すると、任意のトレース メッセージ関数を使用することができます。 既定のトレース メッセージの関数は、 [ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)マクロ。 このマクロは、ログ ファイルにメッセージを書き込むコードを追加できます。 次の表には、いくつかの定義済みのトレース メッセージの関数が一覧表示され、デバッグ トレース メッセージの作成に使用できる関数を印刷します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トレース メッセージ関数の例</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"><strong>DoTraceMessage</strong></a></td>
<td align="left"><p>これは、既定のトレース メッセージの関数です。 使用する利点<a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>ですが、関数は既に定義されています。 WPP_CONFIG_GUIDS マクロで指定したトレース フラグを使用することができます。 使用する欠点<strong>DoTraceMessage</strong>関数がのみ 1 つの条件付きパラメーターは、トレース フラグを受け取ることができます。 トレース レベルを使用する場合は、エラーまたは警告メッセージのみを記録することができますを使用する<strong>DoDebugTrace</strong>マクロ、または使用<strong>TraceEvents</strong>、トレース フラグとトレース レベルの両方を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceEvents</strong></td>
<td align="left"><p>Visual Studio で WDF のテンプレートを使用して、ドライバーを作成する場合、既定のトレース メッセージの関数になります。 使用する利点<strong>TraceEvents</strong>はトレース フラグでは、トレース メッセージの関数と<a href="trace-level.md" data-raw-source="[Trace Level](trace-level.md)">トレース レベル</a>は既に定義されています。 さらに、テンプレートには、関数の開始と終了時にログ ファイルにメッセージを書き込むインストルメンテーションも含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff548092" data-raw-source="[&lt;strong&gt;KdPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548092)"><strong>KdPrint</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548100" data-raw-source="[&lt;strong&gt;KdPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548100)"> <strong>KdPrintEx</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543632" data-raw-source="[&lt;strong&gt;DbgPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543632)"><strong>による DbgPrint</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543634" data-raw-source="[&lt;strong&gt;DbgPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543634)"> <strong>DbgPrintEx</strong></a></td>
<td align="left"><p>デバッグ印刷機能を使用する利点は、既存のデバッグの print ステートメントを変更する必要はありません。 ファイルにトレース メッセージを記録する、デバッガーでのメッセージの表示から簡単に切り替えることできます。 デバッグ印刷機能のいずれかに含めるトレース メッセージの関数をカスタマイズする場合より多くの作業を行う必要はありません。 Logman でトレース セッションを作成すると、または<a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">Tracelog</a>、別のトレース コント ローラーだけを指定するフラグとレベルは、プロバイダーの。 指定した条件を満たすデバッグ print ステートメントは、ログに出力されます。</p></td>
</tr>
</tbody>
</table>



<span id="using_dotracemessage"></span><span id="USING_DOTRACEMESSAGE"></span>
**DoTraceMessage ステートメントを使用します。**

1.  追加、 [**DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918) マクロ コード デバッグ印刷ルーチンの場合と同様にします。 **DoTraceMessage**マクロは 3 つのパラメーター: フラグ レベル (*TraceFlagName*)、トレース メッセージが書き込まれるときに、条件を定義する、*メッセージ*文字列省略可能な変数一覧。

    ```
    DoTraceMessage(TraceFlagName, Message, [VariableList... ]
    ```

    たとえば、次 [**DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918) ステートメントを含む関数の名前を書き込み、 **DoTraceMessage** ステートメントとトレース\_ドライバー フラグ、WPP で定義されている\_コントロール\_トレース セッションの GUID が有効になっています。

    ```ManagedCPlusPlus
         DoTraceMessage( TRACE_DRIVER, "\nEntering %!FUNC!" );

    ```

    例では、定義済みの文字列を使用して、現在実行中の関数 (%func!) のです。 WPP の詳細については、書式指定文字列を定義を参照してください[書式指定文字列を拡張、WPP は何ですか?。](what-are-the-wpp-extended-format-specification-strings-.md)

2.  トレース メッセージを生成するには、Logman を使用して、トレース プロバイダーのトレース セッションを作成または[Tracelog](tracelog.md)、トレースを設定するトレース フラグを指定して\_ドライバー フラグ (ビット 1、0x2)。

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

<span id="using_traceevents"></span><span id="USING_TRACEEVENTS"></span> Visual Studio で、Windows ドライバーのテンプレートを使用している場合、 **TraceEvents** Trace.h ヘッダー ファイルに自動的にマクロが定義されます。

**TraceEvents ステートメントを使用します。**

1.  追加、 **TraceEvents**マクロ コード デバッグ印刷ルーチンの場合と同様にします。 **TraceEvents**マクロは、次のパラメーター: トレース レベル (*レベル*) およびトレース フラグ (*フラグ*)、トレース メッセージが条件を定義します。書き込まれた、*メッセージ*文字列、および省略可能な変数一覧。

    ```
    TraceEvents(Level, Flags, Message, [VariableList... ]
    ```

    たとえば、次**TraceEvents**ステートメントを含む関数の名前を書き込み、 **TraceEvents**ステートメントで指定すると、条件、 [のトレースレベル](trace-level.md)トレース フラグ パラメーターが満たされているとします。 トレース レベルは、整数値。トレース レベル以下で指定されたデータのトレース セッションを追跡することです。 トレース\_レベル\_情報 Evntrace.h で定義されているし、4 の値を持ちます。 トレース\_WPP でドライバー フラグ (ビット 1、0x2) が定義されている\_コントロール\_GUID。 場合はこのトレース\_トレース セッションのドライバーのビットが設定され、トレース レベルが 4 以上**TraceEvents**トレース メッセージを書き込みます。

    ```ManagedCPlusPlus
            TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    ```

    例では、定義済みの文字列を使用して、現在実行中の関数 (%func!) のです。 WPP の詳細については、書式指定文字列を定義を参照してください[書式指定文字列を拡張、WPP は何ですか?。](what-are-the-wpp-extended-format-specification-strings-.md)

2.  トレース メッセージを生成するには、Logman を使用して、トレース プロバイダーのトレース セッションを作成または[Tracelog](tracelog.md)します。 トレースのトレース レベルを指定\_レベル\_情報 (4) 以上の場合、トレースを設定するトレース レベルを指定して\_ドライバー ビット (ビット 1、0x2)。

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

## <a name="step-6-modify-the-visual-studio-project-to-run-the-wpp-preprocessor-and-build-the-solution"></a>手順 6:WPP プリプロセッサを実行し、ソリューションを構築するには、Visual Studio プロジェクトを変更します。


WDK のサポートを提供する、 [WPP プリプロセッサ](wpp-preprocessor.md)、Visual Studio と MSBuild 環境を使用して、プリプロセッサを実行できるようにします。

**WPP プリプロセッサを実行するには**

1.  ソリューション エクスプ ローラーでドライバーのプロジェクトを右クリックし、をクリックして**プロパティ。**
2.  プロジェクトのプロパティ ページで次のようにクリックします。**構成プロパティ**クリック**WPP トレース**。
3.  **全般**設定、**実行 WPP**オプションを **はい** 。
4.  **コマンドライン**トレースの動作をカスタマイズするその他のオプションを追加します。 追加することについては、次を参照してください。 [WPP プリプロセッサ](wpp-preprocessor.md)します。
5.  プロジェクトまたはターゲットの構成とプラットフォームのためのソリューションをビルドします。 参照してください[WDK でドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)します。

ビルド プロセスの詳細については、次を参照してください。 [TraceWPP タスク](tracewpp-task.md)と[WDK と Visual Studio ビルド環境](wdk-and-visual-studio-build-environment.md)します。

TraceWPP ツール (TraceWPP.exe) を使用して、ビルド環境から個別のプリプロセッサを実行することもできます。 このツールは、WDK の bin/x86 および x64 bin サブディレクトリにあります。

## <a name="step-7-start-a-trace-session-to-capture-and-verify-your-trace-messages"></a>手順 7:キャプチャし、トレース メッセージを確認します。 トレース セッションを開始します。


WPP の設定を確認する正しくトレース、する必要があります、ドライバーまたはアプリケーションをテスト コンピューターにインストールして、トレース メッセージをキャプチャするトレース セッションを作成します。 トレース セッションを作成するには、Logman などの任意のトレース コント ローラーを使用して、トレース プロバイダーの[Tracelog](tracelog.md)、または[traceview で](traceview.md)します。 メッセージのログ ファイルに書き込まれるか、カーネル デバッガーに送信されることができます。 使用するトレース メッセージの関数によっては、必要がありますにするトレース フラグと、メッセージを生成するトレース レベルを指定します。

Evntrace.h で定義されているトレース レベルを使用してであると、トレースをキャプチャする場合など、\_レベル\_情報 (4) 以上、またはレベルを 4 に設定する必要があります。 すべての情報 (4) は、トレース セッションのレベルを 4 に設定すると、警告 (3) エラー (2)、および重大なメッセージが (1) がキャプチャすることも、トレース フラグなど、他の条件が満たされてもと仮定するとします。

すべてのメッセージが生成されることを確認するに場合がありますだけ設定するレベルのトレースとトレース フラグに最大値をすべてのメッセージが生成されるようにします。 トレース フラグは、ため (たとえば、0 xffffffff) のすべてのビットを設定する可能性があります (ULONG)、ビット マスクを使用します。 トレース レベルは、バイト値で表されます。 たとえば、使用する場合、Logman を指定することがの 0 xff まではすべてのレベルについて説明します。

(例)Logman を使用してトレース セッションを開始します。

```
logman create trace "myWPP_session" -p {11C3AAE4-0D88-41b3-43BD-AC38BF747E19} 0xffffffff 0xff -o c:\DriverTest\TraceFile.etl 

logman start "myWPP_session"

logman stop "myWPP_session"
```

(例)トレース ログを使用してトレース セッションを開始します。

```
tracelog -start MyTrace -guid  MyProvider.guid -f d:\traces\testtrace.etl -flag 2 -level 0xFFFF
```

[Tracelog](tracelog.md)コマンドが含まれています、 **-f**イベント トレース ログ ファイルの場所と名前を指定するパラメーター。 含まれています、 **-フラグ**フラグ セットを指定するパラメーター、および **-レベル**レベルの設定を指定するパラメーター。 これらのパラメーターを省略できますが、一部のトレース プロバイダー メッセージは生成されず、トレース フラグまたはレベルを設定していない場合。 [トレース レベル](trace-level.md)Evntrace.h のファイルで定義されたトレース レベルは、重要としてトレース メッセージ、エラー、警告、および情報メッセージを分類する便利な方法を提供します。









