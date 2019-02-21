---
title: PDBCopy を使用します。
description: PDBCopy を使用します。
ms.assetid: f8207b09-5a1b-4ff3-b99d-20daa88cfe10
keywords:
- PDBCopy を使用して
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f5d61816aa99cb20dd7c91db0f2ca4ba266b12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531378"
---
# <a name="using-pdbcopy"></a>PDBCopy を使用します。


PDBCopy は、完全なシンボル ファイルから削除されたシンボル ファイルを作成するコマンド ライン ツールです。 つまり、プライベート シンボル データと、パブリック シンボル テーブルの両方が含まれていて、パブリック シンボル テーブルのみを含むファイルのコピーが作成されるシンボル ファイルがかかります。 PDBCopy オプションの使用によって削除されたシンボル ファイルには、全体のパブリック シンボルの表に、またはパブリック シンボル テーブルの指定したサブセットのいずれかが含まれています。

PDB 形式シンボル ファイル (ファイル名拡張子 .pdb) と連携 PDBCopy は古い形式 (.dbg) シンボル ファイル使用できません。

パブリック シンボル テーブルとプライベート シンボル データの説明は、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

### <a name="span-idremovingprivatesymbolsspanspan-idremovingprivatesymbolsspanremoving-private-symbols"></a><span id="removing_private_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS"></span>プライベート シンボルの削除

含む、すべてのパブリック シンボルとプライベート シンボルの削除されたシンボル ファイルを作成する場合は、3 つのパラメーターで PDBCopy を使用します。 ファイル、パスと、新しいシンボル ファイルとは、-p オプションの名前のシンボル パスと、元の名前。

たとえば、次のコマンドは、mysymbols.pdb と同じパブリック シンボル テーブルが含まれていますが、プライベート シンボル データの含まれていませんが、publicsymbols.pdb という名前の新しいファイルを作成します。

**pdbcopy mysymbols.pdb publicsymbols.pdb -p**

Mysymbols.pdb が既に削除されたシンボル ファイルである場合、新しいファイルと、古いファイルのシンボリック コンテンツが同じになります。

このコマンドを実行した後は必要があります、新しいファイルを新しい場所に移動し、シンボル ファイルの元の名前に変更します (この例で mysymbols.pdb) ほとんどのデバッグ プログラムとシンボルの展開プログラムが特定のファイルに基づくシンボルを検索するため、名前。 または、別のディレクトリが指定されている限り、入力ファイルと PDBCopy コマンドラインに出力ファイルの同じファイル名を使用できます。

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir2\\mysymbols.pdb -p**

**注**  PDBCopy の実行前に、コピー先ファイルが存在しない必要があります。 この名前のファイルが存在する場合は、さまざまなエラーが発生します。

 

### <a name="span-idremovingprivatesymbolsandselectedpublicsymbolsspanspan-idremovingprivatesymbolsandselectedpublicsymbolsspanremoving-private-symbols-and-selected-public-symbols"></a><span id="removing_private_symbols_and_selected_public_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS_AND_SELECTED_PUBLIC_SYMBOLS"></span>削除するプライベート シンボルし、パブリック シンボルを選択

だけでなく、プライベート シンボル データを削除もパブリック シンボルの表の情報の量を削減する場合は、削除するにはパブリック シンボルの一覧を指定する-f オプションを使用できます。

次の例は、この手順を示しています。

1.  削除するシンボルの装飾を含め、完全な名前を決定します。 シンボルの装飾名の確信できない場合は使用できます、 [DBH](dbh.md)それらを判断するためのツール。 詳細については、特定の記号の文字装飾を決定するを参照してください。 この例でお知らせがあるとすることを削除するシンボルの装飾名 **\_myGlobal1**と **\_myGlobal2**します。

2.  削除するシンボルの一覧を含むテキスト ファイルを作成します。 このファイル内の各行には、装飾を含みますが、モジュール名を含まない 1 つのシンボルの名前を含める必要があります。 この例で、ファイルには次の 2 つの行が含まれます。

    ```text
    _myGlobal1
    _myGlobal2 
    ```

    ファイルには、選択した任意の名前を指定できます。 このファイル listfile.txt という名前をし、c: ディレクトリ内に配置したことをお知らせと\\Temp します。

3.  次の PDBCopy コマンドラインを使用します。

    ```console
    pdbcopy OldPDB NewPDB-p -f:@TextFile 
    ```

    場所*OldPDB*と*NewPDB*は元のシンボル ファイルと、新しいシンボル ファイルおよび*TextFile*は 2 つの手順で作成したファイルです。 特定のパブリック シンボルが、削除するには、(マーク @)、アンパサンドは、指定したテキスト ファイルで、これらのシンボルが表示されていることを示すことを-f オプションを示します。

    現在の例では、コマンドは次のようになります。

    ```console
    pdbcopy c:\dir1\mysymbols.pdb c:\dir3\mysymbols.pdb -p -f:@c:\temp\listfile.txt 
    ```

    新しいシンボル ファイルでは、c: が作成されます\\ディレクトリ 2\\mysymbols.pdb、任意のプライベート シンボルが含まれていないあり listfile.txt で表示されている 2 つのグローバル変数が含まれていません。

この例に示すように、PDBCopy の-f オプションは、特定のパブリック シンボルの一覧を削除します。 (マーク @)、アンパサンドは、テキスト ファイルで、これらのシンボルが表示されていることを示します。 別の方法では、アンパサンドせず-f オプションを使用して、コマンドラインですべてのシンボルを一覧表示します。 したがって、次のコマンドラインは、上記の手順の例と同等です。

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir3\\mysymbols.pdb -p -f:\_myGlobal1 -f:\_myGlobal2**

1 つまたは 2 つのシンボルを削除するには、しない限りにコマンドラインでそれらを一覧するよりもテキスト ファイルを使用するが簡単です。

.Pdb ファイルからほとんどのパブリック シンボルを削除する場合は、-f オプションは、最も簡単な方法です。 -F オプションを削除するこれらのパブリック シンボルを一覧表示する必要があります、-f オプションでは、これらのパブリック シンボルを削除したくないを一覧表示する必要があります。 その他のすべてのパブリック シンボル (およびそのすべてのプライベート シンボル) は削除されます。 -F オプション-f オプションと同じ 2 つの構文オプションをサポートしています: F が後にシンボルの名前を保持するまたは @ f: のいずれかの後に保持するシンボルの一覧を含むテキスト ファイルの名前。 どちらの場合は、シンボル名を使用する必要がありますを装飾します。

次のコマンドがすべてプライベート シンボルとシンボルのみを残して、ほぼすべてのパブリック シンボルを削除するなど、  **\_myFunction5**と **\_myGlobal7**:

**pdbcopy c:\\dir1\\mysymbols.pdb c:\\dir3\\mysymbols.pdb -p -F:\_myFunction5 -F:\_myGlobal7**

1 行で-f オプションの複数のインスタンスを結合する場合は、指定したすべてのシンボルが削除されます。 1 行で-f オプションの複数のインスタンスを結合する場合は、指定したすべてのシンボルが保持される場合およびその他のすべてのシンボルが削除されます。 -F で-f を組み合わせることはできません。

プライベート シンボルのすべてのデータが削除され-p オプションを指定せず、-f および-f オプションを使用できません。 元のファイルにプライベート シンボルが含まれていない場合でも (ただし、影響を与えませんこの場合) は、-p オプションを含める必要があります。

プライベート シンボル データが削除されないようにするのには、-f オプションを使用できません。 パブリック シンボル テーブルに含まれていないシンボルでこのオプションを使用する場合は、PDBCopy 無視します。

### <a name="span-idthemspdbdllfilespanspan-idthemspdbdllfilespanthe-mspdbdll-file"></a><span id="the_mspdb__dll_file"></span><span id="THE_MSPDB__DLL_FILE"></span>Mspdb\*.dll ファイル

PDBCopy では、Mspdb80.dll ファイルまたは Mspdb60.dll ファイルのいずれかを実行するためにアクセスする必要があります。 既定では、PDBCopy は、Visual Studio .NET 2002 および Visual Studio の以降のバージョンで使用されるバージョンである Mspdb80.dll で使用します。 指定できるかどうか、Visual Studio 6.0 または以前のバージョンを使用して、シンボルが作成されたは、vc6 コマンド ライン オプションためその PDBCopy を使用して Mspdb60.dll 代わりに、これは必要ありませんの。 PDBCopy があっても、適切なファイルを探し、vc6 オプションは使用されません。 Visual Studio、Platform SDK、または Windows Driver Kit (WDK) のインストール内では、これらのファイルを検索できます。

PDBCopy を実行する前に必ず正しいバージョンの mspdb\*の .dll ファイルは、コンピューターにアクセスとその場所がコマンドのパスの一部であることを確認します。 使用する必要がありますがない場合、**パス**コマンド パスにこの場所を追加するコマンド。

### <a name="span-idthefilesignatureandthesymsrvindexspanspan-idthefilesignatureandthesymsrvindexspanthe-file-signature-and-the-symsrv-index"></a><span id="the_file_signature_and_the_symsrv_index"></span><span id="THE_FILE_SIGNATURE_AND_THE_SYMSRV_INDEX"></span>ファイルの署名と SymSrv インデックス

各シンボル ファイルには、一意に識別されている固定の署名があります。 SymSrv では、署名を使用して、一意「インデックス値を」ファイルを生成します。 2 つのファイルには、さまざまな内容または別の作成時間がある、個別の署名と個別の SymSrv インデックス値があります。

PDBCopy で作成したファイルには、ルールの一意のインデックス値の例外です。 PDBCopy では、新しいシンボル ファイルを作成するとき、古いファイルとして、SymSrv のインデックス値と同じシグネチャがあります。 この機能は、シンボルに関連するツールの動作を変更することがなく、他の置き換えられる 1 つのファイルを使用できます。

新しいファイルを個別の署名と SymSrv インデックスがある場合は、-s オプションを使用します。 ほとんどの場合 PDBCopy の最も一般的な用途は、不一致を発生させることがなく、古いファイルを置き換えることができる変更のシンボル ファイルを作成するために、このオプションを使用するはありません。 新しい署名に新しいファイルが古いものを正しく交換するを防ぐ、古いファイルより新しいファイルに別のインデックス値を代入する SymSrv があります。

完全なコマンドラインの構文を参照してください。 [ **PDBCopy コマンド ライン オプション**](pdbcopy-command-line-options.md)します。

 

 





