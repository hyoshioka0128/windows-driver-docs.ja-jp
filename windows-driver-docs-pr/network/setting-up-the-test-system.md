---
title: テスト システムをセットアップします。
description: テスト システムをセットアップします。
ms.assetid: 99c591e0-fe01-4db9-af95-4ce458625bfb
keywords:
- テスト ネットワーク コンポーネントをアップグレード WDK
- アップグレードのテストの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d3a9cfe5b1ebf73d821da1197b53b286bca5db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532815"
---
# <a name="setting-up-the-test-system"></a>テスト システムをセットアップします。





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

ネットワーク コンポーネントをアップグレードする前にアップグレードするネットワーク コンポーネントが正しくインストールされ構成されているいることを確認します。

**テスト システムを設定するには**

1.  アップグレード前のオペレーティング システムの 1 つのパーティションと、Microsoft Windows 2000 またはそれ以降のオペレーティング システムの別のパーティションを作成します。
    **注**  同じパーティションに、アップグレード前のオペレーティング システムとアップグレードのオペレーティング システムをインストールしません。 場合は、同じパーティションには、アップグレード前のオペレーティング システムおよび Windows 2000 またはそれ以降がインストールされている、同じプログラム ファイル ディレクトリが共有します。

     

2.  テスト システムにアップグレードする 1 つ以外のオペレーティング システムのビルドを起動します。 パーティション全体をアップグレード、pagefile.sys ファイルを除き、バックアップ ディレクトリにコピーします。 Windows 2000 以降の起動時に作成されるので、ページファイルをコピーする必要はありません。

    バックアップのインストールを作成するには、このメソッドは、使用できるため、ディスク イメージのプログラムを作成することをお勧め**xcopy**、ディスク イメージ プログラムよりもファイルをコピーするには、少ない時間がかかります。 アップグレードする新しいパーティションにバックアップ パーティションの内容をコピーするだけで、アップグレードのテストを繰り返すことができます場合によっては、アップグレード前のオペレーティング システムを再インストールする必要はありません。

3.  ネットワーク移行 DLL と netmap.inf ファイルのファイルを格納するためのテスト ディレクトリを作成し、テスト ディレクトリにこれらのファイルをコピーします。

4.  Windows 2000 または Winnt32 アップグレード フェーズに必要な以降のファイルを格納するための別のディレクトリを作成します。

5.  Windows 2000 またはそれ以降ドライバー開発キット (DDK) を Windows 2000 以降のチェックのビルドを含む CD-ROM を挿入します。 \\Cd-rom、i386 ディレクトリでは、次のファイルをコピー バックアップ ディレクトリ (手順 2)。
    -   winnt32.exe
    -   winnt32u.dll
    -   pidgen.dll
    -   wetuplog します。\*

6.  Winntupg という名前のアップグレードのディレクトリを作成します。 内のファイルをコピー、 \\i386\\winntupg ディレクトリ、テスト システムに CD-ROM 上 winntupg ディレクトリ。

7.  テキストのシステム上のデバッガーを有効にするか、リソース キットの Windows 2000 またはそれ以降のオペレーティング システムに含まれている、debugmon.exe を開始します。 Netcfg.ini ファイルを %windir% にコピーします。 Netcfg.ini ファイルは、デバッグ トレースを有効します。

    Netcfg.ini ファイルのサンプルを次に示します。

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

 

 





