---
title: Windows デバイス コンソール (Devcon.exe)
description: デバイス コンソールである DevCon (Devcon.exe) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示するコマンドライン ツールです。
ms.assetid: ac74200e-e2ae-40db-9fb7-5ea2e7760613
keywords:
- DevCon WDK
- デバイス コンソール WDK
- ドライバー テスト WDK、DevCon
- ドライバーのテスト WDK、DevCon
- デバイス情報 WDK DevCon
- 検索 WDK DevCon
- デバイス情報の表示
- デバイス構成の変更 WDK DevCon
- デバイスの操作 WDK DevCon
- 状態の変更 WDK DevCon
- デバイスの再起動
- デバイス管理 WDK DevCon
- デバイス情報の一覧表示 WDK
ms.date: 04/20/2017
ms.localizationpriority: high
ms.openlocfilehash: d5c3e1418e05d8ffc0a852d626dbefbe1433dc72
ms.sourcegitcommit: 29d9e97439f19d2c5a090006640e4e5659e56412
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335946"
---
# <a name="windows-device-console-devconexe"></a>Windows デバイス コンソール (Devcon.exe)


デバイス コンソールである DevCon (Devcon.exe) は、Windows を実行しているコンピューター上のデバイスに関する詳細情報を表示するコマンドライン ツールです。 DevCon を使用して、デバイスを有効化、無効化、インストール、構成、および削除できます。

DevCon は、Microsoft Windows 2000 以降のバージョンの Windows で実行されます。

## <span id="ddk_devcon_tools"></span><span id="DDK_DEVCON_TOOLS"></span>


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DevCon はどこでダウンロードできますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DevCon (Devcon) は、デスクトップ アプリ用の WDK、Visual Studio、Windows SDK をインストールするときに組み込まれます。 キットのダウンロードの詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェア ダウンロード</a>に関するページを参照してください。</p>
<p><strong>Windows Driver Kit (WDK) 8 および Windows Driver Kit (WDK) 8.1</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p>
<p>%WindowsSdkDir%\tools\arm\devcon.exe</p>
<div class="alert">
<strong>注</strong> Visual Studio 環境変数 %WindowsSdkDir% では、キットがインストールされる Windows キット ディレクトリへのパスが表されます (たとえば、C:\Program Files (x86)\Windows Kits\8.1)。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

このセクションの内容:

[DevCon コマンド](devcon-general-commands.md)

[DevCon の例](devcon-examples.md)

## <a name="span-idwhat_you_can_do_with_devconspanspan-idwhat_you_can_do_with_devconspanspan-idwhat_you_can_do_with_devconspanwhat-you-can-do-with-devcon"></a><span id="What_you_can_do_with_DevCon"></span><span id="what_you_can_do_with_devcon"></span><span id="WHAT_YOU_CAN_DO_WITH_DEVCON"></span>DevCon でできること


Windows ドライバーの開発者およびテスト担当者は、DevCon を使用することで、ドライバーのインストールおよび構成が正しく行われていること (INF ファイル、ドライバー スタック、ドライバー ファイル、ドライバー パッケージが適切であることなど) を確認できます。 また、スクリプト内に DevCon コマンド (enable、disable、install、start、stop、continue) を使用してドライバーをテストすることもできます。

DevCon は、ローカル コンピューターとリモート コンピューターでデバイス管理機能を実行するためのコマンドライン ツールです。

**注**  リモート コンピューターで DevCon コマンドを実行するには、リモート コンピューター上でのプラグアンドプレイ サービスの実行がグループ ポリシー設定によって許可されている必要があります。 Windows Vista および Windows 7 を実行しているコンピューターでは、このサービスへのリモート アクセスがグループ ポリシーによって既定で無効にされています。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモート アクセスを使用できません。

 

DevCon 機能は次のとおりです。

-   **ドライバーとデバイスの情報を表示する** DevCon を使用すれば、ローカル コンピューターと、リモート コンピューター (Windows XP およびそれ以前を実行している) 上のドライバーとデバイスの次のプロパティを表示できます。
    -   ハードウェア ID、互換性 ID、デバイス インスタンス ID。 これらの識別子の詳細については「[デバイスの識別用文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)」を参照してください。
    -   [デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)
    -   デバイス セットアップ クラス内のデバイス
    -   INF ファイルとデバイス ドライバー ファイル
    -   [ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)の詳細
    -   ハードウェア リソース
    -   デバイスの状態
    -   期待されるドライバー スタック
    -   ドライバー ストア内のサードパーティ製ドライバー パッケージ
-   **デバイスを検索する** DevCon を使用すると、ハードウェア ID、デバイス インスタンス ID、またはデバイス セットアップ クラスによって、ローカル コンピューターまたはリモート コンピューター上でインストールされた、およびアンインストールされたデバイスを検索できます。

-   **デバイスの設定を変更する** DevCon を使用すると、ローカル コンピューター上のプラグ アンド プレイ (PnP) デバイスの状態または構成を次の方法で変更できます。
    -   デバイスを有効にする
    -   デバイスを無効にする
    -   ドライバーを更新する (対話型および非対話型)
    -   デバイスをインストールする (devnode を作成してソフトウェアをインストールする)
    -   デバイス ツリーからデバイスを削除し、そのデバイス スタックを削除する
    -   プラグ アンド プレイ デバイスを再スキャンする
    -   ルート列挙デバイスのハードウェア ID を追加、削除、および順序変更する
    -   デバイス セットアップ クラス用の上位および下位のフィルター ドライバーを変更する
    -   ドライバー ストアに対してサードパーティ製ドライバー パッケージの追加および削除を行う
-   **デバイスまたはコンピューターを再起動する** DevCon を使用すると、ローカル デバイスの再起動、オンデマンドでのローカル システムの再起動、または別の DevCon 操作で必要になった場合のローカル システムの再起動を行うことができます。

## <a name="span-iddevcon_source_codespanspan-iddevcon_source_codespanspan-iddevcon_source_codespandevcon-source-code"></a><span id="DevCon_source_code"></span><span id="devcon_source_code"></span><span id="DEVCON_SOURCE_CODE"></span>DevCon ソース コード


また、DevCon で使用する、セットアップおよび構成のデータを取得および変更するための方法を調べることができるように、DevCon ソース コードも提供されています。 DevCon では、[一般的なセットアップ関数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))、[デバイス インストール関数](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))、[PnP 構成マネージャー関数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))の使用法が示されます。 [デバイス コンソール (DevCon) ツール](https://go.microsoft.com/fwlink/p/?LinkId=617966)用のソース コードは、GitHub 上の [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507) リポジトリにあります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[DevCon コマンド](devcon-general-commands.md)

[DevCon の例](devcon-examples.md)

 

 






