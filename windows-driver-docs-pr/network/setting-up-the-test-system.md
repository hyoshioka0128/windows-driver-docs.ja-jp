---
title: テスト システムのセットアップ
description: テスト システムのセットアップ
ms.assetid: 99c591e0-fe01-4db9-af95-4ce458625bfb
keywords:
- ネットワークコンポーネントのアップグレードのテスト (WDK)
- アップグレードテスト WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d3a9cfe5b1ebf73d821da1197b53b286bca5db
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750043"
---
# <a name="setting-up-the-test-system"></a>テスト システムのセットアップ





**注:**   ベンダーが提供するネットワークアップグレードは、microsoft windows XP (SP1 以降)、microsoft windows Server 2003、およびそれ以降のオペレーティングシステムではサポートされていません。

 

ネットワークコンポーネントをアップグレードする前に、アップグレードするネットワークコンポーネントが正しくインストールおよび構成されていることを確認してください。

**テストシステムを設定するには**

1.  Preupgrade オペレーティングシステム用に1つのパーティションを作成し、Microsoft Windows 2000 以降のオペレーティングシステム用に別のパーティションを作成します。
    **注 preupgrade オペレーティング**システムとアップグレードオペレーティングシステムを同じパーティションにインストールしないでください。   Preupgrade オペレーティングシステムと Windows 2000 以降が同じパーティションにインストールされている場合は、同じプログラムファイルのディレクトリが共有されます。

     

2.  テストシステムで、アップグレードするオペレーティングシステム以外のビルドを起動します。 次に、アップグレードするパーティション全体をコピーします。ただし、pagefile.sys ファイルはバックアップディレクトリにコピーします。 Pagefile.sys ファイルは、Windows 2000 以降の起動時に作成されるため、コピーする必要はありません。

    このバックアップを作成するこの方法は、ディスクイメージプログラムを作成する場合にお勧めします。これは、ディスクイメージプログラムよりもファイルをコピーするのに要する時間が短い**xcopy**を使用できるためです。 アップグレードテストは、バックアップパーティションの内容をアップグレードする新しいパーティションに単にコピーするだけで繰り返すことができます。preupgrade オペレーティングシステムを再インストールする必要はありません。

3.  ネットワーク移行 DLL と netmap .inf ファイルを格納するためのテストディレクトリを作成し、これらのファイルをテストディレクトリにコピーします。

4.  Winnt32 のアップグレードフェーズに必要な Windows 2000 以降のファイルを格納するために、別のディレクトリを作成します。

5.  Windows 2000 以降のチェックされたビルドを含む Windows 2000 またはそれ以降の Driver Development Kit (DDK) cd-rom を挿入します。 Cd-rom の\\i386 ディレクトリから、次のファイルをバックアップディレクトリにコピーします (手順 2)。
    -   winnt32.exe
    -   winnt32u
    -   pidgen.dll 読み込め
    -   wetuplog.\*

6.  Winntupg という名前のアップグレードディレクトリを作成します。 Cd-rom の\\i386\\winntupg ディレクトリにあるファイルを、テストシステムの winntupg ディレクトリにコピーします。

7.  テキストシステムでデバッガーを有効にするか、Windows 2000 以降のオペレーティングシステムのリソースキットに含まれている debugmon を起動します。 次に、netcfg ファイルを% windir% にコピーします。 Netcfg ファイルを使用すると、デバッグトレースが有効になります。

    Netcfg ファイルの例を次に示します。

    ```INI
    [DebugFlags]
    BreakOnAddLegacy=0
    BreakOnAlloc=0
    BreakonDoUnattend=0
    BreakonDwrefProblem=0
    BreakOnError=0
    BreakOnHr=0
    BreakOnHrInteraction=0
    BreakOnIteration=0
    BreakOnNetInstall=0
    BreakOnWizard=0
    DisableTray=0
    DumpLeaks=0
    DumpNetCfgTree=0
    NetShellBreakOnInit=0
    ShowIngnoreErrors=0
    ShowProcessAndThreadIds=0
    SkipLanEnum=0
    TracingTimeStamps=0

    [Default]
    OutputToDebug=1

    [EsLocks]
    OutputToDebug=0

    [ShellViewMsgs]
    OutputToDebug=0

    [OptErrors]
    OutputToDebug=0
    ```

 

 





