---
title: DTrace ETW
description: DTrace では、LKD () を使用したライブダンプファイルの作成がサポートされています。
ms.assetid: bbf23d76-423d-4d1e-afde-83739015bbf1
keywords:
- DTrace WDK
- ソフトウェアトレース WDK、DTrace
- トレースメッセージの表示
- トレースメッセージの書式設定 WDK DTrace
- トレースメッセージの書式設定 WDK DTrace
- ソフトウェアトレース WDK, 書式設定メッセージ
- WDK のトレース、DTrace
- トレースメッセージフォーマットファイル WDK
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: cb08888529dda9234e01e30bf765e1dca9c3f46d
ms.sourcegitcommit: 5081de283b09b4fe847912fc1dc0e7f057e0a0cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73592428"
---
# <a name="dtrace-live-dump"></a>DTrace ライブダンプ

DTrace は、lkd () を使用して、D スクリプト内からライブダンプをキャプチャする機能を提供します。 メモリダンプファイルは、windows デバッガーを使用して Windows の複雑な問題をデバッグするために使用されます。 詳細については、「WinDbg を使用した[クラッシュダンプファイルの分析](https://docs.microsoft.com/windows-hardware/drivers/debugger/crash-dump-files)」を参照してください。 デバッガーをダウンロードするには、「 [WinDbg Preview-Installation](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)」を参照してください。

 DTrace ライブダンプには、エラーが発生した時点でダンプをトリガーする機能が用意されています。 たとえば、エラーは、エラーを返す関数である可能性があります。 DTrace を使用してこの関数にフックし、戻り値が "error" のときにライブダンプをトリガーできます。

> [!NOTE]
> DTrace は、バージョン18980および Windows Server Insider Preview ビルド18975以降の Windows の Insider ビルドでサポートされています。

Windows での DTrace の使用に関する一般的な情報については、「 [dtrace](dtrace.md)」を参照してください。

## <a name="dtrace-live-dump-usage"></a>DTrace のライブダンプの使用

使用法: **lkd (パラメーター);**

ライブミニダンプに含まれる情報を変更するには、次のオプションを設定します。

0x0-完全なカーネルダンプ (既定値)

0x1-ユーザーページ + カーネルページ (KD attach でのみ機能)

0x2-ミニダンプ

0x4-hyper-v ページ + カーネルページ)

0x5-ユーザー、カーネル、ハイパーバイザーページ。

## <a name="live-dump-example-code"></a>ライブダンプのサンプルコード

```dtrace
#pragma D option destructive

inline uint32_t STATUS_UNSUCCESSFUL = 0xc0000001UL;

syscall:::return
{ 
    this->status = (uint32_t)arg0;

    if (this->status == STATUS_UNSUCCESSFUL)
    { 
        printf ("Return value arg0:%x \n", this->status);
        printf ("Triggering LiveDump \n");
        lkd(0);
        exit(0);
    }
}
```

ファイルを livedumpstatuscheck として保存します。

管理者としてコマンドプロンプトを開き、-s オプションを使用してスクリプトを実行します。

```dtrace
C:\Windows\System32>dtrace -s livedumpstatuscheck.d
dtrace: script 'livedumpstatuscheck.d' matched 1881 probes
dtrace: allowing destructive actions
CPU     ID                    FUNCTION:NAME
  0     93 NtAlpcSendWaitReceivePort:return Return value arg0:c0000001
Triggering LiveDump
```

作成されるダンプファイルは、通常 `C:\Windows\LiveKernelReports`にあります。

ダンプファイルの場所が変更されている場合、値は次のレジストリキーに格納されます: `hklm\system\currentcontrolset\control\crashcontrol\livekernelreports`

上で説明したように、WinDbg を使用してダンプファイルを操作します。

## <a name="troubleshooting"></a>[トラブルシューティング]

### <a name="viewing-live-dump-related-events"></a>ライブダンプ関連のイベントの表示

Windows イベントビューアーを開きます。 アプリケーションとサービスログ-> Microsoft-> Windows-> Kernel-Livedump-> Operational を参照してください。

ログが見つからない場合は、次に示すように、コマンドプロンプトまたはイベントビューアーから分析チャネルを有効にします。

**コマンドプロンプトから分析チャネルを有効にする**

このコマンドを使用して、および管理者コマンドプロンプトから分析チャネルを有効にします。

`wevtutil sl Microsoft-Windows-Kernel-LiveDump/Analytic /e:true`

**イベントビューアーを使用して分析チャネルを有効にする**

1. Windows イベントビューアーを開始する

2. [表示] をクリックし、[分析およびデバッグログの表示] をオンにします。 これにより、livedump の分析チャネルが表示されます。

3. を右クリックして、 *LiveDump/分析*を有効にします。

### <a name="enabling-full-live-dumps"></a>完全なライブダンプを有効にする

次の例の設定では、任意の時点でディスク上に存在する可能性がある完全なライブダンプの最大数を10に設定し、ミニダンプだけでなく、完全なメモリダンプを格納します。

`reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v FullLiveReportsMax /d 10`

`reg add "HKLM\System\CurrentControlSet\Control\CrashControl" /f /t REG_DWORD /v AlwaysKeepMemoryDump /d 1`

これらの設定の詳細については、「 [WER の設定](https://docs.microsoft.com/windows/win32/wer/wer-settings)」を参照してください。

### <a name="disable-throttling"></a>調整を無効にする

調整は、ダンプとログ記録システムが Windows の通常の使用に影響を及ぼさないようにする機能です。 この機能は、特定のリソースの制約付き環境でのライブダンプの作成に干渉する可能性があります。

次に示すように、SystemThrottleThreshold キーと ComponentThrottleThreshold キーを0に設定してスロットルを無効にして、ライブダンプスロットルの設定を確認し、必要に応じて再試行します。

```registry
reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v SystemThrottleThreshold /d 0
reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v ComponentThrottleThreshold /d 0
```

### <a name="disk-space-issues-event-id-202--error-text-live-dump-write-deferred-dump-data-api-ended-nt-status-0xc000007f"></a>ディスク領域の問題 (イベント ID 202-エラーテキスト: ライブダンプ書き込み遅延ダンプデータ API が終了しました。 NT ステータス: 0xC000007F)

これは、ディスク領域が不足していることを意味します。 次のレジストリキーを更新して、ライブダンプ作成のパス (この例では、追加の記憶領域があるドライブ d) を変更します。

`reg add hklm\system\currentcontrolset\control\crashcontrol\livekernelreports /v "LiveKernelReportsPath" /t reg_sz /d "\??\d:\livedumps"`

このコマンドは、ライブダンプルートパスを `d:\livedumps` (例として) に設定します。

フォルダーは OS によって管理されるため、手動で作成しないでください。適切なアクセス許可でダンプがトリガーされたときに作成されます。

## <a name="see-also"></a>参照

[Windows 上の DTrace](dtrace.md)

[DTrace の Windows プログラミング](dtrace-programming.md)

[DTrace Windows コードサンプル](dtrace-code-samples.md)
