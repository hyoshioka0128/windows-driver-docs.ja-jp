---
title: TraceView の開始と終了
description: TraceView の開始と終了
ms.assetid: ebadf441-c28a-4d8e-ae83-444c8a68f62b
keywords:
- Traceview で WDK、開始
- Traceview で WDK、終了
- Traceview で WDK、コマンド ライン インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c97ae0ddd275c3988108ab32d72be4cd2b64ec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387907"
---
# <a name="starting-and-exiting-traceview"></a>TraceView の開始と終了


## <span id="ddk_starting_traceview_tools"></span><span id="DDK_STARTING_TRACEVIEW_TOOLS"></span>


このトピックでは、traceview でウィンドウを開いたり閉じたりする方法について説明します。

### <a name="span-idstartingtraceviewspanspan-idstartingtraceviewspanstarting-traceview"></a><span id="starting_traceview"></span><span id="STARTING_TRACEVIEW"></span>Traceview での開始

Windows エクスプ ローラーで、traceview でを起動するに移動、\\ツール\\トレース\\WDK とダブルクリックの i386 サブディレクトリ、 **TraceView.exe**アイコン。

または、コマンド プロンプト ウィンドウに移動、\\ツール\\トレース\\の種類と WDK、i386 サブディレクトリ**traceview で**します。

### <a name="span-idexitingtraceviewspanspan-idexitingtraceviewspanexiting-traceview"></a><span id="exiting_traceview"></span><span id="EXITING_TRACEVIEW"></span>Traceview で終了します。

Traceview でを終了、**ファイル** メニューのをクリックして**終了**、traceview でウィンドウの右上隅の閉じるボタンをクリックします。

Traceview で終了すると、ときに開始された、停止、traceview でウィンドウで実行されているすべてのトレース セッション トレース セッションで実行されているトレース プロバイダーを無効にして、閉じます。 Windows ことを通知する traceview でが応答していないを完了するまでしばらくかかる場合があります。 終了する準備が整うまで traceview では強制されません。

Traceview で終了するなど、他の方法で開始されたトレース セッションを停止しません、 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)します。 これらのセッションは、それらを停止するか、Windows をシャット ダウンするまでの実行を続けます。

### <a name="span-idstartingthetraceviewcommandlineinterfacespanspan-idstartingthetraceviewcommandlineinterfacespanstarting-the-traceview-command-line-interface"></a><span id="starting_the_traceview_command_line_interface"></span><span id="STARTING_THE_TRACEVIEW_COMMAND_LINE_INTERFACE"></span>Traceview でコマンド ライン インターフェイスを開始

コマンドラインで traceview でを起動するには、コマンド プロンプト ウィンドウを開きに移動します、\\ツール\\トレース\\の WDK、およびなど、traceview でコマンドを入力し、i386 ディレクトリ**traceview で/でしょうか。** します。 (入力した場合**traceview で**パラメーターなしで traceview でウィンドウが表示されます)。

Traceview でコマンドについては、次を参照してください。 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)します。

 

 





