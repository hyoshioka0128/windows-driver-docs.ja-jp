---
title: モジュール
description: モジュール
ms.assetid: 0cd99869-4014-4f9f-b5f1-d06c69fd134e
keywords:
- モジュールのシンボル
- モジュール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c602a64f1c1c5434a47def32efddebc6f5a7b87f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366467"
---
# <a name="modules"></a>モジュール


## <span id="modules"></span><span id="MODULES"></span>


*イメージ*実行可能ファイル、DLL、またはユーザー モード プロセスまたはカーネルの一部として Windows が読み込まれているドライバーです。 イメージの読み込み元のファイルと呼びますその*イメージ ファイル*します。

[デバッガー エンジン](introduction.md#debugger-engine)の一覧をキャッシュ*モジュール*プロセスごとに (または、カーネル モードの仮想プロセスで)。 通常このリスト内の各モジュールは、プロセスの画像を表します。 使用して、ターゲットとエンジンのモジュールの一覧を同期できます**再読み込み**します。

**注**  カーネル モードのデバッグで、仮想プロセス エンジンのモジュールの一覧には、システム全体のカーネル モードのモジュールと現在のプロセスのユーザー モードのモジュールの両方が含まれています。

 

モジュールの一覧で、インデックスを使用して、エンジンは、ターゲットの保持またはのターゲットの仮想アドレス空間では、そのベース アドレスでモジュールを指定できます。 モジュールのインデックスには、モジュールの一覧内の位置と等しいし、下限のインデックスを持つモジュールが読み込まれた場合にこのインデックスがそのため変更します。 すべての読み込まれたモジュールがあるインデックス。これらは、読み込まれたモジュールのインデックスよりも高いは常にです。 モジュールのベース アドレスは、それが読み込まれた; 限り変更されません。場合によっては、モジュールがアンロードおよび再読み込みし、時に変更可能性があります。

インデックスが 0 から 1 を引いたターゲット内のモジュールの数までの数です。 現在のプロセスでモジュールの数を呼び出すことによって見つかります[ **GetNumberModules**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getnumbermodules)します。

呼び出すことによって、ベース アドレスを検索するインデックスを使用できる[ **GetModuleByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyindex)します。 使用して指定された名前のシンボルを所有しているモジュールのベース アドレスを検出できる[ **GetSymbolModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolmodule)します。

次のメソッドには、インデックスと、指定したモジュールのベース アドレスの両方が返されます。

-   指定したモジュールの名前のモジュールを検索する使用[ **GetModuleByModuleName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebymodulename)します。

-   仮想アドレスの範囲内には、指定されたアドレスが含まれています。 モジュールは、によって返される[ **GetModuleByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyoffset)します。 このメソッドは、モジュールのベース アドレスを指定されたモジュールのインデックスの検索に使用できます。

次のメソッドには、インデックスまたはベース アドレスのいずれかを指定されたモジュールに関する情報が返されます。

-   モジュールの名前がによって返される[ **GetModuleNames** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenames)と[ **GetModuleNameString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenamestring)します。

-   モジュールのバージョン情報がによって返される[ **GetModuleVersionInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleversioninformation)します。

-   によって返されるモジュールの記述に使用されるパラメーターの一部[ **GetModuleParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleparameters)します。 このメソッドによって返されるパラメーターの詳細については、「 [**デバッグ\_モジュール\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_module_parameters)します。

### <a name="span-idunloadedmodulesspanspan-idunloadedmodulesspanunloaded-modules"></a><span id="unloaded_modules"></span><span id="UNLOADED_MODULES"></span>モジュールのアンロード

ユーザー モードのデバッグは、中にアンロードされたモジュールは、Windows Server 2003 と Windows の以降のバージョンでのみ追跡されます。 Windows の以前のバージョンは、カーネル モードで読み込まれたモジュールのみを追跡します。 追跡時に読み込まれたモジュールの後にインデックスします。 そのため、読み込まれたすべてのモジュールとし、アンロードされたモジュールのターゲットのモジュールを検索するメソッドが検索されます。 によってアンロードされたコードを呼び出そうとすると発生したエラーを分析する読み込まれたモジュールを使用できます。

### <a name="span-idsyntheticmodulesspanspan-idsyntheticmodulesspan-synthetic-modules"></a><span id="synthetic_modules"></span><span id="SYNTHETIC_MODULES"></span> 統合モジュール

*合成モジュール*メモリの領域にラベルを付ける方法として作成できます。 これらのモジュールは、実際の記号を含めることはできませんが、合成のシンボルを含めることができます。 メソッド[ **AddSyntheticModule** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticmodule)新しい統合モジュールを作成します。 統合モジュールを使用して削除できる[ **RemoveSyntheticModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticmodule)します。 ターゲット内のすべてのモジュールを再読み込みには、すべての合成モジュールが削除されます。

### <a name="span-idimagepathspanspan-idimagepathspanimage-path"></a><span id="image_path"></span><span id="IMAGE_PATH"></span>イメージのパス

*実行可能イメージ パス*実行可能イメージを検索するときに、エンジンによって使用されます。

実行可能イメージのパスは、セミコロンで区切られた複数のディレクトリで構成できます ( **;** )。 順序でこれらのディレクトリが検索されます。

実行可能イメージ パスの概要については、実行可能イメージのパスを参照してください。

実行可能イメージのパスにディレクトリを追加するには、メソッドを使用して[ **AppendImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-appendimagepath)します。 によって、まったく実行可能イメージのパスが返される[ **GetImagePath** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getimagepath)を使用して変更できる[ **SetImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setimagepath)します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスと仮想プロセスの詳細については、次を参照してください。[スレッドとプロセス](controlling-threads-and-processes.md)します。

 

 





