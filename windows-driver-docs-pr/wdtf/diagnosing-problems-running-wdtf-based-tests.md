---
title: WDTF ベース テストの実行時に発生する問題の診断
description: WDTF ベースのテストを実行している問題をトラブルシューティングするために、デバッガーを使用することができます。
ms.assetid: 24257B50-ED9C-4D45-A245-1EC855463D33
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5136738c5fb9a69b6508ee3bafab18ba23616a03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574492"
---
# <a name="diagnosing-problems-running-wdtf-based-tests"></a>WDTF ベース テストの実行時に発生する問題の診断


WDTF ベースのテストを実行している問題をトラブルシューティングするために、デバッガーを使用することができます。

## <a name="diagnose-problems-with-unresponsive-wdtf-based-tests-run-from-visual-studio"></a>(Visual Studio から実行) が応答しなく WDTF ベースのテストに関する問題を診断します。


1.  構成し、カーネル デバッガーを WDTF ベースのテストを実行しているコンピューターに接続します。 参照してください[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/dn745909)します。
2.  Te.exe プロセスとスイッチを検索するには、そのプロセスのコンテキスト。 Te.exe については、次を参照してください。[テストの作成および実行フレームワーク (TAEF)](https://msdn.microsoft.com/library/windows/hardware/hh439725)します。

    ``` syntax
    !process 0 0 Te.exe 

    PROCESS fffffa80093c6340

    SessionId: 1 Cid: 1320 Peb: 7f6595b3000 ParentCid: 12a0

    DirBase: 21eee000 ObjectTable: fffff8a0035b0a00 HandleCount: 327.

    Image: TE.exe

    ·         .process /p /r fffffa80093c6340

    ·         
    ```

3.  実行、 [ **! プロセス**](https://msdn.microsoft.com/library/windows/hardware/ff564717) Te.exe で実行されているスレッドを識別するためにコマンド。

    ``` syntax
    !process fffffa80093c6340
    ```

    スレッドの検索**WDTF** \*スタックにします。

4.  (存在する) 場合は、Te.ProcessHost.exe の手順 3. を繰り返します。

## <a name="diagnose-problems-with-pnp-and-power-management-tests"></a>PnP に関する問題、および電源管理テストを診断します。


これらのコマンドの問題を診断できます。

[**! powertriage** ](https://msdn.microsoft.com/library/windows/hardware/mt431710) (についてシステムとデバイスの電源関連のコンポーネントの情報を提供します) [ **! devnode** ](https://msdn.microsoft.com/library/windows/hardware/ff562345) (PnP ツリーに関する情報を表示) する[**! プロセス**](https://msdn.microsoft.com/library/windows/hardware/ff564717) (関連付けられているスレッドを検索するプロセスの検証) を[ **! スレッド**](https://msdn.microsoft.com/library/windows/hardware/ff565440) (スレッドに関する情報を表示) する[ **! wdfkd.wdfdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff565703) (WDF ドライバー情報) をスタックしている PnP または電源管理のアクティブなスレッドがあることを確認した後 (この TickCount を確認します)、適切なコンポーネントでフォロー アップ所有者。 (スタックのスレッドのスタックを見てから、コンポーネントの所有者を検索できます。)

 

 




