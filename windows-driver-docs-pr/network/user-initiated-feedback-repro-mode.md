---
title: ユーザーが開始したフィードバック - 再現モード
description: このトピックでは、WDI ドライバーでのログ記録 IHV トレースでユーザーが開始したフィードバックの再現コード モードをについて説明します。
ms.assetid: C9784C2D-75B1-4229-A219-748C52F430D5
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: bed127cb83a53ab8f507a9e590a40ba55468196f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366540"
---
# <a name="user-initiated-feedback---repro-mode"></a>ユーザーが開始したフィードバック - 再現モード

ユーザーが開始したフィードバック (し) 再現コード モードは、ユーザーがバグを再現中より詳細なログ記録を収集するシステムを許可します。 標準モードのようにはこれも、IHV で定義された ETW プロバイダーを使用した新しい WMI ログ セッションを作成して実現されます。 再現コードのモードが完了したら、詳細ログが収集し、分析のため Microsoft に送信します。 有効化またはファームウェアの詳細なログを無効にする拡張機能ポイントを IHV があります。 再現コードのログは、顧客の問題が発生する理由を追跡できるより詳細なが意図されています。 そのため、再現コード モードは、ログのログ ファイルのサイズは 10 MB の最大サイズに設定されます。 IHV は、ETW プロバイダー フラグ/レベル/keywords の値より詳細な設定を使用する必要があります。

現在し再現モードのモデルでは、IHV フィードバックのログが含まれる前にすべてのプロバイダーの Guid、レベル、およびフラグの Microsoft に通知する必要があります。 このトピックに記載されているをレジストリにプロバイダーを追加すると、適切なレベルのログをテストする IHV ができます。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供の WMI 自動ロガー セッション

Microsoft では、初期ありません ETW プロバイダーを使用した WMI 自動ロガー セッションを提供します。 IHV のドライバーがインストールされている場合は、Microsoft 提供の WMI 自動ロガーのセッション キーの下で、WMI プロバイダーのレジストリ キーが必要なを追加があります。 IHV は、自動ロガー セッションのレジストリ値のいずれかを変更しないでください。 ただし、すべての ETW プロバイダー オプションは有効にするレベルを含む、IHV、いずれとも一致、すべて、一致するなど。

> [!IMPORTANT]
> 自動ロガーは、自動ロガーとして有効になっていることはありません。 これらの値を使用してで説明されている、再現コード モード IHV ログ記録を検証[再現モードのログをテスト](#testing-the-repro-mode-logs)します。 さらに、ユーザーを使用して手動でこれらのログを送信する可能性があります要求、`netsh`ツール。 プロバイダー Guid、レベル、およびフラグも送信する必要が、Microsoft に、ログのサンプルと共に再現モード UIFs に含まれますが、(を参照してください[を Microsoft に送信する IHV プロバイダー](#submitting-ihv-providers-to-microsoft)します。

WMI の自動ロガー セッションは、次のパス HKLM レジストリ ハイブに追加されます。

`HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSessionRepro`

結果として得られる ETL ログ ファイルはここにあります。

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSessionRepro.etl`

## <a name="ihv-driver-inf-changes"></a>IHV ドライバーの INF 変更

Ihv は、しの通常モード中に詳細ログを IHV できるように、次のレジストリ キーの値を追加する、ドライバーの INF ファイルを更新する必要があります。 次のスニペットは、自動ロガー セッションに 1 つの ETW プロバイダーを追加するためのテンプレートを提供します。 IHV は、適切に多くのプロバイダーを追加することができます。 さらに、レベルの値を有効にする ETW プロバイダーごとの IHV 固有に必ずしも付与しないように、マイクロソフトによって定義された値 (TRACE_LEVEL_CRITICAL、TRACE_LEVEL_ERROR など) と同じにします。

### <a name="add-ihv-etw-providers"></a>IHV ETW プロバイダーを追加します。

次のスニペットでは、INF ファイルで IHV ETW プロバイダーを追加する方法を示します。

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,,EnableLevel,%REG_DWORD%,<IHV_LogEnableLevelValue>
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,MatchAnyKeyword,%REG_QWORD%,<IHV_MatchAnyKewordValue>

[The following is optional]
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,MatchAllKeyword,%REG_QWORD%,<IHV_MatchAllKewordValue>

[Strings]
REG_DWORD = 0x00010001
REG_QWORD = 0x000B0001
```

### <a name="example-values"></a>値の例

この例では、すべてのキーワードを持つ、WDI UE 情報レベルの設定を示します。

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},,EnableLevel,%REG_DWORD%,0xFF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},MatchAnyKeyword,%REG_QWORD%,0x000FFFFF

Standard EnableLevel values:
0x5 - Verbose
0x4 - Informational
0x3 - Warning
0x2 - Error
0x1 - Critical
0x0 – LogAlways
```

## <a name="etw-control-callback"></a>ETW コントロールのコールバック

IHV は、ETW のログ記録コード内の ETW コントロールのコールバックを登録できます。 これにより、ETW プロバイダーを有効に、無効になっている、またはキャプチャ コントロールが開始したときに通知を IHV ができます。 これにより、IHV できるオン/オフ再現モードの詳細なファームウェア ログ。

> [!NOTE]
> ETW プロバイダーを標準と再現モードの間で共有している場合、IHV は、IHV 定義 EnableLevel、INF ファイルで定義されている開始/停止の詳細なファームウェアのログをオフ キーする必要があります。

### <a name="etw-callback-function"></a>ETW のコールバック関数

次のスニペットでは、ETW のコールバックを登録する方法を示します。 これは、重要なは、IHV は、開始と終了し再現モード (起動、ファームウェアの詳細なログ記録を停止するなど) の中に特別なアクションを実行する必要がある場合だけです。 複数の ETW プロバイダーを使用している場合、Ihv がのみファームウェアのログ記録を開始する 1 つのコールバックの実装を検討する可能性があります。 すべてのファームウェアのログ記録は、IHV の ETW トレース プロバイダーにルーティングする必要があります。 するための診断ツールのみ IHV の ETW プロバイダーのトレースが収集されます。

ETW のログ記録の実装方法によって、ETW コールバックを有効にする 2 つの方法はあります。

1. 使用して自動生成されたコードで ETWs を指します`MC.exe`します。 参照してください[、インストルメンテーション マニフェストを記述](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)の詳細。
    1. 次のスニペット (etwtracingevents.h) のヘッダーを使用して作成された自動生成された ETW イベントのヘッダーは、`MC.exe`します。 前提に、ETW イベントが既に生成されている、ため、このトピックではこの部分で説明されます。
    1. MCGEN_PRIVATE_ENABLE_CALLBACK_V2 は自動生成された ETW のヘッダーをインクルードする前に定義する必要があります。 それ以外の場合、コールバックは呼び出されません。
1. 使用して ETW コールバックの登録、 [ **EventRegister** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventregister) API。
    1. コールバックの ETW プロバイダーに渡す必要があります、 **EventRegister**トレース プロバイダーの登録時に機能します。

このスニペットは、ETW のコールバック関数のプロトタイプを示しています。

```C++
#include <evntprov.h>
extern
VOID
EtwEventControlCallback(
    _In_ LPCGUID SourceId,
    _In_ ULONG ControlCode,
    _In_ UCHAR Level,
    _In_ ULONGLONG MatchAnyKeyword,
    _In_ ULONGLONG MatchAllKeyword,
    _In_opt_ PEVENT_FILTER_DESCRIPTOR FilterData,
    _Inout_opt_ PVOID CallbackContext
    );
```

次のコードは、のみを使用して自動生成された ETW イベントを使用したかどうかに必要な`MC.exe`ツール。

```C++
#define MCGEN_PRIVATE_ENABLE_CALLBACK_V2 EtwEventControlCallback

#include "etwtracingEvents.h" // Generated from manifest - This must come 
                              // after MCGEN_PRIVATE_ENABLE_CALLBACK_V2 is                   
                              // defined
```

*ControlCode* ETW コールバックのパラメーターは、プロバイダーを有効または無効になっていることを示します。 値が定義されている`<evntrace.h>`され、次の値。

```C++
#define EVENT_CONTROL_CODE_DISABLE_PROVIDER 0
#define EVENT_CONTROL_CODE_ENABLE_PROVIDER  1
#define EVENT_CONTROL_CODE_CAPTURE_STATE    2
```

#### <a name="eventcontrolcodeenableprovider"></a>EVENT_CONTROL_CODE_ENABLE_PROVIDER

このフラグは、ETW プロバイダーを有効にし、しの再現コード モードのセッションが開始されたことを示します。 詳細なファームウェアのログ記録やパケットのログ記録を開始するために使用する必要があります。

#### <a name="eventcontrolcodedisableprovider"></a>EVENT_CONTROL_CODE_DISABLE_PROVIDER

このフラグは、ETW プロバイダーを無効になり、しの再現コード モードのセッションが終了したことを示します。 IHV の実装がフラッシュし、場合、この時点でファームウェアのログをリセットする必要があります、*レベル*パラメーターに一致する INF ファイル (次のセクションのサンプルでは 0 xff) で IHV 指定し、再現コードのモード レベル。

#### <a name="eventcontrolcodecapturestate"></a>EVENT_CONTROL_CODE_CAPTURE_STATE

このフラグを要求の状態情報をプロバイダーがログに記録します。 これは一般に、メモリ内のログをディスクにフラッシュする呼び出されます。 IHV の実装がフラッシュし、場合、この時点でファームウェアのログをリセットする必要があります、*レベル*パラメーターに一致する INF ファイル (次のセクションのサンプルでは 0 xff) で IHV 指定し、再現コードのモード レベル。

### <a name="sample-code"></a>サンプル コード

詳細なドライバーとファームウェア ログし再現モードのシナリオを有効にするテンプレートとして使用できる ETW コールバック実装の例を次に示します。

> [!NOTE]
> Ihv は、両方の保留中のログのファームウェアをフラッシュする必要があります、 **EVENT_CONTROL_CODE_CAPTURE_STATE**と**EVENT_CONTROL_CODE_DISABLE_PROVIDER**コードを制御します。

後に、 **EVENT_CONTROL_CODE_CAPTURE_STATE**が呼び出されると、し診断ツールは、ETW のコールバックを呼び出します 2 回以上で、 **EVENT_CONTROL_CODE_ENABLE_PROVIDER**コードを制御します。 そのため、ファームウェアのログ記録を再度有効にするを避けるためには、ステート マシンを移動しますから、 *ReproModeStateCaptured*状態、 *ReproModeStateFinal*状態に戻す前に、 *ReproModeStateNotStarted*状態。 **EVENT_CONTROL_CODE_DISABLE_PROVIDER**制御コードは、プロバイダーを無効にするのみ使用されます。 これは、しプロセスの一部ではありませんが、まだ有効である必要があります。

Ihv を変更する必要があります、 **IHV_ETW_REPRO_MODE_LEVEL**の INF ファイルで設定再現モード レベルに一致する次の例の値。

```C++
#define IHV_ETW_REPRO_MODE_LEVEL 0xFF // This value must match the repro mode              
                                      // EnableLevel INF value

typedef enum _EtwReproModeState
{
    ReproModeStateNotStarted = 0,
    ReproModeStateStarted,
    ReproModeStateCaptured,
    ReproModeStateFinal
} EtwReproModeState;
 
static EtwReproModeState g_eReproModeLoggingEnabled = ReproModeStateNotStarted; 

VOID
EtwEventControlCallback(
    _In_ LPCGUID SourceId,
    _In_ ULONG ControlCode,
    _In_ UCHAR Level,
    _In_ ULONGLONG MatchAnyKeyword,
    _In_ ULONGLONG MatchAllKeyword,
    _In_opt_ PEVENT_FILTER_DESCRIPTOR FilterData,
    _Inout_opt_ PVOID CallbackContext
    )
{
    UNREFERENCED_PARAMETER(SourceId);
    UNREFERENCED_PARAMETER(MatchAnyKeyword);
    UNREFERENCED_PARAMETER(MatchAllKeyword);
    UNREFERENCED_PARAMETER(FilterData);
    UNREFERENCED_PARAMETER(CallbackContext);

    switch(ControlCode)
    {
        case EVENT_CONTROL_CODE_ENABLE_PROVIDER:
            if (Level == IHV_ETW_REPRO_MODE_LEVEL)
            {
                switch(g_eReproModeLoggingEnabled)
                {
                    case ReproModeStateNotStarted:
                        //
                        // Enable verbose Firmware logs.
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateStarted;
                        break;

                    case ReproModeStateCaptured:
                        //
                        // The diagnostic tools will invoke the callback after
                        // the capture with EVENT_CONTROL_CODE_ENABLE_PROVIDER
                        // twice. 
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateFinal;
                        break;

                    case ReproModeStateFinal:
                        //
                        // The state machine is now complete, reset the state.
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateNotStarted;
                        break;

                    case ReproModeStateStarted:
                    default:
                        break;
                }
            }
            break;  

        case EVENT_CONTROL_CODE_DISABLE_PROVIDER:
            if (g_eReproModeLoggingEnabled == ReproModeStateStarted) 
            {
                // 
                // Merge verbose firmware logs into ETW log (if not done already).
                // Disable verbose firmware logs
                // 
                g_eReproModeLoggingEnabled = ReproModeStateNotStarted;
            }
            break;

        case EVENT_CONTROL_CODE_CAPTURE_STATE:
            if (Level == IHV_ETW_REPRO_MODE_LEVEL &&
                g_eReproModeLoggingEnabled == ReproModeStateStarted)
            {
                // 
                // Merge verbose firmware logs into ETW log (if not done already).
                // Disable verbose firmware logs
                // 
                g_eReproModeLoggingEnabled = ReproModeStateCaptured;
            }
            break;  
    }
}
```

## <a name="testing-the-repro-mode-logs"></a>再現コード モードのログをテストします。

IHV 再現モードのログをテストするには、開始およびキャプチャを停止する次のコマンドを使用できます。 

> [!NOTE]
> 結果として得られる ETL ファイルは、いくつかの OS のログが格納されます。

- netsh wlan IHV startlogging
- netsh wlan IHV stoplogging

これらのコマンドは、手動でデバイスからログを収集する顧客も使用されます。

## <a name="submitting-ihv-providers-to-microsoft"></a>IHV プロバイダーが Microsoft に送信します。

再現コード モードのユーザーが開始したフィードバックを送信する ihv 向けの最後の手順では、Microsoft に連絡し、要求されたプロバイダーの Guid、レベル、およびレビューのためのサンプル ログ データと共にフラグを指定します。 ログ記録が承認されると、プロバイダーは、ユーザーが開始したフィードバック システムに追加されます。 

> [!NOTE]
> プロバイダー Guid、レベル、またはフラグを変更に送信された後に、しログへの影響はありません。

## <a name="related-links"></a>関連リンク

[IHV のトレース ログ記録でフィードバックをユーザーが開始しました。](user-initiated-feedback-with-ihv-trace-logging.md)

[ユーザーによって開始されたフィードバック - 標準モード](user-initiated-feedback-normal-mode.md)
