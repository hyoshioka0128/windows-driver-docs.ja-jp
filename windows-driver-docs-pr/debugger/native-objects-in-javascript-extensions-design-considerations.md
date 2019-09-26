---
title: JavaScript 拡張機能のネイティブデバッガーオブジェクト-設計とテストに関する考慮事項
description: ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構成要素を表します。 このトピックでは、JavaScript 拡張機能でのネイティブデバッガーオブジェクトの設計とテストに関する考慮事項について説明します。
ms.assetid: A8E12564-D083-43A7-920E-22C4D627FEEA
ms.date: 09/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 579efb8f4b693b9c4c42437896eef5edbf3cc368
ms.sourcegitcommit: 3b7c8b3cb59031e0f4e39dac106c1598ad108828
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70935899"
---
# <a name="native-debugger-objects-in-javascript-extensions---design-and-testing-considerations"></a>JavaScript 拡張機能のネイティブデバッガーオブジェクト-設計とテストに関する考慮事項

このトピックでは、JavaScript 拡張機能でネイティブデバッガーオブジェクトを使用するための設計とテストの考慮事項について説明します。

ネイティブデバッガーオブジェクトは、デバッガー環境のさまざまな構造と動作を表します。 オブジェクトは、デバッガーの状態を操作するために (またはで取得した) JavaScript 拡張機能に渡すことができます。

デバッガーオブジェクトの JavaScript 拡張機能の詳細については、「 [Javascript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)」を参照してください。

JavaScript の使用に関する一般的な情報については、「 [Javascript デバッガースクリプト](javascript-debugger-scripting.md)」を参照してください。

## <a name="span-iddesign-considerationsspanspan-iddesign-considerationsspanspan-iddesign-considerationsspandebugger-data-model-design-considerations"></a><span id="Design-Considerations"></span><span id="design-considerations"></span><span id="DESIGN-CONSIDERATIONS"></span>デバッガーデータモデルの設計に関する考慮事項

**設計原則**

次の原則を考慮して、検出可能、クエリ可能、およびスクリプト可能な情報をデバッガー拡張機能に提供します。

-   情報は、必要な場所の近くにあります。 たとえば、レジストリキーの情報は、レジストリキーハンドルを含むローカル変数の一部として表示される必要があります。
-   情報は構造化されています。 たとえば、レジストリキーに関する情報は、キーの種類、キー ACL、キー名、値などの別のフィールドに表示されます。 これは、テキストを解析せずに個々のフィールドにアクセスできることを意味します。
-   情報は一貫しています。 レジストリキーのハンドルに関する情報は、ファイルハンドルに関する情報と同様の方法で表示されます。

これらの原則をサポートしていないこれらのアプローチは避けてください。

-   1つのフラットな "キッチンシンク" に項目を構築しないでください。 整理された階層を使用すると、ユーザーが探している情報を参照したり、見つけやすさをサポートしたりすることができます。
-   従来の dbgeng 拡張機能を変換するには、そのままモデルに移動するだけで、生のテキストの画面を出力します。 これは他の拡張機能と共にコンポーザブルではなく、LINQ 式を使用してクエリを行うことはできません。 代わりに、複数のクエリ可能フィールドにデータを分割します。

**名前付けのガイドライン**

-   フィールドの大文字と小文字は区別して使用する必要があります。 別の文字種で広く知られている名前 (jQuery など) については、例外を考慮することができます。
-   C++識別子では通常使用されない特殊文字を使用しないようにしてください。 たとえば、"Total Length" (スペースを含む)、または "\[size\]" (角かっこを含む) などの名前を使用しないようにします。 この規則により、これらの文字が識別子の一部として許可されていないスクリプト言語の使用が簡単になります。また、コマンドウィンドウの使用も簡単になります。

**組織と階層のガイドライン**

-   デバッガーの名前空間の最上位レベルを拡張しないでください。 代わりに、最も関連性の高い場所に情報が表示されるように、デバッガー内の既存のノードを拡張する必要があります。
-   概念を複製しないでください。 デバッガーに既に存在する概念に関する追加情報を一覧表示するデータモデル拡張機能を作成する場合は、新しい情報で置き換えるのではなく、既存の情報を拡張してください。 つまり、モジュールに関する詳細を表示する拡張機能は、モジュールの新しいリストを作成するのではなく、既存の*モジュール*オブジェクトを拡張する必要があります。
-   無料のフローティングユーティリティコマンドは、 *Debugger*名前空間の一部である必要があります。 また、これらのサブコレクションは、(例: *FromListEntry*) のように、適切なものにする必要があります。

**下位互換性と重大な変更**

パブリッシュされたスクリプトは、そのスクリプトに依存している他のスクリプトとの互換性を損なうことはありません。 たとえば、関数がモデルにパブリッシュされた場合は、可能な限り同じ場所に保持され、同じパラメーターを持つ必要があります。

**外部リソースを使用しない**

-   拡張機能は外部プロセスを生成しません。 外部プロセスは、デバッガーの動作に干渉する可能性があります。また、さまざまなリモートデバッガーのシナリオ (たとえば、dbgsrv リモート、ntsd リモート、"ntsd-d リモート") に不適切な動作ます。
-   拡張機能では、ユーザーインターフェイスを表示することはできません。 リモートデバッグのシナリオでは、ユーザーインターフェイス要素の表示が正しく動作しないため、コンソールのデバッグシナリオが中断される可能性があります。
-   拡張機能は、ドキュメント化されていないメソッドを使用してデバッガーエンジンまたはデバッガー UI を操作することはできません これにより、互換性の問題が発生し、UI が異なるデバッガークライアントで正しく動作しなくなります。
-   拡張機能は、ドキュメント化されたデバッガー Api を介してのみ、ターゲット情報にアクセスする必要があります。 Win32 Api を使用してターゲットに関する情報にアクセスしようとすると、多くのリモートシナリオでは失敗し、セキュリティ境界を越えたローカルデバッグシナリオもあります。

**Dbgeng 固有の機能を使用しない**

拡張機能として使用することを意図したスクリプトは、可能な限り dbgeng 固有の機能に依存しないようにする必要があります ("クラシック" デバッガー拡張機能の実行など)。 スクリプトは、データモデルをホストする任意のデバッガー上で使用できる必要があります。

## <a name="span-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspanspan-idtesting-debugger-extensionsspantesting-debugger-extensions"></a><span id="Testing-Debugger-Extensions"></span><span id="testing-debugger-extensions"></span><span id="TESTING-DEBUGGER-EXTENSIONS"></span>デバッガー拡張機能のテスト


拡張機能は、さまざまなシナリオで動作します。 一部の拡張機能はシナリオ (カーネルデバッグシナリオなど) に固有である場合がありますが、ほとんどの拡張機能はすべてのシナリオで動作するか、サポートされているシナリオを示すメタデータを持つ必要があります。

カーネルモード

-   ライブカーネルデバッグ
-   カーネルダンプのデバッグ

ユーザーモード

-   ライブユーザーモードのデバッグ
-   ユーザーモードのダンプデバッグ

また、これらのデバッガーの使用シナリオを検討してください。

-   マルチプロセスデバッグ
-   マルチセッションデバッグ (たとえば、1つのセッション内のダンプとライブユーザー)

**リモートデバッガーの使用**

リモートデバッガーの使用シナリオで適切な操作をテストします。

-   dbgsrv リモート
-   ntsd リモート
-   ntsd-d リモート

詳細については、「 [CDB と NTSD を使用](debugging-using-cdb-and-ntsd.md)したデバッグ」と「[**プロセスサーバーのアクティブ化**](activating-a-process-server.md)」を参照してください。

**回帰テスト**

新しいバージョンのデバッガーがリリースされると、拡張機能の機能を確認できるテスト自動化の使用を調査します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[JavaScript 拡張機能のネイティブデバッガーオブジェクト](native-objects-in-javascript-extensions.md)

 [JavaScript 拡張機能のネイティブデバッガーオブジェクト-デバッガーオブジェクトの詳細](native-objects-in-javascript-extensions-debugger-objects.md)。

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)

 

 





