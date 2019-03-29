---
title: カーネル デバッガーにトレース メッセージを送信する方法
description: カーネル デバッガーにトレース メッセージを送信する方法
ms.assetid: 867791a7-30a5-4539-be85-61f1716c279a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2783a065d9dce8080d559cefb394c47c5d29d483
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579389"
---
# <a name="how-do-i-send-trace-messages-to-a-kernel-debugger"></a>カーネル デバッガーにトレース メッセージを送信する方法


いくつかのメソッドを使用して、トレース メッセージをカーネル モードのデバッガーにリダイレクトすることができます。 ここでは、いくつかについて説明します。

トレース メッセージをリダイレクトするには、Windbg、KD からか、どちらがアタッチされています。 デバッグ (ヌル モデム) ケーブルを使用して COM ポートを使用または IEEE 1394 ケーブルで 1394 ("firewire") のポートを介して、デバッガーをアタッチする必要があります。 NTSD などの他のカーネル デバッガーには、トレース メッセージをリダイレクトすることはできません。

デバッガーでのトレース メッセージを表示するには、wmitrace.dll と traceprt.dll する必要がありますにホスト コンピューターで、デバッガーの検索パス。 これらの Dll が含まれている[ツールを Windows のデバッグ](https://go.microsoft.com/fwlink/p/?linkid=8708)も、検索するデバッガーを有効にする、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)、トレース メッセージの TMF ファイルは、デバッガーの検索である必要がありますホスト コンピューター上のパス。 デバッガーの検索パスを設定するには、使用、! wmitrace.searchpath デバッガー拡張機能を特殊化または % のトレースの値を設定\_形式\_検索\_%path% 環境変数。

詳細については、検索 **! wmitrace**で*ツールを Windows のデバッグ*します。

### <a name="span-idlogmanspanspan-idlogmanspanlogman"></a><span id="logman"></span><span id="LOGMAN"></span>Logman

トレース メッセージをカーネル モードのデバッガーにリダイレクトするのにには、Logman の次のコマンドを使用します。

```
logman start TraceSession -ets -mode KernelFilter -bs 3
```

**-Ets**パラメーターは、パフォーマンス ログと警告サービスによって管理されていないイベント トレース セッションを開始します。 **-モード**パラメーターなど、高度なオプションがアクティブになります、 **KernelFilter**オプション。

**-Bs**パラメーターは 3 KB、デバッガーの最大バッファー サイズをトレース セッションのバッファー サイズを設定します。 このパラメーターを省略した場合、デバッガー セッションが正しく動作しません。

Windows XP および Windows の以降のバージョンので Logman が含まれます。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>トレース ログ

次を使用して、 [Tracelog](tracelog.md)コマンド、カーネル モードのデバッガーへのリダイレクト トレース メッセージ。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**- Guid**パラメーターを指定します、[トレース プロバイダー](trace-provider.md)します。 **-Rt**パラメーターは、リアルタイムのトレース セッションを指定します。 **-Kd**パラメーターは、カーネル デバッガーにトレース メッセージをリダイレクトし、最大バッファー サイズは 3 KB、デバッガーの最大値を設定します。

例については、次を参照してください。[例 16。デバッガーでのトレース メッセージを表示する](example-16--viewing-trace-messages-in-a-debugger.md)します。

トレース ログは、ツールにある\\トレース\\*&lt;プラットフォーム&gt;* 、WDK のサブディレクトリで*&lt;プラットフォーム&gt;* i386、amd64、または ia64 のいずれかです。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>Traceview で

[Traceview で](traceview.md)はグラフィカル ユーザー インターフェイスがあります。

トレース セッションを作成するときに、カーネル デバッガーにトレース メッセージをリダイレクトできます。 **ログ セッション オプション** ページで **ログ セッション オプションの高度な**、 をクリックして、**ログ セッションのパラメーター オプション**タブをクリックし、の値を変更し、**Windbg**オプションを**TRUE**します。 トレース セッションの実行中に、このオプションを変更することはできません。

Traceview では、ツールである\\トレース\\*&lt;プラットフォーム&gt;* 、WDK のサブディレクトリで*&lt;プラットフォーム&gt;* i386、amd64、または ia64 のいずれかです。

 

 





