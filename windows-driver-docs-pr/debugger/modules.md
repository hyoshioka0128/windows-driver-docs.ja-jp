---
title: モジュール
description: モジュール
ms.assetid: 0cd99869-4014-4f9f-b5f1-d06c69fd134e
keywords:
- モジュールのシンボル
- モジュール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07765e1cba145cd40b1ff2ec39c3fe303ec27d59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361503"
---
# <a name="modules"></a>モジュール


## <span id="modules"></span><span id="MODULES"></span>


*イメージ*実行可能ファイル、DLL、またはユーザー モード プロセスまたはカーネルの一部として Windows が読み込まれているドライバーです。 イメージの読み込み元のファイルと呼びますその*イメージ ファイル*します。

[デバッガー エンジン](introduction.md#debugger-engine)の一覧をキャッシュ*モジュール*プロセスごとに (または、カーネル モードの仮想プロセスで)。 通常このリスト内の各モジュールは、プロセスの画像を表します。 使用して、ターゲットとエンジンのモジュールの一覧を同期できます**再読み込み**します。

**注**  カーネル モードのデバッグで、仮想プロセス エンジンのモジュールの一覧には、システム全体のカーネル モードのモジュールと現在のプロセスのユーザー モードのモジュールの両方が含まれています。

 

モジュールの一覧で、インデックスを使用して、エンジンは、ターゲットの保持またはのターゲットの仮想アドレス空間では、そのベース アドレスでモジュールを指定できます。 モジュールのインデックスには、モジュールの一覧内の位置と等しいし、下限のインデックスを持つモジュールが読み込まれた場合にこのインデックスがそのため変更します。 すべての読み込まれたモジュールがあるインデックス。これらは、読み込まれたモジュールのインデックスよりも高いは常にです。 モジュールのベース アドレスは、それが読み込まれた; 限り変更されません。場合によっては、モジュールがアンロードおよび再読み込みし、時に変更可能性があります。

インデックスが 0 から 1 を引いたターゲット内のモジュールの数までの数です。 現在のプロセスでモジュールの数を呼び出すことによって見つかります[ **GetNumberModules**](https://msdn.microsoft.com/library/windows/hardware/ff547927)します。

呼び出すことによって、ベース アドレスを検索するインデックスを使用できる[ **GetModuleByIndex**](https://msdn.microsoft.com/library/windows/hardware/ff547080)します。 使用して指定された名前のシンボルを所有しているモジュールのベース アドレスを検出できる[ **GetSymbolModule**](https://msdn.microsoft.com/library/windows/hardware/ff549112)します。

次のメソッドには、インデックスと、指定したモジュールのベース アドレスの両方が返されます。

-   指定したモジュールの名前のモジュールを検索する使用[ **GetModuleByModuleName**](https://msdn.microsoft.com/library/windows/hardware/ff547095)します。

-   仮想アドレスの範囲内には、指定されたアドレスが含まれています。 モジュールは、によって返される[ **GetModuleByOffset**](https://msdn.microsoft.com/library/windows/hardware/ff547132)します。 このメソッドは、モジュールのベース アドレスを指定されたモジュールのインデックスの検索に使用できます。

次のメソッドには、インデックスまたはベース アドレスのいずれかを指定されたモジュールに関する情報が返されます。

-   モジュールの名前がによって返される[ **GetModuleNames** ](https://msdn.microsoft.com/library/windows/hardware/ff547146)と[ **GetModuleNameString**](https://msdn.microsoft.com/library/windows/hardware/ff547149)します。

-   モジュールのバージョン情報がによって返される[ **GetModuleVersionInformation**](https://msdn.microsoft.com/library/windows/hardware/ff547170)します。

-   によって返されるモジュールの記述に使用されるパラメーターの一部[ **GetModuleParameters**](https://msdn.microsoft.com/library/windows/hardware/ff547161)します。 このメソッドによって返されるパラメーターの詳細については、「 [**デバッグ\_モジュール\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff541514)します。

### <a name="span-idunloadedmodulesspanspan-idunloadedmodulesspanunloaded-modules"></a><span id="unloaded_modules"></span><span id="UNLOADED_MODULES"></span>モジュールのアンロード

ユーザー モードのデバッグは、中にアンロードされたモジュールは、Windows Server 2003 と Windows の以降のバージョンでのみ追跡されます。 Windows の以前のバージョンは、カーネル モードで読み込まれたモジュールのみを追跡します。 追跡時に読み込まれたモジュールの後にインデックスします。 そのため、読み込まれたすべてのモジュールとし、アンロードされたモジュールのターゲットのモジュールを検索するメソッドが検索されます。 によってアンロードされたコードを呼び出そうとすると発生したエラーを分析する読み込まれたモジュールを使用できます。

### <a name="span-idsyntheticmodulesspanspan-idsyntheticmodulesspan-synthetic-modules"></a><span id="synthetic_modules"></span><span id="SYNTHETIC_MODULES"></span> 統合モジュール

*合成モジュール*メモリの領域にラベルを付ける方法として作成できます。 これらのモジュールは、実際の記号を含めることはできませんが、合成のシンボルを含めることができます。 メソッド[ **AddSyntheticModule** ](https://msdn.microsoft.com/library/windows/hardware/ff537937)新しい統合モジュールを作成します。 統合モジュールを使用して削除できる[ **RemoveSyntheticModule**](https://msdn.microsoft.com/library/windows/hardware/ff554536)します。 ターゲット内のすべてのモジュールを再読み込みには、すべての合成モジュールが削除されます。

### <a name="span-idimagepathspanspan-idimagepathspanimage-path"></a><span id="image_path"></span><span id="IMAGE_PATH"></span>イメージのパス

*実行可能イメージ パス*実行可能イメージを検索するときに、エンジンによって使用されます。

実行可能イメージのパスは、セミコロンで区切られた複数のディレクトリで構成できます (**;**)。 順序でこれらのディレクトリが検索されます。

実行可能イメージ パスの概要については、実行可能イメージのパスを参照してください。

実行可能イメージのパスにディレクトリを追加するには、メソッドを使用して[ **AppendImagePath**](https://msdn.microsoft.com/library/windows/hardware/ff538092)します。 によって、まったく実行可能イメージのパスが返される[ **GetImagePath** ](https://msdn.microsoft.com/library/windows/hardware/ff546851)を使用して変更できる[ **SetImagePath**](https://msdn.microsoft.com/library/windows/hardware/ff556708)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスと仮想プロセスの詳細については、次を参照してください。[スレッドとプロセス](controlling-threads-and-processes.md)します。

 

 





