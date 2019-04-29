---
title: ユーザーが開始したフィードバック - 標準モード
description: このトピックでは、WDI ドライバーでのログ記録 IHV トレースでユーザーが開始したフィードバックを通常モードをについて説明します。
ms.assetid: 723732A3-4B24-4FE5-B338-B8443F287FDE
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d27dd6793cc76611243ba7a6745e3f05d49be3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384993"
---
# <a name="user-initiated-feedback---normal-mode"></a>ユーザーが開始したフィードバック - 標準モード

通常のユーザーが開始したフィードバック (し) のシナリオでは、ユーザーは Wi-fi に問題が発生し、フィードバック レポートを送信します。 このレポートは、Wi-fi の WMI の自動ロガー、ネットワークの統計情報などを含む Wi-fi サブシステムのスナップショットを収集します。IHV 固有のログを収集するには、Microsoft はない初期の ETW プロバイダーを使用した WMI 自動ロガー セッションを提供します。 各 IHV は、Microsoft から提供された WMI 自動ロガーのセッションのレジストリ エントリの ETW プロバイダーのセットを追加します。 レポートが送信されたときに、IHV 自動-ロガー ETL が収集され、分析のため Microsoft に送信されます。 このログ ファイルは循環バッファー サイズを使用して、多少の制限を実装 (\<= 1 MB)。 このログ ファイルに保存されているイベントは、ことを確認するには少なくとも 30 分間のログ イベントが常に保存する過去のフラグ、レベルとキーワードを使用して、適切に調整する必要があります。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供の WMI 自動ロガー セッション

Microsoft では、初期ありません ETW プロバイダーを使用した WMI 自動ロガー セッションを提供します。 IHV のドライバーがインストールされている場合は、Microsoft 提供の WMI 自動ロガーのセッション キーの下で、WMI プロバイダーのレジストリ キーが必要なを追加があります。 IHV は、自動ロガー セッションのレジストリ値のいずれかを変更しないでください。 ただし、すべての ETW プロバイダー オプションは有効にするレベルを含む、IHV、いずれとも一致、すべて、一致するなど。このログ セッションが常に実行され、制限付きの循環バッファーを持つため、Ihv プロバイダー EnableLevels を適切に設定する必要があります。

WMI の自動ロガー セッションは、次のパス HKLM レジストリ ハイブに追加されます。

`HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession`

結果として得られる ETL ログ ファイルはここにあります。

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSession.etl`

## <a name="ihv-driver-inf-changes"></a>IHV ドライバーの INF 変更

Ihv は、しの通常モード中に詳細ログを IHV できるように、次のレジストリ キーの値を追加する、ドライバーの INF ファイルを更新する必要があります。 次のスニペットは、自動ロガー セッションに 1 つの ETW プロバイダーを追加するためのテンプレートを提供します。 IHV は、適切に多くのプロバイダーを追加することができます。 さらに、レベルの値を有効にする ETW プロバイダーごとの IHV 固有に必ずしも付与しないように、マイクロソフトによって定義された値 (TRACE_LEVEL_CRITICAL、TRACE_LEVEL_ERROR など) と同じにします。

### <a name="enable-the-ihv-auto-logger-session"></a>IHV 自動ロガーのセッションを有効にします。

IHV 自動ロガーのセッションがありません ETW プロバイダーを使用した初期化されるため、既定で無効です。 Ihv は"Start"の値を更新してこのセッションを有効にするために必要な**1**ドライバーの INF ファイル、この例で示すようにします。

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession,Start,%REG_DWORD%,1
```

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

この例では、すべてのネイティブ Wi-fi キーワードを持つネイティブ Wi-fi カスタム レベル設定 (すべて有効にする) を示します。

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},,EnableLevel,%REG_DWORD%,0x04
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},MatchAnyKeyword,%REG_QWORD%,0x000FFFFF

Standard EnableLevel values:
0x5 - Verbose
0x4 - Informational
0x3 - Warning
0x2 - Error
0x1 - Critical
0x0 – LogAlways
```

## <a name="related-links"></a>関連リンク

[IHV のトレース ログ記録でフィードバックをユーザーが開始しました。](user-initiated-feedback-with-ihv-trace-logging.md)

[ユーザーが開始したフィードバックの再現コード モード](user-initiated-feedback-repro-mode.md)
