---
title: ターゲット
description: ターゲット
ms.assetid: 103d9b0a-2d51-404e-b8b9-513465427f7b
keywords:
- デバッガーエンジン、ターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057ef3a2beb9a317141b58add9fb2e1f6a9248f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838809"
---
# <a name="targets"></a>ターゲット


[デバッガーエンジン](introduction.md#debugger-engine)では、さまざまな種類のターゲット、[ユーザーモード](#live--user-mode-targets)と[カーネルモード](#live--kernel-mode-targets)のターゲット、ライブターゲットとクラッシュダンプファイル、およびローカルターゲットとリモートターゲットのデバッグがサポートされています。 エンジンをこれらの異なる種類のターゲットに接続するには、さまざまな方法があります。

### <a name="span-idcrash_dump_filesspanspan-idcrash_dump_filesspancrash-dump-files"></a><span id="crash_dump_files"></span><span id="CRASH_DUMP_FILES"></span>クラッシュダンプファイル

[**OpenDumpFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfile)を使用して、ユーザーモードとカーネルモードのクラッシュダンプファイルの両方が開かれます。 エンジンは、 [**WriteDumpFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)を使用してターゲットからダンプファイルを作成することもできます。

### <a name="span-idlive--user-mode-targetsspanspan-idlive--user-mode-targetsspanlive-user-mode-targets"></a><span id="live--user-mode-targets"></span><span id="LIVE--USER-MODE-TARGETS"></span>ライブ、ユーザーモードターゲット

デバッガーエンジンは、ユーザーモードプロセスを作成してアタッチすることができます。

プロセスを作成するには、新しいプロセスのコマンドラインと、必要に応じて初期ディレクトリと環境を指定します。 その後、エンジンは新しいプロセスに接続したり、別のプロセスに接続している間は新しいプロセスを中断したままにすることができます。 たとえば、クライアントとサーバーの両方で構成されるアプリケーションをデバッグする場合、中断状態のクライアントを作成し、既に実行されているサーバーにアタッチすることができます。これにより、クライアントを実行してサーバーを誘発する前に、サーバーのブレークポイントを設定できるようになります。業務.

プロセスからデタッチする場合、エンジンは、必要に応じてプロセスを正常に実行したままにするか、プロセスを強制終了するか、またはプロセスを破棄します (別のデバッガーがアタッチするか、強制終了されるまで中断されます)。

プロセスを開始するために使用される実行可能イメージのプロセス ID や名前など、コンピューター上で実行されているすべてのユーザーモードプロセスに関する情報を照会できます。 この情報は、デバッグするプロセスを見つけるために使用できます。

### <a name="span-idlive--kernel-mode-targetsspanspan-idlive--kernel-mode-targetsspanlive-kernel-mode-targets"></a><span id="live--kernel-mode-targets"></span><span id="LIVE--KERNEL-MODE-TARGETS"></span>ライブ、カーネルモードターゲット

[**Attachkernel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachkernel)メソッドは、デバッガーエンジンを Windows カーネルに接続します。

### <a name="span-idremote-targetsspanspan-idremote-targetsspanremote-targets"></a><span id="remote-targets"></span><span id="REMOTE-TARGETS"></span>リモートターゲット

デバッガーエンジンを使用してリモートでデバッグする場合、次の2つの追加の手順があります。

1.  ホストエンジンに接続します。 ホストエンジンがローカルエンジンインスタンスでない場合は、 [**Debugconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)を使用して、ホストエンジンに接続されているクライアントオブジェクトを作成します。

2.  ホストエンジンをプロセスサーバーまたはカーネル接続サーバーに接続します。 ホストエンジンがターゲットに直接接続しない場合は、プロセスサーバーまたはを実行するカーネル接続サーバーに接続する必要があります。

これで、クライアントは、プロセスサーバーまたはカーネル接続サーバーを介してターゲットを取得するようにホストエンジンに指示できます。

### <a name="span-idacquiring_targetsspanspan-idacquiring_targetsspanacquiring-targets"></a><span id="acquiring_targets"></span><span id="ACQUIRING_TARGETS"></span>ターゲットの取得

ターゲットを取得するとき、ターゲットがイベントを生成するまで、ターゲットの取得は完了しません。 通常、これは、最初にデバッガーをターゲットにアタッチするメソッドを呼び出し、次に[**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)を呼び出してターゲットにイベントを生成させることを意味します。 これは、ターゲットがクラッシュダンプファイルの場合にも当てはまります。これは、ターゲットが常にイベント (通常はダンプファイルを作成したイベント) を格納するためです。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ターゲットへのアタッチの詳細については、「[ターゲットへの接続](connecting-to-targets.md)」を参照してください。

 

 





