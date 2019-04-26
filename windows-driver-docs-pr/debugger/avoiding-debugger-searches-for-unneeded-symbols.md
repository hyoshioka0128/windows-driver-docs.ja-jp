---
title: デバッガーによる不要なシンボルの検索の回避
description: 理由はシンボルの読み込みもほど時間がかかるでしょうか。 シンボル名は、修飾名または修飾されていないかどうかによって異なります。
ms.assetid: 710BAEAF-BC45-416E-8359-69E9DFCA2570
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2ac691b1bb58f52f506e9fb7d3fbf6caa5031fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354399"
---
# <a name="avoiding-debugger-searches-for-un-needed-symbols"></a>不要にするデバッガーが不要なシンボルを検索します。


**最終更新日。**

-   2007 年 5 月 27 日

興味深いブレークポイントに到着するには、「のデバッグ作業にも重要でないを所有していないドライバーのシンボルの読み込みを試行中非常に長い時間が一時停止デバッガーがある場合にのみ、ドライバーのデバッグ中にします。 何が起こったのでしょうか。

既定では、シンボルは、必要に応じて、デバッガーによって読み込まれます。 (これが呼び出されます遅延シンボルの読み込みまたは遅延シンボルの読み込み。)デバッガーは、シンボルの表示を呼び出して取得するコマンドを実行するたびに、シンボルを検索します。 これは、コンテキストが変更されたときに無効ななるため、関数のパラメーターなど、現在のコンテキストで有効でないウォッチ変数または現在のスタック フレームに存在しないローカル変数を設定している場合、ブレークポイントで発生します。 でも発生します。 単にシンボル名を入力またはコマンドの無効なデバッガーを実行する場合デバッガーが一致するシンボルの検索を開始します。

これはなぜかかる非常に長いことがありますか。 シンボル名は、修飾名または修飾されていないかどうかによって異なります。 修飾シンボル名の記号を含むモジュールの名前が付きます-たとえば、myModule! myVar します。 修飾されていないシンボルの名前はモジュール名を指定しない-myOtherVar など。

修飾名の場合、デバッガー、指定したモジュールのシンボルを検索し、モジュールが既に読み込まれていない場合は、(モジュールが存在し、記号を含むを想定) モジュールを読み込みます。 これは非常に簡単に起こります。

非修飾名では、場合、デバッガーは「がわからない」でそれらのすべてに表示する必要がありますので、どのモジュールが、記号を格納します。 デバッガーがシンボルのすべての読み込まれたモジュールを最初にチェックし、次に、読み込むモジュール内の記号が一致しない場合、デバッガー、アンロード、すべての読み込みによって検索モジュール以降では、ダウン ストリームのストアと場合、シンボル サーバーで終わるいずれかを使用します。 当然ながら、この大量の時間がかかります。

## <a name="span-idhowtopreventautomaticloadingforunqualifiedsymbolsspanspan-idhowtopreventautomaticloadingforunqualifiedsymbolsspanspan-idhowtopreventautomaticloadingforunqualifiedsymbolsspanhow-to-prevent-automatic-loading-for-unqualified-symbols"></a><span id="How_to_prevent_automatic_loading_for_unqualified_symbols_"></span><span id="how_to_prevent_automatic_loading_for_unqualified_symbols_"></span><span id="HOW_TO_PREVENT_AUTOMATIC_LOADING_FOR_UNQUALIFIED_SYMBOLS_"></span>修飾されていないシンボルの自動読み込みを回避する方法


**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**オプションが非修飾のシンボルを検索するときに、モジュールのデバッガーの自動読み込みを有効または無効にします。 ときに**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**が設定され、デバッガーに非修飾のシンボルを照合する検索のみモジュールを既に読み込まれているときに検索を停止しますが検索を継続する読み込まれたモジュールの読み込みではなく、シンボルを一致することはできません。 このオプションは、修飾名の検索には影響しません。

**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**は既定で無効です。 このオプションを有効にするには、使用、 **- snul**コマンド ライン オプション、またはデバッガーの実行中を使用して、 **.symopt + 0x100**または **.symopt 0x100**オンまたはオフ、オプションを有効にするにはそれぞれします。

効果を確認する**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**、この実験を実行してください。

1.  ノイズの多いシンボルの読み込みをアクティブ化 (**SYMOPT\_デバッグ**) を使用して、 **-n**コマンド ライン オプション、またはデバッガーが既に実行されている場合は、使用 **.symopt + 0x80000000**または **! sym ノイズの多い**デバッガー拡張機能コマンド。 **SYMOPT\_デバッグ**デバッガー ファイルが見つからない場合は、読み込まれると、各モジュールの名前などのシンボルの検索に関する情報を表示するデバッガーまたはエラー メッセージを指示します。
2.  存在しないシンボルを評価するデバッガーに指示する (たとえば、「**でしょうか。 asdasdasd**)。 デバッガーは、存在しないシンボルの検索中に多数のエラーを報告する必要があります。
3.  アクティブ化**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**を使用して **.symopt + 0x100**します。
4.  手順 2. を繰り返します。 デバッガーが存在しないのシンボルのみ読み込まれたモジュールを検索する必要があり、はるかに高速のタスクを完了する必要があります。
5.  無効にする**SYMOPT\_デバッグ**を使用して、 **.symopt 0x80000000**または **! sym quiet**デバッガー拡張機能コマンド。

さまざまなオプション、デバッガーの読み込みし、シンボルを使用して制御を利用できます。 シンボルのオプションとその使用方法の完全な一覧は、Windows のツールをデバッグで提供されるオンライン ドキュメントの「シンボル オプションの設定」を参照してください。 Windows のツールをデバッグ パッケージの最新リリースは、web から無料でダウンロードとして入手できますか Windows DDK、Platform SDK、またはカスタマー サポート診断用 CD からパッケージをインストールすることができます。

## <a name="span-idwhatshouldyoudospanspan-idwhatshouldyoudospanspan-idwhatshouldyoudospanwhat-should-you-do"></a><span id="What_should_you_do__"></span><span id="what_should_you_do__"></span><span id="WHAT_SHOULD_YOU_DO__"></span>何を実行する必要がありますか


-   シンボルの検索の速度、ブレークポイントと可能な限りのデバッガー コマンドで修飾名を使用します。 既知のモジュールからのシンボルを表示する場合は、モジュール名で修飾します。シンボルの場所がわからない場合は、非修飾名を使用します。 ローカル変数と関数の引数は、次のように使用します**$** モジュール名と (たとえば、 *$!。MyVar*)。
-   シンボルの読み込みが低速の原因を診断するためには、ノイズの多いシンボルの読み込みをアクティブ化 (**SYMOPT\_デバッグ**) を使用して、 **-n**コマンド ライン オプションまたは、を使用して、デバッガーは既に実行している場合 **.symopt + 0x80000000**または **! sym ノイズの多い**デバッガー拡張機能コマンド。
-   デバッガーが、読み込まれたモジュールのシンボルの検索をするを防ぐためにアクティブ化**SYMOPT\_いいえ\_UNQUALIFIED\_読み込み**を使用して、 **- snul**コマンドラインオプションを使用して、デバッガーは既に実行している場合や、 **.symopt + 0x100**します。
-   デバッグ セッションを必要とするモジュールを明示的に読み込む場合などのデバッガー コマンドを使用して **.reload**または **%ld**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WDK と WinDbg のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=733614)

[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063.aspx)

 

 






