---
title: タイム トラベル デバッグ - トラブルシューティング
description: このセクションは、時間のトラブルシューティングを行う方法を説明しますトレースを移動します。
ms.date: 10/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9fcb1c922b3bc769d78153c0fb90c01f31be67f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530870"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---troubleshooting"></a>タイム トラベル デバッグ - トラブルシューティング

このセクションは、時間のトラブルシューティングを行う方法を説明しますトレースを移動します。

## <a name="issues-attempting-to-record-a-process"></a>問題のプロセスを記録しようとしています。

### <a name="i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>「WinDbg 実行する必要があるタイム トラベルのデバッグをサポートするために管理者特権で」というエラー メッセージします。

メッセージが示すとおり、管理者特権でのデバッガーを実行しているが必要です。 管理者特権でのデバッガーを実行するのを右クリックし、 **WinDbg プレビュー**アイコンをクリックして [スタート] メニューで**詳細** > **管理者として実行**します。

### <a name="i-installed-windbg-preview-with-an-account-that-does-not-have-administrator-privileges-and-i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>管理者特権がないアカウントを使用して WinDbg Preview をインストールして、「WinDbg 実行する必要があるタイム トラベルのデバッグをサポートするために管理者特権で」というエラー メッセージが表示

WinDbg を管理者特権を持つアカウントを使用してプレビューを再インストールし、デバッガーで記録するときに、そのアカウントを使用します。

### <a name="i-cant-launch-and-record-a-uwp-application"></a>起動し、UWP アプリケーションを記録することはできません。

これは、現時点ではサポートされていませんをアタッチし、既に実行中の UWP アプリケーションを記録することがあります。

### <a name="i-cant-record-a-insert-name-of-unusual-process-type---running-in-another-session-security-context-credentials-process"></a>記録できません、< の通常とは異なるプロセスの種類 - 別のセッション、セキュリティ コンテキストは、資格情報で実行されている名前を挿入しています.> プロセス

この時点で TTD はことを通常どおり起動できるコマンド コンソールから、または、実行可能ファイルまたは Windows エクスプ ローラーのショートカットをクリックして通常のプロセスのみを記録します。

### <a name="i-cannot-successfully-record-my-application-on-my-computer"></a>私のコンピューターでアプリケーションが正常に記録できません。

アプリケーションの記録に失敗した場合、シンプルな Windows プロセスを記録することを確認します。  たとえば、"ping.exe"または"cmd.exe"は、通常記録できる単純なプロセスです。

### <a name="i-cannot-successfully-record-anything-at-all-on-my-computer"></a>正常に記録できません何もすべてのコンピューターで

TTD 記録は、アプリケーション仮想化のフレームワーク、管理製品の情報、セキュリティ ソフトウェアやウイルス対策製品などの他の干渉のテクノロジに干渉することができます、侵テクノロジです。

「検索すること」を参照してください[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)既知 TTD 非互換性について。

### <a name="im-tracing-an-application-and-running-appverifer-at-the-same-time-and-the-performance-when-replaying-the-trace-is-slow"></a>アプリケーションのトレースであり、同時 AppVerifer を実行していると、トレースを再生する場合のパフォーマンスが低下します。

方法により AppVerifer はメモリを使用してよりも著しく悪い AppVerifier せず、トレースの再生にできる場合に、エクスペリエンス、後でアプリケーションを確認します。 パフォーマンスを向上させるには、アプリを記録するときに、AppVerifier を無効にします。 それができない場合は、パフォーマンスを向上させるために WinDbg で呼び出し履歴ウィンドウを閉じる必要があります。


## <a name="issues-with-idx-index-files"></a>問題です。IDX インデックス ファイル

インデックス ファイルを使用しないか破損しているか不完全なインデックス ファイルでは、トレース ファイルのデバッグは可能ですは推奨されません。
インデックス ファイルがそのメモリを実現に必要なデバッグ対象のプロセスから読み取られた値が最も正確なおよびその他のすべてのデバッグ操作の効率を向上させる。

使用して、`!index -status`コマンドの状態を確認します。IDX インデックスのファイルに関連付けられている、します。トレース ファイルを実行します。

その可能性がありますしようとすると、インデックス ファイルを再作成を実行して`!index -force`します。

### <a name="recreating-the-idx-index-file"></a>再作成します。IDX インデックス ファイル

疑いがあるし、インデックス ファイルを発行する場合または`!index -status`以外は何も「読み込まれるファイルのインデックス」で、再作成します。
実行することがありますこれを行う`!index -force`します。 失敗したかどうか。

1. デバッガーを閉じます。
2. 既存の IDX ファイルを削除と同じ名前になります、します。トレース ファイルを実行し、同じディレクトリに存在するが、します。実行ファイルは次のとおりです。
3. トレースを開きます。WinDbg のプレビューでは、ファイルを実行します。 これは、実行、`!index`インデックスを再作成するコマンド。
4. 使用して、`!index -status`コマンドをトレースのインデックスが機能していることを確認します。

トレース ファイルが存在する同じ場所にインデックス ファイルのための十分な領域があることを確認します。
によっては、記録の内容は、インデックス ファイルが大きなトレース ファイルで、通常約 2 倍よりもずっと大きな可能性があります。

## <a name="issues-with-trace-run-files"></a>トレースの問題です。ファイルを実行します。

トレースの問題がある場合。ファイルを実行するには、次のようにエラー メッセージが表示可能性があります。

```dbgcmd
Replay and log are out of sync at fallback data. Packet type is incorrect "Packet Type"
Replay and log are out of sync at opaque data. Log had already reached the end
Replay exit thread event does not match up with logged event
Logged debug write values are out of sync with replay
```

ほとんどの場合のエラー メッセージをすべて示すします。実行のトレース ファイルは使用できませんし、再記録する必要があります。


### <a name="re-recording-the-user-mode-app"></a>ユーザー モードのアプリを再記録

ユーザー モードのアプリの録画に関する特定の問題がある場合は、同じの pc では、別のアプリを記録してみてくださいする場合や、別の PC で同じアプリをお試しください可能性があります。 アプリの特定の部分を録画に関する特定の問題があるかどうかは、アプリのさまざまな使用を記録することがあります。


### <a name="when-debugging-or-creating-the-index-i-see-messages-about-derailment-events"></a>デバッグまたはインデックスを作成する、「脱線イベント」に関するメッセージを表示します。

このようなメッセージが生じることができます。

```dbgcmd
Derailment event MissingDataDerailment(7) on UTID 2, position 2A550B:108 with PC 0x7FFE5EEB4448 Request address: 0x600020, size: 32
```

TTD は記録内の各位置にそのプロセスの状態をレプリケートするには、デバッグ対象プロセスの手順を実行すると、デバッガー内でエミュレーターを実行して動作します。 つまずくは、このエミュレーターはなんらかの結果の状態と、トレース ファイルに含まれる情報の間に不一致を監視するときに発生します。 上、引用符で囲まれたエラーは、たとえば、拠点 0x7FFE5EEB4448、位置 2A550B:108 は記録に存在しない場所 0x600020、周囲のいくつかのメモリを読み取るしようとしています。 これは、トレース内で見つかった命令を参照します。

つまずくは、レコーダーでまたはエミュレーターでいくつかのエラーによって発生した多くの場合、トレースにさらにいくつかの記録された命令にします。 

ほとんどの場合にこのエラー メッセージことを示します、します。実行のトレース ファイルが必要で derailed、命令のいくつかの不確定な数の derailed その時点で開始したスレッドにギャップがあります。 デバッグしようとして関心のあるイベントは、その間隔中に発生していない、トレースが使用可能な可能性があります。 その間隔中に関心のあるイベントが発生した場合は、トレースを再記録する必要があります。


## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---






