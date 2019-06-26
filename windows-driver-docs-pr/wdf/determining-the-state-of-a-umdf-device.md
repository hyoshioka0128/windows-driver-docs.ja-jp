---
title: UMDF デバイスの状態の判断
description: このトピックでは、UMDF デバイスはどのような状態を確認すると共に、ユーザー モード ドライバー フレームワーク (UMDF) のバージョン 1 または 2 ドライバー デバッガー拡張機能を使用する方法について説明します。
ms.assetid: ed1a4429-4f36-44b9-9564-587aa381342f
keywords:
- UMDF WDK、UMDF デバイスの状態
- UMDF WDK、デバイスの状態
- ユーザー モード デバッガーの WDK UMDF、UMDF デバイスの状態を判断します。
- カーネル モードのデバッガー WDK UMDF、UMDF デバイスの状態を判断します。
- デバッグ シナリオ WDK UMDF、UMDF デバイスの状態
- UMDF WDK、デバッグ シナリオでは、UMDF デバイスの状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31efec7ebf074d7c67b153a95c7509bdf36036a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377444"
---
# <a name="determining-the-state-of-a-umdf-device"></a>UMDF デバイスの状態の判断


このトピックでは、UMDF デバイスはどのような状態を確認すると共に、ユーザー モード ドライバー フレームワーク (UMDF) のバージョン 1 または 2 ドライバー デバッガー拡張機能を使用する方法について説明します。

UMDF バージョン 1、wudfext.dll で実装された拡張機能のコマンドを使用します。 UMDF バージョン 2 以降、wdfkd.dll で実装された拡張機能のコマンドを使用します。

デバイスの状態を確認するのには、次の手順を使用します。

1.  次のデバッガーの種類のいずれかを使用してドライバーのホスト プロセスに分割します。
    -   ユーザー モード デバッガー:
        1.  デバイス (つまり、WUDFHost.exe) の適切なドライバーのホスト プロセスを見つけます。 ホスト プロセスの複数のインスタンスがある場合は、どのプロセスには、ドライバーをホストしているかを判断する Tasklist.exe のオペレーティング システムが指定したアプリケーションを使用できます。

            管理者特権でコマンド プロンプトから次のコマンドを使用します。

            **tasklist -m &lt;yourdriver.dll&gt;**

        2.  昇格された特権で、デバッガーを起動し、適切なプロセスにアタッチします。
        3.  シンボルの再読み込みを使用して、 **.reload**デバッガー コマンド。
        4.  すべてのスレッドを表示するを使用して、  **~ \*k**デバッガー コマンド。

    -   カーネル モード デバッガー:
        1.  デバイス (つまり、WUDFHost.exe) の適切なドライバーのホスト プロセスを見つけます。 使用して、 **! プロセス**カーネル モード デバッガー拡張がすべて WUDFHost.exe のインスタンスの一覧を取得する次の例に示すようにします。

            **!process 0 0 WUDFHost.exe**

            プロセスのアドレスとプロセスの環境ブロック (PEB) のアドレスから、 **! process 0 0**出力は次の手順で使用します。

        2.  次の方法のいずれかで、ホスト プロセスを接続します。
            -   使用して、 **.process**非干渉型のデバッガー コマンドが次の例に示すようにアタッチします。

                **.process/p/r&lt;プロセス addr&gt;**

                非侵を使用する必要がありますできません、引き続き実行できるようにする場合にアタッチします。 非侵を使用する必要がありますなど、アプリケーションで、中断を受信して、ドライバーが何を中断させるまたはときに、reflector をホスト プロセスを終了する準備を表示するときに添付します。

            -   使用して、 **.process**干渉のデバッガー コマンドが次の例に示すようにアタッチします。

                **.process /i &lt;process-addr&gt;**

                デバッガーを使用して続行することを要求、 **g**デバッガーのコマンドを実行した後すぐ、 **g**デバッガー コマンドをアクティブなプロセスにデバッガーが中断します。 使用してユーザーのシンボルの再読み込み、 **.reload**で次の例で示すように、デバッガー コマンド。

                **.reload /user**

        3.  ホスト プロセスの複数のインスタンスがある場合は、使用、 **! peb**プロセスに読み込まれるモジュールの一覧を取得する次の例に示すように、デバッガーの一般的な拡張機能。

            **! peb &lt;PEB アドレス&gt;**

            このコマンドを実行するプロセスにアタッチする必要があります。 非-invasively 前の手順で示すように割り当てることができます。

            DLL には、ドライバーが読み込まれているプロセスを見つけます。

        4.  使用して、 **! プロセス**カーネル モード デバッガー拡張がプロセスの詳細情報を取得する次の例で示すようにします。 情報には、プロセスおよびこれらのスレッドのアドレスでを実行するスレッドが含まれます。

            **!process &lt;process-addr&gt;**

        5.  使用して、 **! スレッド**カーネル モード デバッガー拡張が各スレッドについての情報を取得する次の例に示すようにします。

            **!thread &lt;thread-addr&gt;**

2.  デバッガーで使用して、 **.chain** wudfext.dll (UMDF 1) または wdfkd.dll (UMDF 2) デバッガー拡張機能ライブラリが読み込まれていることを確認するコマンド。
3.  使用して、必要なライブラリが存在しない場合、 [ **.load** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-load---loadby--load-extension-dll-)をデバッガーに拡張 DLL を読み込むコマンド。 Enter **.reload**シンボル情報を再読み込みします。
4.  使用[ **! wudfext.umdevstacks** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstacks) (UMDF 1) または[ **! wdfkd.wdfumdevstacks** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)ホスト プロセスで読み込まれた (UMDF 2)、すべてのデバイス スタックを参照してください。

    使用して[ **! wudfext.umdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstack) (UMDF 1) または[ **! wdfkd.wdfumdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)デバイスに関する詳細情報を取得する (UMDF 2)スタックです。

5.  使用[ **! wudfext.wudfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdevice) (UMDF 1) または[ **! wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice) (UMDF 2)、プラグ アンド プレイ (PnP) に関する情報を取得し、デバイスの電源管理の状態。

6.  使用[ **! wudfext.wudfdriverinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-wudfdriverinfo) (UMDF 1) または[ **! wdfkd.wdfdriverinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo) (UMDF 2) に関する追加情報を表示しますこのドライバーを使用して、そのデバイス ツリーを含みます。

 

 





