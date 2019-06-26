---
title: ネットワーク アップグレード プロセスの Winnt32 フェーズ
description: ネットワーク アップグレード プロセスの Winnt32 フェーズ
ms.assetid: a83edcfb-e075-4763-8a6a-33879ccf2357
keywords:
- ネットワーク コンポーネントをアップグレード WDK、フェーズ
- WDK のネットワーク コンポーネントのアップグレード フェーズします。
- Winnt32 フェーズ WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 583135f196a4e8adb3179a3e7660e423f5ae0322
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384699"
---
# <a name="winnt32-phase-of-the-network-upgrade-process"></a>ネットワーク アップグレード プロセスの Winnt32 フェーズ





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

ユーザーまたはシステム管理者は、次の操作のいずれかを実行して、アップグレード プロセスを開始します。

-   Windows 2000 またはそれ以降の CD-ROM のスピンアップ後に表示されるユーザー インターフェイス コンポーネントのアップグレードを選択します。

-   選択し、実行\\i386\\CD-ROM 上の winnt32.exe

かどうか、ユーザーまたはシステム管理者が、NETUPGRD 設定\_INIT\_ファイル\_アップグレード対象のシステムで DIR 環境変数、NetSetup 検索、 [netupg.inf](creating-a-netupg-inf-file.md)ディレクトリ内のファイルその変数で指定します。 Netupg.inf ファイルには、1 つだけのセクションが含まれています。**OemNetUpgradeDirs**します。 このセクションでは、各エントリは、ベンダーから提供されたアップグレードなど、ファイルを含むディレクトリへの完全パスを指定します、 [netmap.inf ファイル](creating-a-netmap-inf-file.md)ネットワーク コンポーネントのファイル。 場合、NETUPGRD\_INIT\_ファイル\_DIR 環境変数が設定されていない、NetSetup (, 944 netupgrd.dll) が自分のディレクトリに netmap.inf ファイルのファイルを検索します。

NetSetup では、組み込みのアップグレードのサポートがないネットワーク コンポーネントを識別するために netmap.inf ファイルのファイルを読み取ります。 NetSetup が無人モードで実行している場合、ウィザードが表示されます。ただし、ユーザーまたはシステム管理者は、ウィザードを使用できません。 NetSetup が無人モードで実行されていない場合は、組み込みのアップグレードのサポートがないネットワーク コンポーネントの一覧が表示されます。

ウィザードでは、ユーザーまたはシステム管理者を使用します。

-   クリックして**キャンセル**オペレーティング システムのインストールを中止します。

-   クリックして**次**表示されているネットワーク コンポーネントをアップグレードすることがなく、オペレーティング システムをインストールします。

-   アップグレードのファイルを一覧表示されているネットワーク コンポーネントのベンダーから提供されたのドライブとディレクトリの場所を指定します。

    NetSetup は、指定した位置に netmap.inf ファイル ファイルを読み取って、その場所にベンダーから提供されたアップグレード ファイルをシステムのハード ディスク上の一時ディレクトリにコピーします。 この一時ディレクトリでは、DLL のベンダーから提供されたネットワークの移行の作業ディレクトリになります。 NetSetup には、ウィザードで、コンポーネントの一覧から netmap.inf ファイルのファイルがある任意のコンポーネントも削除されます。

NetSetup、$Win で winnt.sif ファイル (応答ファイルとも呼ばれます) を生成する\_nt$。 ~ bt ディレクトリは、通常は c: ドライブ上にあります。

NetSetup には、次のように、応答ファイルが生成されます。

1.  NetSetup では、各ネットワーク コンポーネントを列挙する preupgraded システムのレジストリを読み取ります。 組み込みアップグレードがサポートする各ネットワーク コンポーネントは、NetSetup には、応答ファイルをレジストリから読み取られた情報が書き込まれます。

2.  組み込みのアップグレードのサポートがない各ネットワーク コンポーネント NetSetup はコンポーネントの netmap.inf ファイルのファイルを読み取ります。 Netmap.inf ファイルのファイルは、アップグレードされたオペレーティング システムに対応する ID に、アップグレード前のデバイス、ハードウェア、またはネットワーク コンポーネントの互換性のある ID をマップします。 NetSetup がアップグレード前の id レジストリから読み取ることがネットワーク コンポーネントのアップグレード前の ID と一致するかどうか、 **OemNetAdapters**、 **OemNetProtocols**、 **OemNetServices**、または**OemAsyncAdapters** NetSetup、netmap.inf ファイルのファイルのセクションは、応答ファイルをコンポーネントのベンダーが提供情報を書き込みます。

3.  コンポーネントのデバイスのオペレーティング システム、ハードウェア、または互換性 ID を使用して、NetSetup を読み取り、 **OemUpgradeSupport**ネットワーク移行を DLL の読み込みを決定する netmap.inf ファイルのファイルのセクション。 NetSetup を読み込みネットワーク移行 DLL、DLL の呼び出す[ **PreUpgradeInitialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562439(v=vs.85))関数。 **PreUpgradeInitialize**関数が DLL に自体を初期化するために使用する情報を提供します。

4.  NetSetup 呼び出し、DLL の[ **DoPreUpgradeProcessing** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545634(v=vs.85)) DLL のネットワークの移行でサポートされている各ネットワーク コンポーネントに対して 1 回の関数。 **DoPreUpgradeProcessing**レジストリおよび呼び出しから、ネットワーク コンポーネントのアップグレード前のパラメーターの値を読み取り、 [ **NetUpgradeAddSection** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559063(v=vs.85))と[ **NetUpgradeAddLineToSection** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559059(v=vs.85))関数には他のコンポーネントに固有の情報と共に、これらのパラメーターを応答ファイルに書き込めません。 **DoPreUpgradeProcessing**応答ファイルに適切なエントリを加えることによって、preupgraded コンポーネントに関連付けられているバイナリ データを移行することができます。

5.  応答ファイルが完全に生成されると、NetSetup は適切なディレクトリにベンダーから提供されたアップグレード ファイルをコピーし、アップグレード プロセスのテキスト モードのフェーズにブートされます。

 

 





