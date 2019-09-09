---
title: I (Windows デバッガー用語集)
description: 用語集のページ-H
ms.assetid: 4415522d-6ea3-42f6-9acc-0e3ceaa36dc7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b6cbd422ef35bf4b0ff43c13c3814a2a37853c6
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387071"
---
# <a name="i"></a>I


<span id="i_o_request_packet__irp_"></span><span id="I_O_REQUEST_PACKET__IRP_"></span>**I/o 要求パケット (IRP)**  
I/o 要求を表し、その処理を制御するために使用されるデータ構造。 IRP 構造体は、ヘッダーと1つ以上のスタック位置で構成されます。

<span id="image"></span><span id="IMAGE"></span>**絵**  
Windows によってユーザーモードプロセスまたは Windows カーネルの一部として読み込まれた実行可能ファイル、DLL、またはドライバー。

「イメージファイル」も参照してください。

<span id="image_file"></span><span id="IMAGE_FILE"></span>**イメージファイル**  
イメージの読み込み元のファイル。

<span id="implicit_process"></span><span id="IMPLICIT_PROCESS"></span>**暗黙のプロセス**  
カーネルモードのデバッグでは、仮想マシンから物理アドレスへの変換を実行するときに使用する仮想アドレス空間を決定するために使用されるプロセス。 イベントが発生すると、暗黙のプロセスがイベントプロセスに設定されます。

「暗黙的なスレッド」も参照してください。

詳細については、「[スレッドとプロセス](threads-and-processes.md)」を参照してください。

<span id="implicit_thread"></span><span id="IMPLICIT_THREAD"></span>**暗黙のスレッド**  
カーネルモードのデバッグでは、フレームオフセットや命令オフセットなど、ターゲットのレジスタの一部を決定するために使用されるスレッド。 イベントが発生すると、暗黙的なスレッドがイベントスレッドに設定されます。

<span id="inaccessible"></span><span id="INACCESSIBLE"></span>**アク**  
すべてのターゲットが実行されている場合、デバッグセッションにアクセスすることは*できませ*ん。

<span id="initial_breakpoint"></span><span id="INITIAL_BREAKPOINT"></span>**最初のブレークポイント**  
デバッグセッションの開始間近、再起動後、または対象アプリケーションの再起動後に自動的に発生するブレークポイント。

詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

<span id="input_callback_objects"></span><span id="INPUT_CALLBACK_OBJECTS"></span>**入力コールバックオブジェクト**  
クライアントに登録されている[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)インターフェイスのインスタンス。 デバッガーエンジンは、入力を必要とするたびに、入力コールバックに指定を要求します。

「出力コールバック」も参照してください。

詳細については、「 [AMLI デバッガーコマンドの使用](using-amli-debugger-commands.md)」を参照してください。

<span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>**入力コールバック**  
「入力コールバックオブジェクト」を参照してください。

<span id="interrupt"></span><span id="INTERRUPT"></span>**妨害**  
通常のコマンドの実行を中断し、割り込みハンドラーに制御を転送する条件。 プロセッサのサービスを必要とする i/o デバイスは、通常、割り込みを開始します。

<span id="interrupt_request_level__irql_"></span><span id="INTERRUPT_REQUEST_LEVEL__IRQL_"></span>**割り込み要求レベル (IRQL)**  
割り込みの優先順位。 各プロセッサには、スレッドが発生させることのできる IRQL の設定があります。 プロセッサの IRQL 設定の下または下で発生する割り込みはマスクされ、現在の操作に干渉することはありません。 プロセッサの IRQL 設定を超える割り込みは、現在の操作よりも優先されます。

 

 





