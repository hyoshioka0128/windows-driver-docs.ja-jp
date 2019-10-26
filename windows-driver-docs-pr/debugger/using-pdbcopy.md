---
title: PDBCopy の使用
description: PDBCopy の使用
ms.assetid: f8207b09-5a1b-4ff3-b99d-20daa88cfe10
keywords:
- PDBCopy、使用
ms.date: 10/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: ddb03513eae658b54a6d41582b1ebc74db59c559
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916113"
---
# <a name="using-pdbcopy"></a>PDBCopy の使用

PDBCopy は、完全なシンボルファイルから削除されたシンボルファイルを作成するコマンドラインツールです。 つまり、プライベートシンボルデータとパブリックシンボルテーブルの両方を含むシンボルファイルを受け取り、そのファイルのコピーを作成します。このファイルには、パブリックシンボルテーブルだけが含まれています。 使用する PDBCopy オプションに応じて、削除されたシンボルファイルには、パブリックシンボルテーブル全体またはパブリックシンボルテーブルの指定したサブセットのいずれかが含まれます。

WDK の PDBCopy の場所については、「 [Windows 用デバッグツールに含まれるツール](extra-tools.md#installation-directory)の**インストールディレクトリ**」を参照してください。

PDBCopy は、(ファイル名拡張子 .pdb を持つ) 任意の PDB 形式のシンボルファイルで動作しますが、古い形式 (dbg) のシンボルファイルは使用できません。

パブリックシンボルテーブルとプライベートシンボルデータの説明については、「[パブリックシンボルとプライベート](public-and-private-symbols.md)シンボル」を参照してください。

### <a name="span-idremoving_private_symbolsspanspan-idremoving_private_symbolsspanremoving-private-symbols"></a><span id="removing_private_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS"></span>プライベートシンボルの削除

すべてのパブリックシンボルを含み、プライベートシンボルを含まない、削除されたシンボルファイルを作成する場合は、3つのパラメーター (元のシンボルファイルのパスと名前、新しいシンボルファイルのパスと名前、-p オプション) を指定して PDBCopy を使用します。

たとえば、次のコマンドは、publicsymbols という名前の新しいファイルを作成します。このファイルには、mysymbols と同じパブリックシンボルテーブルが含まれていますが、プライベートシンボルデータは含まれていません。

**pdbcopy mysymbols. .pdb-p**

Mysymbols .pdb が既に削除されたシンボルファイルである場合、新しいファイルのシンボリックコンテンツと古いファイルは同じになります。

このコマンドを発行した後、新しいファイルを新しい場所に移動して、シンボルファイルの元の名前 (この例では、mysymbols .pdb) に変更する必要があります。これは、ほとんどのデバッグプログラムおよびシンボル抽出プログラムは、特定のファイルに基づいてシンボルを検索するためです。指定. また、別のディレクトリが指定されている場合は、PDBCopy コマンドラインで入力ファイルと出力ファイルに同じファイル名を使用することもできます。

**pdbcopy c:\\dir1\\mysymbols. .pdb c:\\dir2\\mysymbols. .pdb-p**

PDBCopy を実行する前に、コピー先のファイルが存在してはならない**ことに注意**してください  。 この名前のファイルが存在する場合は、さまざまなエラーが発生する可能性があります。

### <a name="span-idremoving_private_symbols_and_selected_public_symbolsspanspan-idremoving_private_symbols_and_selected_public_symbolsspanremoving-private-symbols-and-selected-public-symbols"></a><span id="removing_private_symbols_and_selected_public_symbols"></span><span id="REMOVING_PRIVATE_SYMBOLS_AND_SELECTED_PUBLIC_SYMBOLS"></span>プライベートシンボルと選択されたパブリックシンボルの削除

プライベートシンボルデータを削除するだけでなく、パブリックシンボルテーブルの情報量を減らしたい場合は、-f オプションを使用して、削除するパブリックシンボルの一覧を指定できます。

次の例は、この手順を示しています。

1. 削除するシンボルの完全な名前 (装飾を含む) を決定します。 修飾されたシンボル名がわからない場合は、 [Dbh](dbh.md)ツールを使用してそれらを判別できます。 詳細については、「特定のシンボルの装飾を決定する」を参照してください。 この例では、削除するシンボルの装飾さ\_れた名前が**myGlobal1**で、 **\_myGlobal2**であるとします。

2. 削除するシンボルの一覧を含むテキストファイルを作成します。 このファイルの各行には、装飾を含む1つの記号の名前を含める必要がありますが、モジュール名は含めません。 この例では、ファイルに次の2つの行が含まれています。

    ```text
    _myGlobal1
    _myGlobal2
    ```

    ファイルには任意の名前を付けることができます。 このファイルに「listfile」という名前を指定し、ディレクトリ C:\\Temp に配置するとします。

3. 次の PDBCopy コマンドラインを使用します。

    ```console
    pdbcopy OldPDB NewPDB -p -f:@TextFile
    ```

    *Oldpdb*と*newpdb*は元のシンボルファイルと新しいシンボルファイルで、 *TextFile*は手順 2. で作成したファイルです。 -F オプションは、特定のパブリックシンボルが削除されることを示し、アンパサンド (@) は、これらのシンボルが指定されたテキストファイルに一覧表示されることを示します。

    現在の例では、コマンドは次のようになります。

    ```console
    pdbcopy c:\dir1\mysymbols.pdb c:\dir3\mysymbols.pdb -p -f:@c:\temp\listfile.txt
    ```

    これにより、新しいシンボルファイル C:\\dir3\\mysymbols .pdb が作成されます。このファイルにはプライベートシンボルが含まれておらず、listfile に一覧表示されている2つのグローバル変数が含まれていません。

この例に示すように、PDBCopy の-f オプションは、パブリックシンボルの特定のリストを削除します。 アンパサンド (@) は、これらのシンボルがテキストファイルに含まれていることを示します。 別の方法として、アンパサンドなしで-f オプションを使用して、コマンドライン上のすべてのシンボルを一覧表示することもできます。 したがって、次のコマンドラインは、上記の手順の例と同じです。

**pdbcopy c:\\dir1\\mysymbols. .pdb c:\\dir3\\mysymbols-p-f:\_myGlobal1-f:\_myGlobal2**

1つまたは2つのシンボルのみを削除する場合を除き、テキストファイルをコマンドラインに表示するよりも簡単に使用できます。

.Pdb ファイルから大部分のパブリックシンボルを削除する場合は、-F オプションが最も簡単な方法です。 -F オプションを使用すると、削除するパブリックシンボルを一覧表示する必要がありますが、-F オプションでは削除しないパブリックシンボルを一覧表示する必要があります。 その他のすべてのパブリックシンボル (およびすべてのプライベートシンボル) は削除されます。 -F オプションでは、-f オプションと同じ2つの構文オプションがサポートされています。-f: の後に保持するシンボルの名前、-F: @、保持するシンボルの一覧を含むテキストファイルの名前の順に指定します。 どちらの場合も、装飾されたシンボル名を使用する必要があります。

たとえば、次のコマンドを実行すると、すべてのプライベートシンボルとほとんどすべてのパブリックシンボルが削除され、シンボル **\_myFunction5**と **\_myGlobal7**だけが残ります。

**pdbcopy c:\\dir1\\mysymbols. .pdb c:\\dir3\\mysymbols-p-F:\_myFunction5-F:\_myGlobal7**

-F オプションの複数のインスタンスを1行に結合すると、指定したすべてのシンボルが削除されます。 -F オプションの複数のインスタンスを1行に結合すると、指定したすべてのシンボルが保持され、他のすべてのシンボルは削除されます。 -F と-F を組み合わせることはできません。

-F オプションと-F オプションは、-p オプションを指定せずに使用することはできません。これにより、すべてのプライベートシンボルデータが削除されます。 元のファイルにプライベートシンボルが含まれていない場合でも、-p オプションを含める必要があります (ただし、この場合は効果がありません)。

-F オプションを使用して、プライベートシンボルデータが削除されないようにすることはできません。 このオプションを、パブリックシンボルテーブルに含まれていないシンボルと共に使用すると、PDBCopy は無視されます。

### <a name="span-idthe_mspdb__dll_filespanspan-idthe_mspdb__dll_filespanthe-mspdbdll-file"></a><span id="the_mspdb__dll_file"></span><span id="THE_MSPDB__DLL_FILE"></span>Mspdb\*.dll ファイル

PDBCopy を実行するには、Mspdb80 ファイルまたは Mspdb60 ファイルのいずれかにアクセスする必要があります。 既定では、PDBCopy は Mspdb80 を使用します。これは、visual Studio .NET 2002 以降のバージョンの Visual Studio で使用されるバージョンです。 シンボルが Visual Studio 6.0 またはそれ以前のバージョンを使用して作成されている場合は、-vc6.dll コマンドラインオプションを指定すると、PDBCopy は代わりに Mspdb60 を使用します。ただし、これは必須ではありません。 PDBCopy は、-vc6.dll オプションが使用されていない場合でも、適切なファイルを検索します。 これらのファイルは、Visual Studio、Platform SDK、または Windows Driver Kit (WDK) のインストール内で見つけることができます。

PDBCopy を実行する前に、適切なバージョンの mspdb\*.dll ファイルがコンピューターにアクセス可能であることを確認し、その場所がコマンドパスの一部であることを確認してください。 そうでない場合は、 **path**コマンドを使用して、この場所をコマンドパスに追加する必要があります。

### <a name="span-idthe_file_signature_and_the_symsrv_indexspanspan-idthe_file_signature_and_the_symsrv_indexspanthe-file-signature-and-the-symsrv-index"></a><span id="the_file_signature_and_the_symsrv_index"></span><span id="THE_FILE_SIGNATURE_AND_THE_SYMSRV_INDEX"></span>ファイルの署名と SymSrv インデックス

各シンボルファイルには、それを一意に識別する固定署名があります。 SymSrv は、署名を使用して、ファイルの一意な "インデックス値" を生成します。 2つのファイルの内容が異なる場合、または作成時間が異なる場合は、個別の署名と異なる SymSrv インデックス値も保持されます。

PDBCopy で作成されたファイルは、一意のインデックス値のルールの例外です。 PDBCopy によって新しいシンボルファイルが作成されると、古いファイルと同じ署名と SymSrv インデックス値が生成されます。 この機能により、シンボル関連のツールの動作を変更することなく、1つのファイルを別のファイルに置き換えることができます。

新しいファイルに個別の署名と SymSrv インデックスを作成する場合は、-s オプションを使用します。 ほとんどの場合、このオプションは使用しません。これは、PDBCopy の最も一般的な用途は、変更されたシンボルファイルを作成して、不一致が発生することなく古いファイルを置き換えることができるためです。 新しい署名があると、SymSrv によって古いファイルとは異なるインデックス値が新しいファイルに割り当てられ、新しいファイルが古いファイルを適切に置き換えることができなくなる可能性があります。

コマンドラインの完全な構文については、「 [**PDBCopy のコマンドラインオプション**](pdbcopy-command-line-options.md)」を参照してください。

 

 





