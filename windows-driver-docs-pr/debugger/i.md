---
title: (Windows デバッガーの用語集)
description: 用語集ページ - H
Robots: noindex, nofollow
ms.assetid: 4415522d-6ea3-42f6-9acc-0e3ceaa36dc7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c244b178522ecf323c67abe4a4818f48e03ee1f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366833"
---
# <a name="i"></a>I


<span id="i_o_request_packet__irp_"></span><span id="I_O_REQUEST_PACKET__IRP_"></span>**I/O 要求パケット (IRP)**  
I/O 要求を表し、その処理を制御するために使用するデータ構造。 IRP の構造体は、ヘッダーとスタックの 1 つまたは複数の場所で構成されます。

<span id="image"></span><span id="IMAGE"></span>**イメージ**  
実行可能ファイル、DLL、またはユーザー モード プロセスまたは Windows カーネルの一部として Windows が読み込まれているドライバーです。

イメージ ファイルを参照してください。

<span id="image_file"></span><span id="IMAGE_FILE"></span>**イメージ ファイル**  
イメージの読み込み元のファイルです。

<span id="implicit_process"></span><span id="IMPLICIT_PROCESS"></span>**暗黙的なプロセス**  
カーネル モードでプロセスのデバッグ、物理仮想アドレス変換を実行するときに使用するには、どの仮想アドレス空間を決定するために使用します。 イベントの発生時に、暗黙的なプロセスは、イベントの処理に設定されます。

暗黙的なスレッドを参照してください。

詳細については、次を参照してください。[スレッドとプロセス](threads-and-processes.md)します。

<span id="implicit_thread"></span><span id="IMPLICIT_THREAD"></span>**暗黙的なスレッド**  
カーネル モードでデバッグするには、ターゲットのレジスタのいくつかの判断に使用されるスレッドなどのフレームのオフセットし、命令のオフセットします。 イベントの発生時に、暗黙的なスレッドは、イベントのスレッドに設定されます。

<span id="inaccessible"></span><span id="INACCESSIBLE"></span>**アクセスできません。**  
デバッグ セッションは*アクセスできない*のすべてのターゲットが実行されます。

<span id="initial_breakpoint"></span><span id="INITIAL_BREAKPOINT"></span>**最初のブレークポイント**  
再起動後、または対象のアプリケーションが再起動した後、デバッグ セッションの先頭付近に自動的に発生するブレークポイントです。

詳細については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。

<span id="input_callback_objects"></span><span id="INPUT_CALLBACK_OBJECTS"></span>**入力のコールバック オブジェクト**  
インスタンス、 [IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)クライアントに登録されているインターフェイス。 デバッガー エンジンが入力を必要とされるたびに、入力のコールバックを提供するよう要求されます。

出力のコールバックを参照してください。

詳細については、次を参照してください。 [AMLI デバッガー コマンドを使用して](using-amli-debugger-commands.md)します。

<span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>**入力のコールバック**  
入力のコールバック オブジェクトを参照してください。

<span id="interrupt"></span><span id="INTERRUPT"></span>**割り込み**  
割り込みハンドラーに通常のコマンドの実行と転送コントロールを中断する条件。 通常は、プロセッサからサービスを必要とする I/O デバイスでは、割り込みを開始します。

<span id="interrupt_request_level__irql_"></span><span id="INTERRUPT_REQUEST_LEVEL__IRQL_"></span>**割り込み要求レベル (IRQL)**  
割り込みの優先順位。 各プロセッサには、スレッドを上げたり下げたりする IRQL 設定があります。 プロセッサの IRQL 設定以下で発生する割り込みは、マスクされ、現在の操作には影響しません。 プロセッサの IRQL 設定の上で発生した割り込みは、現在の操作よりも優先されます。

 

 





