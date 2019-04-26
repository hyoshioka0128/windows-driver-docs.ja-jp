---
title: ワークグループ コンピューター上のリモート デバッグ
description: ワークグループに参加しているコンピューターでのリモート デバッグを行うことができます。
ms.assetid: 0E740E1A-8DEA-4086-AE9D-6B135BF278B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 058180e21b9d294f80329ad97b9b12bf7ca83376
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353586"
---
# <a name="remote-debugging-on-workgroup-computers"></a>ワークグループ コンピューター上のリモート デバッグ


ワークグループに参加しているコンピューターでのリモート デバッグを行うことができます。 最初にデバッグ サーバーを実行するコンピューターを構成します。 デバッグ サーバーをアクティブ化します。 デバッグ サーバーがアクティブにした後、デバッグのクライアントからサーバーに接続できます。

## <a name="span-idconfiguringthedebuggingservercomputerspanspan-idconfiguringthedebuggingservercomputerspanspan-idconfiguringthedebuggingservercomputerspanconfiguring-the-debugging-server-computer"></a><span id="Configuring_the_debugging_server_computer"></span><span id="configuring_the_debugging_server_computer"></span><span id="CONFIGURING_THE_DEBUGGING_SERVER_COMPUTER"></span>デバッグ サーバー コンピューターの構成


-   ローカル管理者アカウントを作成し、そのアカウントを使用してログオンします。
-   ファイルとプリンターのアクティブなネットワークの共有を有効にします。 たとえば、アクティブなネットワークが有効にするファイルとプリンターのプライベート ネットワークの共有、プライベートである場合です。

    コントロール パネルを使用して、ファイルとプリンターの共有を有効にすることができます。 たとえば、Windows 8 で手順をここでは。

    1.  コントロール パネルを開きます。
    2.  クリックして**ネットワークとインターネット**し**ネットワークと共有センター**します。 **、アクティブなネットワークを表示**、アクティブになっている (たとえば、プライベート) ネットワークの種類に注意してください。
    3.  クリックして**詳細共有設定の変更**します。 アクティブなネットワークの種類では、選択**ネットワーク探索を有効に**と**ファイルとプリンターの共有を有効に**します。
-   次の手順に従って、リモート レジストリ サービスを開始します。

    1.  コマンド プロンプト ウィンドウで、または [実行] ボックスで、入力**services.msc**します。
    2.  右クリックして**リモート レジストリ**、選択**開始**します。
-   次の手順に従って、forceguest を無効にします。

    1.  コマンド プロンプト ウィンドウで、または [実行] ボックスで、入力**regedit**します。
    2.  レジストリ エディターでは、この値を 0 に設定します。

        **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\Lsa ForceGuest**

## <a name="span-idactivatingthedebuggingserverspanspan-idactivatingthedebuggingserverspanspan-idactivatingthedebuggingserverspanactivating-the-debugging-server"></a><span id="Activating_the_debugging_server"></span><span id="activating_the_debugging_server"></span><span id="ACTIVATING_THE_DEBUGGING_SERVER"></span>デバッグ サーバーのライセンス認証


デバッグ サーバーまたはプロセス サーバーまたは KD 接続のサーバーを使用して、デバッガーを有効にすることができます。 詳しくは、次のトピックをご覧ください。

-   [**デバッグ サーバー アクティブ化します。**](activating-a-debugging-server.md)
-   [**プロセス サーバーをアクティブ化します。**](activating-a-process-server.md)
-   [**KD 接続のサーバーをアクティブ化します。**](activating-a-kd-connection-server.md)

## <a name="span-idactivatingthedebuggingclientspanspan-idactivatingthedebuggingclientspanspan-idactivatingthedebuggingclientspanactivating-the-debugging-client"></a><span id="Activating_the_debugging_client"></span><span id="activating_the_debugging_client"></span><span id="ACTIVATING_THE_DEBUGGING_CLIENT"></span>デバッグ クライアントをアクティブ化します。


デバッグ クライアントをアクティブ化するいくつかの方法はあります。 詳しくは、次のトピックをご覧ください。

-   [**デバッグ クライアントをアクティブ化します。**](activating-a-debugging-client.md)
-   [**スマート クライアントのアクティブ化**](activating-a-smart-client.md)
-   [**スマート クライアント (カーネル モード) をアクティブ化します。**](activating-a-smart-client--kernel-mode-.md)
-   [**プロセス サーバーの検索**](searching-for-process-servers.md)
-   [**KD 接続のサーバーの検索**](searching-for-kd-connection-servers.md)

**注**  デバッグのクライアントをデバッグ サーバーに接続する名前付きパイプを使用する場合、ユーザー名と、デバッグ サーバーを実行しているコンピューターにアクセスできるアカウントのパスワードを提供する必要があります。 使用して、両方ではなく、次のオプションの。

- ユーザー名とデバッグ サーバー コンピューター アカウントのパスワードを共有するアカウントを使用してデバッグ クライアント コンピューターにログオンします。
- デバッグのクライアント コンピューターでコマンド プロンプト ウィンドウで、次のコマンドを入力します。

  **net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>ユーザー名</em>

  場所*サーバー* 、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

  メッセージが表示されたらのパスワードを入力します。 *UserName*します。

 

 

 





