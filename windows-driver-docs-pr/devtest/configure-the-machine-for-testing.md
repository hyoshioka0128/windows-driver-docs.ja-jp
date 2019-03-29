---
title: テスト マシンを構成します。
description: WDTF と TAEF、インストールに必要な手順のアウトラインは、システムの基礎データ ドリブン テストをコピーし、テスト マシンを構成します。
keywords:
- Sysfund テスト
- データ ドリブン テスト
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: af161ef2b4f2cc7c70cc0142abd255b62ce9844f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570883"
---
# <a name="configure-the-machine-for-testing"></a>テスト マシンを構成します。
このトピックでは、インストールに必要な手順を説明[WDTF](https://docs.microsoft.com/windows-hardware/drivers/wdtf/)と[TAEF](https://docs.microsoft.com/windows-hardware/drivers/taef/)、データ ドリブン テストをコピーして、テスト マシンを構成します。 WDTF インストールでは、システムのドライバーがインストールされるため、管理者特権または管理者のコマンド プロンプトから次のコマンドを実行する必要があることに注意してください。
以下の手順では、システムのアーキテクチャは x64 を前提としています。  次の手順は、他のアーキテクチャを調整する必要があります。

**手順 1**:最新のパッケージとファイルを入手[EWDK](https://docs.microsoft.com/windows-hardware/drivers/develop/installing-the-enterprise-wdk)ライセンス条項に同意し、テストを実行するマシンに EWDK ISO ファイルを保存します。 EWDK では、Visual Studio のインストールは必要ありません。 EWDK ISO をダウンロードして、ISO をマウントし、以下で指定したファイルをコピーするだけです。 ISO をマウントするには、クリックし、ISO ファイルを右クリックし**マウント**します。 マウントすると、マウントされた ISO に、ISO ドライブ文字が割り当てられます。

**手順 2**:マウントされた ISO で TAEF msi ファイルの場所に移動し、目的のアーキテクチャのパッケージをインストールするには、TAEF をインストールします。 場所と、インストール ログ ファイルの名前を指定 **%USERPROFILE%\Desktop\TAEFInstall.log**この例では。

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes

msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\TAEFInstall.log"
```

TAEF MSI のインストールに TAEF`%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64`します。  このディレクトリ、システムの PATH 環境変数を追加し、管理者特権でコマンド プロンプトを再起動します。

TAEF サービス (Te.service) を起動し、設定が実行されていない場合**Autostart**次の手順。

1.  サービスの起動: services.msc
2.  Te.Service をダブルクリックします。
3.  「スタートアップ」の種類を「自動」に設定します。
4.  サービスを開始する開始 をクリックします。

Services.msc でのサービスとして Te.Service が表示されない場合は、 **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\TAEF\x64**し、サービスの開始を取得するには、次のコマンドを実行します。

1. `wex.services.exe /install:te.service` 

   Te.service が正常にインストールされていることを確認します。

2. `sc start te.service` 

   '状態' が 'START_PENDING' であることを確認します。

3. `sc query te.service` 

   Verify 'STATE' is 'RUNNING'

4. `sc qc te.service` 

   Verify 'START_TYPE' is 'AUTO_START'

**手順 3**:WDTF MSI (上記のマウントされた iso TAEF MSI と同じ場所) の場所に移動し、目的のアーキテクチャのパッケージをインストールするには、WDTF をインストールします。 場所と、インストール ログ ファイルの名前を指定 **%USERPROFILE%\Desktop\WDTFInstall.log**この例では。

```console
cd <ISO drive>\Program Files\Windows Kits\10\Testing\Runtimes
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* "%USERPROFILE%\Desktop\WDTFInstall.log"
```
WDTF MSI のインストールに WDTF **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF**します。

**手順 4**:テスト マシンを構成します。

1.  完全なダンプを収集、カーネル デバッガーをアタッチするようにマシンを構成します。
2.  テストは、コンピューターの再起動可能性があるとスリープのサイクルを制御する必要があります、ため、スリープ状態を表示、およびテスト アカウント (netplwiz.exe) への自動ログオンをオフにしないでください、マシンを構成します。  その自動ログオンを注意して使用する必要がありますに注意してください。

**手順 5**:すべてのファイルをコピーすることによって、データ ドリブン テスト バイナリを入手 **\<ISO ドライブ > \Program Files\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven**などのローカル フォルダーに **%USERPROFILE%\Desktop\Tests**します。 ISO をマウント解除します。

