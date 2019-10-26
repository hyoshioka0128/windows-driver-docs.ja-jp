---
title: Time Travel Debugging - トラブルシューティング
description: このセクションでは、タイムトラベルトレースのトラブルシューティングを行う方法について説明します。
ms.date: 10/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: a454221b6e823a59a0a770f628378e10b13ee705
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916119"
---
# <a name="time-travel-debugging---troubleshooting"></a>Time Travel Debugging - トラブルシューティング

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png) 

このセクションでは、タイムトラベルトレースのトラブルシューティングを行う方法について説明します。

## <a name="issues-attempting-to-record-a-process"></a>プロセスを記録しようとしている問題

### <a name="i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>"タイムトラベルのデバッグをサポートするために、管理者特権で実行する必要があります" というエラーメッセージが表示されます。

メッセージに示されているように、デバッガーを管理者特権で実行する必要があります。 デバッガーを管理者特権で実行するには、スタート メニューの  **WinDbg Preview** アイコンを右クリックし、**詳細** を選択し**て 管理者として実行** を選択 > ます。

### <a name="i-installed-windbg-preview-with-an-account-that-does-not-have-administrator-privileges-and-i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>管理者特権のないアカウントを使用して WinDbg Preview をインストールしました。「タイムトラベルのデバッグをサポートするには、WinDbg を昇格して実行する必要があります」というエラーメッセージが表示されます。

管理者特権を持つアカウントを使用して WinDbg Preview を再インストールし、そのアカウントをデバッガーで記録するときに使用します。

### <a name="i-cant-launch-and-record-a-uwp-application"></a>UWP アプリケーションを起動して記録できない

これは現時点ではサポートされていませんが、既に実行されている UWP アプリケーションにアタッチして記録することができます。

### <a name="i-cant-record-a-insert-name-of-unusual-process-type---running-in-another-session-security-context-credentials-process"></a>別のセッションで実行されている異常なプロセスの種類の < 挿入名を記録できません。セキュリティコンテキスト、資格情報...> プロセス

現時点では、TTD は通常のプロセスだけを記録します。通常は、コマンドコンソールから、または Windows エクスプローラーで実行可能ファイルまたはショートカットをクリックして起動できます。

### <a name="i-cannot-successfully-record-my-application-on-my-computer"></a>自分のコンピューターでアプリケーションを正常に記録できない

アプリケーションの記録に失敗した場合は、単純な Windows プロセスを記録できることを確認します。  たとえば、"ping.exe" または "cmd.exe" は、通常は記録できる単純なプロセスです。

### <a name="i-cannot-successfully-record-anything-at-all-on-my-computer"></a>コンピューターのすべてのものを正常に記録できません

TTD 記録は、アプリケーション仮想化フレームワーク、情報管理製品、セキュリティソフトウェア、またはウイルス対策製品など、他の影響を及ぼすテクノロジに干渉する可能性がある、侵害されたテクノロジです。

既知の TTD の非互換性については[、「タイムトラベルのデバッグ](time-travel-debugging-overview.md)」を参照してください。

### <a name="im-tracing-an-application-and-running-appverifer-at-the-same-time-and-the-performance-when-replaying-the-trace-is-slow"></a>アプリケーションをトレースし、同時に AppVerifer を実行していて、トレースを再生するときのパフォーマンスが低下しています。

AppVerifer がアプリケーションを確認するためにメモリを使用する方法により、後でトレースを再生するときのエクスペリエンスは、AppVerifier がなければ著しく悪化する可能性があります。 パフォーマンスを向上させるには、アプリを記録するときに AppVerifier を無効にします。 これが不可能な場合は、パフォーマンスを向上させるために、WinDbg の [呼び出し履歴] ウィンドウを閉じる必要がある場合があります。


## <a name="issues-with-idx-index-files"></a>に関する問題。IDX インデックスファイル

インデックスファイルのないトレースファイルや、破損または不完全なインデックスファイルを使用してデバッグすることは可能ですが、推奨されません。
デバッグ対象のプロセスから読み取られたメモリ値が最も正確であることを確認し、他のすべてのデバッグ操作の効率を向上させるには、インデックスファイルが必要です。

の状態を確認するには、`!index -status` コマンドを使用します。に関連付けられている IDX インデックスファイル。トレースファイルを実行します。

その場合は、`!index -force`を実行してインデックスファイルを再作成してみてください。

### <a name="recreating-the-idx-index-file"></a>を再作成します。IDX インデックスファイル

インデックスファイルに問題があると考えられる場合や、"インデックスファイルが読み込まれていません" 以外の内容が `!index -status` 場合は、再作成します。
これを行うには `!index -force`を実行します。 失敗した場合:

1. デバッガーを終了します。
2. 既存の IDX ファイルを削除します。と同じ名前になります。トレースファイルを実行し、と同じディレクトリに配置します。実行ファイルがです。
3. トレースを開きます。WinDbg プレビューでファイルを実行します。 これにより、`!index` のコマンドが実行され、インデックスが再作成されます。
4. `!index -status` コマンドを使用して、トレースインデックスが機能していることを確認します。

トレースファイルが存在する場所に、インデックスファイルに十分な領域があることを確認してください。
記録の内容によっては、インデックスファイルのサイズがトレースファイルよりも大幅に大きくなることがあります。通常、この順序は2倍のサイズになります。

## <a name="issues-with-trace-run-files"></a>トレースに関する問題。ファイルの実行

トレースに問題がある場合。ファイルを実行すると、次のようなエラーメッセージが表示されることがあります。

```dbgcmd
Replay and log are out of sync at fallback data. Packet type is incorrect "Packet Type"
Replay and log are out of sync at opaque data. Log had already reached the end
Replay exit thread event does not match up with logged event
Logged debug write values are out of sync with replay
```

ほとんどの場合、すべてのエラーメッセージは、を示しています。実行トレースファイルは使用できないため、再記録する必要があります。


### <a name="re-recording-the-user-mode-app"></a>ユーザーモードアプリを再記録する

ユーザーモードアプリの記録で特定の問題が発生した場合は、同じ PC で別のアプリを記録するか、別の PC で同じアプリを試すことをお勧めします。 アプリの特定の部分を記録する際に特定の問題があるかどうかを確認するために、アプリの別の用途を記録しておくことができます。


### <a name="when-debugging-or-creating-the-index-i-see-messages-about-derailment-events"></a>インデックスをデバッグまたは作成するときに、"Der" イベントに関するメッセージが表示されます。

次のようなメッセージが表示される可能性があります。

```dbgcmd
Derailment event MissingDataDerailment(7) on UTID 2, position 2A550B:108 with PC 0x7FFE5EEB4448 Request address: 0x600020, size: 32
```

TTD は、デバッガー内でエミュレーターを実行することによって機能します。これは、記録内のすべての位置でそのプロセスの状態をレプリケートするために、デバッグされたプロセスの指示を実行します。 このエミュレーターが、結果の状態とトレースファイル内の情報との間で何らかの不一致を監視するときに発生します。 たとえば、上の引用符で囲まれたエラーは、location 0x7FFE5EEB4448 で見つかった命令を示しています。これは、トレースの位置 2A550B: 108 で、記録に存在しない位置0x600020 を中心にメモリを読み取ろうとしました。

多くの場合、トレースにさかのぼって記録された命令で、レコーダーの何らかのエラー、またはエミュレーターで何らかのエラーが発生することがあります。 

ほとんどの場合、このエラーメッセージは、を示します。実行トレースファイルは、異なっしたスレッド内で、異なっしたポイントから開始します。これは、不特定数の命令によって発生します。 デバッグしようとしているイベントがこの期間内に発生しなかった場合は、トレースを使用できる可能性があります。 この期間中に対象のイベントが発生した場合は、トレースを再記録する必要があります。


## <a name="see-also"></a>参照

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

---






