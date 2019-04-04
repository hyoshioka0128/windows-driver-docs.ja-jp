---
title: PDBCopy のコマンドライン オプション
description: PDBCopy コマンドラインは、次の構文を使用します。 パラメーターは、任意の順序で含めることができます。
ms.assetid: a793f860-db21-41fb-a0d2-931812400f0d
keywords:
- PDBCopy コマンド ライン オプションの Windows デバッグ
ms.date: 04/10/2018
topic_type:
- apiref
api_name:
- PDBCopy Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9f8c1ed1d96b0bc9654ce5ce9aa26cd0c8c04d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580049"
---
# <a name="pdbcopy-command-line-options"></a>PDBCopy のコマンドライン オプション


PDBCopy コマンドラインは、次の構文を使用します。 パラメーターは、任意の順序で含めることができます。

```dbgcmd
pdbcopy OldPDB NewPDB [Options] 

pdbcopy OldPDB NewPDB -p [-f:Symbol] [-f:@TextFile] [Options] 

pdbcopy OldPDB NewPDB -p [-F:Symbol] [-F:@TextFile] [Options] 

pdbcopy InputPDB BackupPDB -CVE-2018-1037 [autofix|verbose]

pdbcopy /? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______OldPDB______"></span><span id="_______oldpdb______"></span><span id="_______OLDPDB______"></span> *OldPDB*   
.Pdb ファイル名拡張子を含む、読み取り元のシンボル ファイルのパスとファイル名を指定します。 *OldPDB*ローカル コンピューター上のディレクトリの絶対または相対パスまたは UNC パスを含めることができます。 パスが指定されていない場合は、現在の作業ディレクトリが使用されます。 場合*OldPDB*スペースが含まれることは、引用符で囲む必要があります。

<span id="_______NewPDB______"></span><span id="_______newpdb______"></span><span id="_______NEWPDB______"></span> *NewPDB*   
.Pdb ファイル名拡張子を含む、作成する新しいシンボル ファイルのパスとファイル名を指定します。 *NewPDB*ローカル コンピューター上のディレクトリの絶対または相対パスまたは UNC パスを含めることができます。 このパスは既に存在する必要があります。PDBCopy では、新しいディレクトリは作成されません。 パスが指定されていない場合は、現在の作業ディレクトリが使用されます。 場合*NewPDB*スペースを含む引用符で括る必要があります。 指定したファイルがまだ存在しない必要があります。場合は、新しいファイルが書き込まれません、または正しく書き込むことができます。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
新しいシンボル ファイルからプライベート シンボル データを削除する PDBCopy をによりします。 古いシンボル ファイルにプライベート シンボルが含まれていない場合、このオプションは影響を与えません。 このオプションを省略すると、PDBCopy は元のファイルと同じシンボルのコンテンツを含む新しいファイルを作成します。

<span id="-f_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-f:**<em>シンボル</em>  
新しいシンボル ファイルから指定されたパブリック シンボルを削除する PDBCopy をによりします。 *シンボル*などのシンボル名の装飾 (たとえば、初期のアンダー スコア)、ただし、モジュール名を除く、削除するシンボルの名前を指定する必要があります。 このオプションでは、-p オプションが必要です。 複数を使用する場合 **-f**または **-@ f:** PDBCopy のパラメーターは、新しいシンボル ファイルから指定したすべてのシンボルを削除します。

<span id="-f__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-@ f:**<em>TextFile</em>  
新しいシンボル ファイルから指定したテキスト ファイルに一覧表示、パブリック シンボルを削除する PDBCopy をによりします。 *TextFile*このファイルのパス (絶対または相対パス) とファイル名を指定します。 このファイルは、任意の数などのシンボル名の装飾 (たとえば、初期のアンダー スコア)、ただし、モジュール名を除く各の行に 1 つのシンボルの名前を一覧表示できます。 このオプションでは、-p オプションが必要です。

<span id="-F_Symbol"></span><span id="-f_symbol"></span><span id="-F_SYMBOL"></span>**-F:**<em>シンボル</em>  
指定したパブリック シンボルを除く、新しいシンボル ファイルからすべてのパブリックおよびプライベート シンボルを削除する PDBCopy をによりします。 *シンボル*などのシンボル名の装飾 (たとえば、初期のアンダー スコア)、ただし、モジュール名を除く、保持するシンボルの名前を指定する必要があります。 このオプションでは、-p オプションが必要です。 複数 **-f**または **-@ f:** パラメーターを使用する場合、指定したすべてのシンボルは、新しいシンボル ファイルに保持されます。

<span id="-F__TextFile"></span><span id="-f__textfile"></span><span id="-F__TEXTFILE"></span>**-@ F:**<em>TextFile</em>  
指定したテキスト ファイルに一覧表示、パブリック シンボルを除く、新しいシンボル ファイルからすべてのパブリックおよびプライベート シンボルを削除する PDBCopy をによりします。 *TextFile*このファイルのパス (絶対または相対パス) とファイル名を指定します。 このファイルは、任意の数などのシンボル名の装飾 (たとえば、初期のアンダー スコア)、ただし、モジュール名を除く各の行に 1 つのシンボルの名前を一覧表示できます。 このオプションでは、-p オプションが必要です。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせ。 これらのオプションは、大文字小文字を区別します。

<span id="-s"></span><span id="-S"></span>**-s**  
古いファイルよりも、別の署名がある新しいシンボル ファイルが実行します。 通常を使用しないでください、-s オプションの新しい署名で SymSrv よりも古いファイルの新しいファイルに別のインデックス値を割り当てることがあるため新しいファイルが古いものを正しく交換することを防止します。

<span id="-vc6"></span><span id="-VC6"></span>**-vc6**  
代わりに使用する mspdb60.dll mspdb80.dll PDBCopy をによりします。 このオプションは、PDBCopy が mspdb の適切なバージョンを自動的に検索するため、必要なことはありません\*.dll です。 既定では、PDBCopy は、Visual Studio .NET 2002 および Visual Studio の以降のバージョンで使用されるバージョンである mspdb80.dll で使用します。 Visual Studio 6.0 または以前のバージョンを使用して、シンボルが構築され場合、は、PDBCopy が mspdb60.dll を代わりに使用されるようにこのコマンド ライン オプションを指定できます。 ただし、これは必要ありません、ため、このオプションを使用しない場合でも、PDBCopy が適切なファイルを探します。 どちらのバージョンの mspdb\*PDBCopy を起動するコマンド プロンプト ウィンドウの実行可能ファイルのパスに .dll を使用する必要があります。


<span id="CVE-2018-1037"></span> **-CVE-2018-1037**   

InputPDBFile CVE-2018-1037 で説明されている問題が発生し、必要に応じて、問題を修復するかどうかを報告します。 参照してください[KB # 4131751 - PDBCopy ツール](https://support.microsoft.com/help/4131751/pdbcopy-update-to-fix-pdb-security-issue)詳細と使用状況の詳細情報。


<span id="_______-_______"></span> **-?**   
PDBCopy コマンドラインのヘルプを表示します。



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

PDBCopy ツールの詳細については、[を使用して PDBCopy](using-pdbcopy.md)を参照してください。

 

 





