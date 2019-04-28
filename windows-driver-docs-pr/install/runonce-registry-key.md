---
title: RunOnce Registry キー
description: RunOnce Registry キー
ms.assetid: dbeb7be7-4d38-49e2-944c-ea95d9914ebe
keywords:
- RunOnce のレジストリ キー
- レジストリの WDK デバイスのインストール
- デバイスのインストール WDK、レジストリ
- インストールを実行するデバイス WDK、レジストリ
- デバイスのセットアップの WDK デバイスのインストール、レジストリ
- ドライバー レジストリ RunOnce キー WDK デバイス インストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf05620ed9ad77c9f0113c6cb0e31bf525af3544
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382919"
---
# <a name="runonce-registry-key"></a>RunOnce Registry キー





すべてのバージョンの Windows レジストリ キーをサポートする**RunOnce**、これは、コマンドは、システムが 1 つを実行することにし、削除の指定に使用することができます。

Windows 8 および Windows 8.1、 **RunOnce** SWENUM デバイスのソフトウェアのみのインストールのエントリは、デバイスのインストール中に処理されます。 その他の**RunOnce**エントリに追加されます、 **RunOnce**キー。 次回のシステムの処理に適用されます、 **RunOnce**キー。 デバイスのインストールを処理するシステムを強制しません**RunOnce**エントリ。

Windows 7 と以前のバージョンでデバイスがインストールされている後すぐに Windows のコマンドを実行の下に格納、 **RunOnce**キーし、キーを削除します。 さらに、毎回、システムの起動時の下に格納するコマンドが実行されます、 **RunOnce**キーし、キーを削除します。 そのため、下のコマンドを配置した場合、 **RunOnce**キー、簡単には予測できませんを実行するとします。

Windows が下に格納コマンドを実行するデバイスがインストールされたら、すぐに、 **RunOnce**キーし、キーを削除します。 さらに、毎回、システムの起動時の下に格納するコマンドが実行されます、 **RunOnce**キーし、キーを削除します。 そのため、下のコマンドを配置した場合、 **RunOnce**キー、簡単には予測できませんを実行するとします。

デバイス インストールの場合、 **RunOnce**を使用してレジストリ キーを作成できる*追加レジストリ セクション*を使用して指定する[ **INF AddReg ディレクティブ**](inf-addreg-directive.md). 各*追加レジストリ セクション*に次の構文があります。

`reg-root, [subkey], [value-entry-name], [flags], [value]`

レジストリ ルート (*reg ルート*) の値のサブキーと、 **RunOnce**レジストリ キーは、次のとおり。

**HKLM、"ソフトウェア\\Microsoft\\Windows\\CurrentVersion\\RunOnce"**

*値のエントリ名*から文字列を省略すると、 **RunOnce**レジストリ エントリ。 示されていると、エントリの種類、*フラグ*値には、いずれかである必要があります[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) (*フラグ*0x00000000 の値) または[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)(*フラグ*0x00010000 の値)。 型のエントリの[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) (既定)、*フラグ*値を省略できます。

*値*でパラメーターを**RunOnce**キーを実行するコマンドを指定します。 このパラメーターは、引用符で囲まれた文字列形式は、次のとおりです。

```cpp
Rundll32[.exe] DllName,EntryPoint[Arguments]
```

既定で、 **RunOnce**キーを削除すると、後で、指定したコマンドを実行します。 プレフィックスにすることができます、 **RunOnce**キー*値*感嘆符 (!)、コマンドが正常に実行されるまで、キーの削除を延期するパラメーター。 指定されたコマンドが失敗した場合、感嘆符プレフィックスなし、 **RunOnce**キーが削除されますが、コマンドを実行できませんが、次回のシステムが起動します。

また、既定で、 **RunOnce**システムがセーフ モードで開始されると、キーは無視されます。 *値*パラメーターの**RunOnce**アスタリスク付きキーを付けることができます (\*) もセーフ モードで実行するコマンドを強制的にします。

作成するときに、次のガイドラインを考慮して、*値*エントリの文字列します。

-   *Rundll32*付けても付けなくても表示されることができます、 *.exe*ファイル名拡張子。

-   *DllName* DLL または実行可能イメージの完全パスを指定します。 必須の終端コンマを除く式にはする必要がありますそれ以外の場合が含まれていないコンマにはです。 既定の拡張機能は、ファイル名拡張子が指定されていない場合 *.dll*します。

-   *EntryPoint*によって示される DLL 内のエントリ ポイントの名前を指定*DllName*します。

-   *引数*は、省略可能な部分文字列を含むすべての引数を指定した DLL に渡される必要があります。

-   1 つだけのスペースで区切る必要があります、 *EntryPoint*から文字列、*引数*部分文字列。

次のコード例は、*追加レジストリ セクション*コマンドと 引数を格納するエントリ、 **RunOnce**キー。

```cpp
;; WDMAud swenum install

HKLM,%RunOnce%,"WDM_WDMAUD",,\
"rundll32.exe streamci.dll,StreamingDeviceSetup %WDM_WDMAUD.DeviceId%,%KSNAME_Filter%,%KSCATEGORY_WDMAUD%,%17%\WDMAUDIO.inf,WDM_WDMAUD.Interface.Install"

[Strings]
RunOnce = "SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce"
WDM_WDMAUD.DeviceId = "{CD171DE3-69E5-11D2-B56D-0000F8754380}"
KSNAME_Filter = "{9B365890-165F-11D0-A195-0020AFD156E4}"
KSCATEGORY_WDMAUD = "{3E227E76-690D-11D2-8161-0000F8775BF1}"
```

使用する場合に、次の規則が適用**RunOnce**デバイスのインストール用のレジストリ キーします。

-   SWENUM、ソフトウェアのデバイスの列挙子によって列挙されているソフトウェア専用デバイスのインストールについてのみ、これらのレジストリ キーを使用する必要があります。

-   **RunOnce**キーへの呼び出しののみで構成*Rundll32.exe*します。 それ以外の場合、WHQL はデジタル署名、[ドライバー パッケージ](driver-packages.md)します。

-   コードを実行するユーザーの入力を表示する必要があります。

-   サーバー側のインストールは、システム コンテキストで実行します。 このため、する必要がありますに実行されるコードに記述されているセキュリティの脆弱性が含まれていないと、ファイルのアクセス許可が変更される悪意からコードを禁止します。

-   Windows Vista 以降では、システムは実行されませんで指定されたコマンド、 **RunOnce**キーの場合、管理者特権のないユーザーがシステムにログオンします。 不完全な可能性または破損したインストールが次のシステムを再起動します。

    前に、*デバイス インストール アプリケーション*を作成、 **RunOnce**エントリ、システムの再起動後に管理者特権を持つユーザーがログオンする必要がありますが、現在のユーザーに通知します。

    詳細については、次を参照してください。[ログオン時に Windows Vista で実行されるアプリケーションの開発](https://go.microsoft.com/fwlink/p/?linkid=133224)します。

 

 





