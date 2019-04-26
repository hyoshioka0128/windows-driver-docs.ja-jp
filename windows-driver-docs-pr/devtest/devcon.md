---
title: Windows デバイス コンソール (Devcon.exe)
description: DevCon (Devcon.exe)、デバイス コンソールは、Windows を実行するコンピューターでデバイスの詳細情報を表示するコマンド ライン ツールです。
ms.assetid: ac74200e-e2ae-40db-9fb7-5ea2e7760613
keywords:
- DevCon WDK
- デバイス コンソール WDK
- driver DevCon、WDK のテスト
- ドライバー WDK、DevCon のテスト
- デバイス情報 WDK DevCon
- WDK DevCon を検索します。
- デバイス情報を表示します。
- WDK DevCon デバイスの構成を変更します。
- WDK DevCon のデバイスを操作します。
- WDK DevCon を状態します。
- デバイスを再起動します。
- デバイス管理 WDK DevCon
- WDK のデバイス情報を一覧表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909ac5e2f1ae49d83f7c2a0ef59fa44d5a9dae1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341706"
---
# <a name="windows-device-console-devconexe"></a>Windows デバイス コンソール (Devcon.exe)


DevCon (Devcon.exe)、デバイス コンソールは、Windows を実行するコンピューターでデバイスの詳細情報を表示するコマンド ライン ツールです。 DevCon を使用して、有効にする、無効にする、インストール、構成、およびデバイスを削除することができます。

DevCon は、Microsoft Windows 2000 以降のバージョンの Windows で動作します。

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
<td align="left"><p>WDK、Visual Studio、およびデスクトップ アプリ用の Windows SDK をインストールするときに、DevCon (Devcon.exe) が含まれます。 キットのダウンロード方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Hardware Downloads](https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows ハードウェア ダウンロード</a>します。</p>
<p><strong>Windows Driver Kit (WDK) 8 と Windows Driver Kit (WDK) 8.1</strong> (インストール パス)</p>
<p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p>
<p>%WindowsSdkDir%\tools\arm\devcon.exe</p>
<div class="alert">
<strong>注</strong>WindowsSdkDir %、Visual Studio 環境変数では、パスを表す Windows キット ディレクトリに、キットがインストールされている、たとえば、C:\Program Files (x86) \windows kits \8.1 です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

このセクションの内容:

[DevCon コマンド](devcon-general-commands.md)

[DevCon 例](devcon-examples.md)

## <a name="span-idwhatyoucandowithdevconspanspan-idwhatyoucandowithdevconspanspan-idwhatyoucandowithdevconspanwhat-you-can-do-with-devcon"></a><span id="What_you_can_do_with_DevCon"></span><span id="what_you_can_do_with_devcon"></span><span id="WHAT_YOU_CAN_DO_WITH_DEVCON"></span>DevCon で行うことができます。


Windows ドライバー開発者およびテスト担当者は、DevCon を使用して、ドライバーがインストールされ、正しい INF ファイル、ドライバー スタック、ドライバー ファイル、およびドライバー パッケージを含むが正しく構成されていることを確認します。 DevCon コマンドを使用することもできます (有効にする、無効にする、インストール、開始、停止、および継続) ドライバーをテストするためのスクリプトでします。

DevCon は、ローカル コンピューターおよびリモート コンピューターをデバイス管理機能を実行するコマンド ライン ツールです。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。

 

Devcon 機能は次のとおりです。

-   **ドライバーとデバイスの情報を表示する**DevCon は、ローカル コンピューターおよびリモート コンピューターにドライバーとデバイスの次のプロパティを表示することができます (Windows XP を実行している以前のバージョン)。
    -   ハードウェア Id、互換性 Id、およびデバイス インスタンス Id。 これらの識別子がで詳しく説明されている[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)します。
    -   [デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)
    -   デバイスのデバイス セットアップ クラス
    -   INF ファイルとデバイスのドライバー ファイル
    -   詳細[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff539954)
    -   ハードウェア リソース
    -   デバイスの状態
    -   必要なドライバー スタック
    -   ドライバー ストアにサード パーティ製のドライバー パッケージ
-   **デバイスの検索**DevCon ハードウェア ID、デバイス インスタンス ID、またはデバイス セットアップ クラスが、ローカルまたはリモート コンピューターにインストールされ、インストールされていないデバイスを検索できます。

-   **デバイスの設定を変更する**DevCon は次の方法で、状態またはローカル コンピューターのプラグ アンド プレイ (PnP) デバイスの構成を変更できます。
    -   デバイスを有効にします。
    -   デバイスを無効にします。
    -   (対話型と非対話型) ドライバーを更新します。
    -   デバイスをインストールする (devnode を作成およびソフトウェアのインストール)
    -   デバイス ツリーからデバイスを削除し、そのデバイス スタックを削除
    -   プラグ アンド プレイ デバイスを再スキャンします。
    -   追加、削除、およびルートで列挙されるデバイスのハードウェア Id の順序を変更
    -   デバイス セットアップ クラスの上限と下限のフィルター ドライバーを変更します。
    -   追加して、サード パーティ製のドライバー パッケージをドライバー ストアから削除
-   **デバイスまたはコンピューターの再起動**DevCon は、ローカルのデバイスを再起動して、必要に応じて、ローカル システムを再起動、または別 DevCon 操作に必要な場合は、ローカル システムを再起動します。

## <a name="span-iddevconsourcecodespanspan-iddevconsourcecodespanspan-iddevconsourcecodespandevcon-source-code"></a><span id="DevCon_source_code"></span><span id="devcon_source_code"></span><span id="DEVCON_SOURCE_CODE"></span>DevCon ソース コード


DevCon のソース コードを使用できるは、DevCon を使用して取得し、セットアップと構成データを変更する方法を確認するようにもです。 DevCon の使用方法を示します[関数の一般的なセットアップ](https://msdn.microsoft.com/library/windows/hardware/ff544985)、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)、および[PnP の Configuration Manager 機能](https://msdn.microsoft.com/library/windows/hardware/ff549713)します。 ソース コード、[デバイス コンソール (DevCon) ツール](https://go.microsoft.com/fwlink/p/?LinkId=617966)で使用できるは、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[DevCon コマンド](devcon-general-commands.md)

[DevCon 例](devcon-examples.md)

 

 






