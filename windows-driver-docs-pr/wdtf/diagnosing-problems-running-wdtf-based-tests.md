---
title: WDTF ベース テストの実行時に発生する問題の診断
description: WDTF ベースのテストを実行している問題をトラブルシューティングするために、デバッガーを使用することができます。
ms.assetid: 24257B50-ED9C-4D45-A245-1EC855463D33
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad50db87b0ccd5a0a00ecd532dbb3d53ffa9d7cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386245"
---
# <a name="diagnosing-problems-running-wdtf-based-tests"></a>WDTF ベース テストの実行時に発生する問題の診断


WDTF ベースのテストを実行している問題をトラブルシューティングするために、デバッガーを使用することができます。

## <a name="diagnose-problems-with-unresponsive-wdtf-based-tests-run-from-visual-studio"></a>(Visual Studio から実行) が応答しなく WDTF ベースのテストに関する問題を診断します。


1.  構成し、カーネル デバッガーを WDTF ベースのテストを実行しているコンピューターに接続します。 参照してください[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。
2.  Te.exe プロセスとスイッチを検索するには、そのプロセスのコンテキスト。 Te.exe については、次を参照してください。[テストの作成および実行フレームワーク (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index)します。

    ``` syntax
    !process 0 0 Te.exe 

    PROCESS fffffa80093c6340

    SessionId: 1 Cid: 1320 Peb: 7f6595b3000 ParentCid: 12a0

    DirBase: 21eee000 ObjectTable: fffff8a0035b0a00 HandleCount: 327.

    Image: TE.exe

    ·         .process /p /r fffffa80093c6340

    ·         
    ```

3.  実行、 [ **! プロセス**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process) Te.exe で実行されているスレッドを識別するためにコマンド。

    ``` syntax
    !process fffffa80093c6340
    ```

    スレッドの検索**WDTF** \*スタックにします。

4.  (存在する) 場合は、Te.ProcessHost.exe の手順 3. を繰り返します。

## <a name="diagnose-problems-with-pnp-and-power-management-tests"></a>PnP に関する問題、および電源管理テストを診断します。


これらのコマンドの問題を診断できます。

[ **! powertriage** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-powertriage) (についてシステムとデバイスの電源関連のコンポーネントの情報を提供します) [ **! devnode** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-devnode) (PnP ツリーに関する情報を表示) する[ **! プロセス**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process) (関連付けられているスレッドを検索するプロセスの検証) を[ **! スレッド**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread) (スレッドに関する情報を表示) する[ **! wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice) (WDF ドライバー情報) をスタックしている PnP または電源管理のアクティブなスレッドがあることを確認した後 (この TickCount を確認します)、適切なコンポーネントでフォロー アップ所有者。 (スタックのスレッドのスタックを見てから、コンポーネントの所有者を検索できます。)

 

 




