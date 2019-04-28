---
title: ターゲット
description: ターゲット
ms.assetid: 103d9b0a-2d51-404e-b8b9-513465427f7b
keywords:
- デバッガー エンジンでは、ターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623b9eed23754f965a5b23a4c691a0b970463dd7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380490"
---
# <a name="targets"></a>ターゲット


[デバッガー エンジン](introduction.md#debugger-engine)ターゲットのさまざまな種類のデバッグをサポートしている[ユーザー モード](#live--user-mode-targets)と[カーネル モード](#live--kernel-mode-targets)ターゲット、ライブのターゲットおよびクラッシュ ダンプ ファイル、およびローカルとリモート対象とします。 さまざまな種類のターゲットに、エンジンを接続するためのさまざまな方法はあります。

### <a name="span-idcrashdumpfilesspanspan-idcrashdumpfilesspancrash-dump-files"></a><span id="crash_dump_files"></span><span id="CRASH_DUMP_FILES"></span>クラッシュ ダンプ ファイル

ユーザー モードとカーネル モードのクラッシュ ダンプ ファイルの両方がで開かれる[ **OpenDumpFile**](https://msdn.microsoft.com/library/windows/hardware/ff552322)します。 エンジンがターゲットをからダンプ ファイルを作成することも[ **WriteDumpFile2**](https://msdn.microsoft.com/library/windows/hardware/ff561382)します。

### <a name="span-idlive--user-mode-targetsspanspan-idlive--user-mode-targetsspanlive-user-mode-targets"></a><span id="live--user-mode-targets"></span><span id="LIVE--USER-MODE-TARGETS"></span>Live、ユーザー モードのターゲット

デバッガー エンジンを作成およびユーザー モード プロセスにアタッチします。

プロセスの作成は、コマンド ラインと必要に応じて初期のディレクトリと、新しいプロセスの環境を提供することで行われます。 エンジンでは、新しいプロセスに接続し、または、新しいプロセスの別のプロセスへの接続中に中断できます。 たとえば、クライアントとサーバーの両方で構成されるアプリケーションをデバッグするときに行うことが一時停止状態で、クライアントを作成して、サーバーのブレークポイントの前に、クライアントが実行され、サーバーで設定することができます、既に実行されているサーバーにアタッチ操作です。

プロセスからデタッチして、エンジン必要に応じて通常どおり実行されているプロセスのままに、プロセスを終了したり、(別のデバッガーが接続すると、またはが強制終了されたまで、中断状態になって) を破棄できます。

エンジンは、すべてのプロセス ID、プロセスを開始するために使用した実行可能イメージの名前など、コンピューターで実行されているユーザー モード プロセスに関する情報の照会できます。 この情報は、デバッグするプロセスを見つけやすいように使用できます。

### <a name="span-idlive--kernel-mode-targetsspanspan-idlive--kernel-mode-targetsspanlive-kernel-mode-targets"></a><span id="live--kernel-mode-targets"></span><span id="LIVE--KERNEL-MODE-TARGETS"></span>Live、カーネル モードのターゲット

メソッド[ **AttachKernel** ](https://msdn.microsoft.com/library/windows/hardware/ff538145) Windows カーネル デバッガー エンジンに接続します。

### <a name="span-idremote-targetsspanspan-idremote-targetsspanremote-targets"></a><span id="remote-targets"></span><span id="REMOTE-TARGETS"></span>リモート ターゲット

をリモートでデバッグするデバッガー エンジンを使用する場合は、可能性のある 2 つの余分な手順があります。

1.  ホストのエンジンに接続します。 ホスト エンジンがローカルのエンジンのインスタンスでない場合は、使用[ **DebugConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff540465)ホスト エンジンに接続されているクライアント オブジェクトを作成します。

2.  ホスト エンジンは、カーネルの接続のサーバー、プロセス サーバーに接続します。 ホスト エンジンがターゲットに直接接続できない場合は、プロセス サーバー、またはカーネル接続のサーバーに接続する必要があります。

ここでクライアントには、プロセス サーバー、またはカーネルの接続のサーバーからターゲットを取得するホスト エンジンがわかります。

### <a name="span-idacquiringtargetsspanspan-idacquiringtargetsspanacquiring-targets"></a><span id="acquiring_targets"></span><span id="ACQUIRING_TARGETS"></span>ターゲットを取得します。

ターゲットを取得する際に、ターゲットの取得は、ターゲットがイベントを生成するまでと完了しません。 通常、これは最初に呼び出して、ターゲットにデバッガーをアタッチするメソッドを呼び出す[ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)に通知するイベントを生成します。 この静止の保留場合に true をターゲットが常にこれらのクラッシュ ダンプ ファイルの格納、ダンプ ファイルを作成するを原因となったイベントでは通常のイベント。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ターゲットへのアタッチに関する詳細については、次を参照してください。[ターゲットへの接続](connecting-to-targets.md)します。

 

 





