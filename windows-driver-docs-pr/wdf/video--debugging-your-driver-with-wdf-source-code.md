---
title: WDF ソースコードを使用したドライバーのデバッグに関するビデオ
description: このトピックには、WDF ソースコードへのフルアクセスを使用して Windows Driver Framework (WDF) ドライバーをデバッグする方法を示すビデオチュートリアルが含まれています。
Search.SourceType: Video
ms.assetid: 735D71FC-0B35-4C79-8C0A-F3C762095C06
ms.date: 05/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: ff1d549d0be4d33cbf391ffda8101adc831dda92
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925635"
---
# <a name="video-debugging-your-driver-with-wdf-source-code"></a>ビデオ: WDF ソースコードを使用したドライバーのデバッグ


このトピックには、WDF ソースコードへのフルアクセスを使用して Windows Driver Framework (WDF) ドライバーをデバッグする方法を示すビデオチュートリアルが含まれています。 ビデオの後に、簡単に参照できるように、ビデオの手順に従って説明します。


>[!VIDEO https://www.microsoft.com/videoplayer/embed/2568bc8a-3f0b-4900-b659-aa5b22159f04]

WDF ソースデバッグを使用すると、WDF ソースコードをダウンロードしなくても、フレームワークコードに自由にステップインできます。 デバッガーは、GitHub から正しいバージョンの WDF を自動的にダウンロードします。

たとえば、WinDbg を使用して Windows 10 コンピューターで WDF ドライバーをデバッグしていて、デバッガーが呼び出し履歴のフレームワークコードによって破損している場合は、[呼び出し履歴] ビューの WDF フレームをダブルクリックすると、関連する WDF ソースファイルが一致する行に自動的にダウンロードされて開きます。 その後、コードをステップ実行したり、ブレークポイントを設定したりできます。

この機能は、Windows 10 Technical Preview ビルド10041以降のパブリックリリースを実行しているターゲットシステムで使用できます。 これらのビルドには、Microsoft パブリックシンボルサーバーで使用可能な KMDF (Wdf01000) および UMDF (Wudfx02000) 用のプライベートソースのインデックス付きシンボルファイルがあります。 WDF コードのソースレベルのデバッグは、Visual Studio デバッガーではなく、WinDbg でのみ使用できます。

## <a name="quick-start"></a>クイック スタート

ターゲットコンピューターへの WinDbg カーネルデバッグセッションを開始し、次の手順に従います。

1. . Symfix を使用して、既定のシンボルパスを設定します。 これにより、シンボルパスがのシンボルサーバーを指すhttps://msdl.microsoft.com/download/symbolsように設定されます。

    `kd> .symfix`

2. . Srcfix を使用して、既定のソースパスを設定します。 これにより、ソースパスが srv * に設定されます。これにより、ターゲットモジュールのシンボルファイルで指定された場所からソースファイルを取得するようにデバッガーに指示します。

    ```
    kd> .srcfix
    Source search path is: SRV*
    ```

3. . Reload を使用してシンボルを再読み込みし、Wdf01000 シンボル (または UMDF の Wudfx02000) がソースインデックス付きであることを確認します。 次のように、! lmi の出力に示されているように、Wdf01000 PDB はソースインデックスが作成されています。 お持ちでない場合は、以下の「WinDbg セットアップ」セクションを参照してください。

    ```
    kd> .reload
    ...

    kd> !lmi wdf01000.sys
    Loaded Module Info: [wdf01000.sys] 
    ...
    Load Report: private symbols & lines, source indexed 
    C:\...\Wdf01000.pdb\...\Wdf01000.pdb
    ```

4. これですべてが設定されるようになりました。 WDF ソースコードを段階的に実行する簡単な方法は、フレームワークの IRP ディスパッチルーチンにブレークポイントを設定し、コードの残りの部分をステップ実行することです。 Windows システムには多くの受信トレイ KMDF ドライバーがあるため、WDF は常に読み込まれて実行されるため、このブレークポイントはすぐにヒットします (独自のドライバーを読み込む必要はありません)。

    ```
    kd> bp Wdf01000!FxDevice::DispatchWithLock
    kd> g
    Breakpoint 0 hit
    Wdf01000!FxDevice::DispatchWithLock:
    87131670 8bff mov edi,edi 
    ```

これがうまくいかない場合は、次の WinDbg のセットアップ手順を確認してください。 

## <a name="windbg-setup"></a>WinDbg セットアップ

上記の例が想定どおりに動作しない場合は、次の手順の1つ以上を実行する必要があります。

### <a name="enable-source-mode-debugging"></a>ソースモードのデバッグを有効にする

[ソースモードでのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-in-source-mode)が有効になっていることを確認します。 [デバッグ] メニューを開き、[ソースモード] がオンになっていることを確認します。


 
### <a name="clear-stale-symbols-cache"></a>古いシンボルキャッシュのクリア

以前に同じ Windows ターゲットに対して WDF ドライバーをデバッグした場合は、ソースのインデックスが作成されていないローカルにキャッシュされた WDF シンボルを使用している可能性があります。 これは、! lmi コマンドを使用して確認できます。

    ```
    kd> !lmi Wdf01000.sys
    Loaded Module Info: [wdf01000.sys]
    ...
    Load Report: private symbols & lines, not source indexed
    C:\...\Wdf01000.pdb\...\Wdf01000.pdb
    ```

上のロードレポートによれば、Wdf01000 はソースのインデックスが作成されていません。 これは、ローカルの WinDbg シンボルキャッシュが古くなっていることを意味します。 この問題を解決するには、WinDbg から PDB をアンロードし、ローカルキャッシュをクリアします (上記の! lmi 出力によってパスが異なる場合があります)。次に、PDB を再読み込みします。

    ```
    kd> .reload /u Wdf01000.sys

    CMD> del
    C:\...\Wdf01000.pdb\...\Wdf01000.pdb

    kd> .reload Wdf01000.sys
    ```

次に、[lmi] を実行してもう一度確認します。 PDB はソースインデックスとして表示され、ソースコードウィンドウがポップアップ表示されます。

    ```
    kd> !lmi Wdf01000.sys
    Loaded Module Info: [wdf01000.sys]
    ...
    Load Report: private symbols & lines, source indexed
    C:\...\Wdf01000.pdb\...\Wdf01000.pdb 
    ```

WDF ソースレベルのデバッグは、ライブデバッグとクラッシュダンプの分析だけでなく、IRP ディスパッチャーのようなコア関数にブレークポイントを設定し、後続のコードパスを調べることで、フレームワークの内部構造の詳細を学習するためにも使用できます。



