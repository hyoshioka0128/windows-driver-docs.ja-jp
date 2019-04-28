---
Description: WpdDeviceInspector Tool の使用
title: WpdDeviceInspector Tool の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aedc1f270b6995fb19b34d74e0b798763f7361b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370454"
---
# <a name="using-the-wpddeviceinspector-tool"></a>WpdDeviceInspector Tool の使用


WpdDeviceInspector ツールとは、包括的な HTML レポートを生成するコンソール アプリケーションです。 このレポートには、デバイスとドライバーについては、次の表に示されている 3 つのカテゴリについて説明します。

| カテゴリ                 | 説明                                                                                              |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| インストール情報 | Windows インストーラーによって使用されるデバイスとドライバーのデータを指定します。                                  |
| デバイスの機能      | コマンド、オブジェクト、コンテンツの種類、形式、およびデバイスでサポートされているイベントを識別します。       |
| デバイスのコンテンツ           | オブジェクト識別子の文字列と対応する永続的な一意オブジェクト識別子 (PUID) 値を一覧表示します。 |

 

## <a name="span-idviewingthecommand-lineoptionsforwpddeviceinspectorspanspan-idviewingthecommand-lineoptionsforwpddeviceinspectorspanspan-idviewingthecommand-lineoptionsforwpddeviceinspectorspanviewing-the-command-line-options-for-wpddeviceinspector"></a><span id="Viewing_the_Command-Line_Options_for_WpdDeviceInspector"></span><span id="viewing_the_command-line_options_for_wpddeviceinspector"></span><span id="VIEWING_THE_COMMAND-LINE_OPTIONS_FOR_WPDDEVICEINSPECTOR"></span>WpdDeviceInspector のコマンド ライン オプションを表示します。


コマンド ライン オプションを表示する*WpdDeviceInspector.exe*、コマンド プロンプトで次のコマンドを入力します。

```cmd
WpdDeviceInspector.exe /?
```

## <a name="span-idgeneratingareportforaspecificdevicespanspan-idgeneratingareportforaspecificdevicespanspan-idgeneratingareportforaspecificdevicespangenerating-a-report-for-a-specific-device"></a><span id="Generating_a_Report_for_a_Specific_Device"></span><span id="generating_a_report_for_a_specific_device"></span><span id="GENERATING_A_REPORT_FOR_A_SPECIFIC_DEVICE"></span>特定のデバイスのレポートを生成します。


実行して、特定のデバイス用のレポートを生成する*WpdDeviceInspector.exe*せず、すべてのパラメーターと、選択したデバイスのインデックスを入力します。

```cpp
> WpdDeviceInspector.exe


1 Windows Portable Device(s) found on the system

[0]     Dev Interface: \\?\root#wpd#0001#{6ac27878-a6fa-4155-ba85-f98f491d4f33}
        Friendly Name: Hello World!
        Manufacturer:  Windows Portable Devices Group
        Description:   Hello World!

Enter the index of the device you want to Inspect.
>
```

または、デバイス id がわかっている場合ことがわかります*WpdDeviceInspector.exe*常に、コマンド プロンプトで/Device スイッチの直後にデバイス id を入力してそのデバイスのレポートを生成します。

```cmd
WpdDeviceInspector.exe /Device:\\?\root#wpd#0000#{6ac27878-a6fa-4155-ba85-f98f491d4f33}
```

デバイス id は、下に表示されます、 *Dev インターフェイス*起動するときに、各デバイスのエントリ*WpdDeviceInspector.exe*パラメーターなし。

## <a name="span-idoperatingwpddeviceinspectorinsnapshotmodespanspan-idoperatingwpddeviceinspectorinsnapshotmodespanspan-idoperatingwpddeviceinspectorinsnapshotmodespanoperating-wpddeviceinspector-in-snapshot-mode"></a><span id="Operating_WpdDeviceInspector_in_Snapshot_Mode"></span><span id="operating_wpddeviceinspector_in_snapshot_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_SNAPSHOT_MODE"></span>スナップショット モードで運用 WpdDeviceInspector


操作できます*WpdDeviceInspector.exe*のモードのスナップショットを取得して、特定のデバイスでオブジェクト階層構造を反映するディレクトリ構造をキャプチャします。 ツールは、スナップショット モードで動作するときに、各フォルダーを特定のオブジェクトのプロパティと属性を格納 .opt ファイルを作成します。

スナップショット モードでは、バイナリのリソースがリソース キー (GUID.pid) という名前のファイルに保存されます。 これらのファイルの名前は変更して必要に応じて開くことができます。 たとえば、JPEG 画像の既定のリソース {0} E81E79BE-34F0-41BF-B53F-F1A06AE87842} に保存されます.0、デバイスに簡単に名前を変更できますが、\_image.jpg できるように、グラフィック ツールでイメージを表示できませんでした。

スナップショット モードで動作するには、コマンド プロンプトで/Snapshot スイッチを使用します。

```cmd
WpdDeviceInspector.exe /Snapshot
```

## <a name="span-idoperatingwpddeviceinspectorinwpdautomationmodespanspan-idoperatingwpddeviceinspectorinwpdautomationmodespanspan-idoperatingwpddeviceinspectorinwpdautomationmodespanoperating-wpddeviceinspector-in-wpd-automation-mode"></a><span id="Operating_WpdDeviceInspector_in_WPD_Automation_Mode"></span><span id="operating_wpddeviceinspector_in_wpd_automation_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_WPD_AUTOMATION_MODE"></span>WPD オートメーション モードで運用 WpdDeviceInspector


操作できます*WpdDeviceInspector.exe* JScript プロパティと、特定のデバイスのメソッドをダンプします。 これは、機能は、Device Stage™ HostedSiteWithDevice タスクから WPD デバイスにアクセスする WPD オートメーションを使用しているときに便利です。 WPD デバイス Device Stage™ タスクを作成する方法の詳細については、Windows デバイス エクスペリエンスのポータルを参照してください。 この機能は、Windows 7 で使用できるだけです。

WPD オートメーション モードで動作するには、コマンド プロンプトで/Automation スイッチを使用します。

```cpp
WpdDeviceInspector.exe /Automation
```

 

 




