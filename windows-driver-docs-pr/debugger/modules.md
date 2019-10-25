---
title: モジュール
description: モジュール
ms.assetid: 0cd99869-4014-4f9f-b5f1-d06c69fd134e
keywords:
- シンボル、モジュール
- モジュール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e1f8e0597ddfe35caccfcc41f569c17c05ce899
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834335"
---
# <a name="modules"></a>モジュール


## <span id="modules"></span><span id="MODULES"></span>


*イメージ*は、Windows によってユーザーモードプロセスまたはカーネルの一部として読み込まれた実行可能ファイル、DLL、またはドライバーです。 イメージの読み込み元のファイルは、*イメージファイル*と呼ばれます。

[デバッガーエンジン](introduction.md#debugger-engine)は、各プロセス (または、カーネルモードでは仮想プロセス) の*モジュール*の一覧をキャッシュします。 通常、この一覧の各モジュールは、プロセス内のイメージを表します。 エンジンのモジュールリストは、 **Reload**を使用してターゲットと同期できます。

**注**   カーネルモードのデバッグでは、仮想プロセスのエンジンのモジュール一覧に、システム全体のカーネルモードモジュールと現在のプロセスのユーザーモードモジュールの両方が含まれています。

 

モジュールは、ターゲットの仮想アドレス空間内のベースアドレス、またはエンジンがターゲット用に保持しているモジュールの一覧のインデックスによって指定できます。 モジュールのインデックスは、モジュールのリスト内の位置と同じであるため、インデックス番号が小さいモジュールがアンロードされると、このインデックスが変更されます。 アンロードされたすべてのモジュールにインデックスがあります。これらは、読み込まれたモジュールのインデックスよりも常に高くなります。 モジュールのベースアドレスは、読み込まれている間は変更されません。場合によっては、モジュールがアンロードされた後に再読み込みされると変更されることがあります。

インデックスは、0からターゲットのモジュール数から1を引いた数までの数値です。 現在のプロセス内のモジュールの数は、 [**Getnumber モジュール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnumbermodules)を呼び出すことによって確認できます。

[**GetModuleByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyindex)を呼び出すことにより、インデックスを使用してベースアドレスを検索できます。 指定された名前を持つシンボルを所有するモジュールのベースアドレスは、 [**Getsymbol モジュール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolmodule)を使用して見つけることができます。

次のメソッドは、指定されたモジュールのインデックスとベースアドレスの両方を返します。

-   モジュール名を指定してモジュールを検索するには、 [**GetModuleByModuleName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebymodulename)を使用します。

-   指定されたアドレスを含む仮想アドレス範囲を持つモジュールは、 [**GetModuleByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyoffset)によって返されます。 このメソッドを使用すると、モジュールのベースアドレスが指定されているモジュールインデックスを見つけることができます。

次のメソッドは、ベースアドレスまたはインデックスによって指定されたモジュールに関する情報を返します。

-   モジュールの名前は、 [**Getmodulenames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenames)および[**GetModuleNameString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenamestring)によって返されます。

-   モジュールのバージョン情報は、 [**GetModuleVersionInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleversioninformation)によって返されます。

-   モジュールを記述するために使用されるパラメーターの一部は、 [**GetModuleParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleparameters)によって返されます。 このメソッドによって返されるパラメーターの詳細については、「 [**DEBUG\_MODULE\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_module_parameters)」を参照してください。

### <a name="span-idunloaded_modulesspanspan-idunloaded_modulesspanunloaded-modules"></a><span id="unloaded_modules"></span><span id="UNLOADED_MODULES"></span>アンロードされたモジュール

ユーザーモードのデバッグ中、アンロードしたモジュールは Windows Server 2003 以降のバージョンの Windows でのみ追跡されます。 以前のバージョンの Windows では、カーネルモードでアンロードされたモジュールのみを追跡していました。 追跡されると、読み込まれたモジュールの後にインデックスが作成されます。 したがって、ターゲットのモジュールを検索するすべてのメソッドは、読み込まれたすべてのモジュールを検索し、アンロードされたモジュールを検索します。 アンロードされたモジュールを使用して、アンロードされたコードを呼び出そうとしたことによって発生したエラーを分析できます。

### <a name="span-idsynthetic_modulesspanspan-idsynthetic_modulesspan-synthetic-modules"></a><span id="synthetic_modules"></span><span id="SYNTHETIC_MODULES"></span>合成モジュール

*合成モジュール*は、メモリ領域にラベルを付ける方法として作成できます。 これらのモジュールに実際のシンボルを含めることはできませんが、合成シンボルを含めることができます。 メソッド[**Addsyntheのモジュール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticmodule)は、新しい合成モジュールを作成します。 合成モジュールは、 [**RemoveSyntheticModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticmodule)を使用して削除できます。 ターゲット内のすべてのモジュールを再読み込みすると、すべての統合モジュールが削除されます。

### <a name="span-idimage_pathspanspan-idimage_pathspanimage-path"></a><span id="image_path"></span><span id="IMAGE_PATH"></span>イメージパス

実行可能*イメージのパス*は、実行可能イメージの検索時にエンジンによって使用されます。

実行可能イメージのパスは、セミコロン ( **;** ) で区切られた複数のディレクトリで構成されます。 これらのディレクトリは順番に検索されます。

実行可能イメージパスの概要については、「実行可能イメージのパス」を参照してください。

実行可能イメージパスにディレクトリを追加するには、 [**AppendImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendimagepath)メソッドを使用します。 実行可能なイメージのパス全体は[**GetImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getimagepath)によって返され、 [**SetImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setimagepath)を使用して変更できます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスと仮想プロセスの詳細については、「[スレッドとプロセス](controlling-threads-and-processes.md)」を参照してください。

 

 





