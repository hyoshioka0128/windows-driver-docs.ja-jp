---
title: ストレージ形式のシンボル
description: ストレージ形式のシンボル
ms.assetid: 4aeaa644-9da4-4567-9dc7-86db38b7e93c
keywords:
- SymStore、ストレージ形式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8e0d2252edf1a1ee5aed505e448de3c04f25d33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550715"
---
# <a name="symbol-storage-format"></a>ストレージ形式のシンボル


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore は、データベースとして、ファイル システム自体を使用します。 このようなものとして、シンボル ファイルのタイムスタンプ、署名、年齢、およびその他のデータをベースにディレクトリ名、ディレクトリの大規模なツリーを作成します。

など、サーバーに追加されたいくつかの異なる acpi.dbgs、ディレクトリでした次のようになります。

```console
Directory of \\mybuilds\symsrv\acpi.dbg
10/06/1999  05:46p      <DIR>          .
10/06/1999  05:46p      <DIR>          ..
10/04/1999  01:54p      <DIR>          37cdb03962040
10/04/1999  01:49p      <DIR>          37cdb04027740
10/04/1999  12:56p      <DIR>          37e3eb1c62060
10/04/1999  12:51p      <DIR>          37e3ebcc27760
10/04/1999  12:45p      <DIR>          37ed151662060
10/04/1999  12:39p      <DIR>          37ed15dd27760
10/04/1999  11:33a      <DIR>          37f03ce962020
10/04/1999  11:21a      <DIR>          37f03cf7277c0
10/06/1999  05:38p      <DIR>          37fa7f00277e0
10/06/1999  05:46p      <DIR>          37fa7f01620a0
```

この例でよう acpi.dbg シンボル ファイルの検索パスになります: \\ \\mybuilds\\symsrv\\acpi.dbg\\37cdb03962040 します。

参照ディレクトリ内で 3 つのファイルがあります。

1.  acpi.dbg、ファイルが格納されている場合

2.  ポインターが格納されている場合は、実際のシンボル ファイルへのパスで file.ptr

3.  シンボル ストアに現在追加されているタイムスタンプとイメージのサイズがこの acpi.dbg のすべての現在場所のリストを含む、refs.ptr

ディレクトリの一覧を表示する\\ \\mybuilds\\symsrv\\acpi.dbg\\37cdb03962040 は、次を提供します。

```console
10/04/1999  01:54p                  52 file.ptr
10/04/1999  01:54p                  67 refs.ptr
```

テキスト文字列を格納するファイル file.ptr"\\\\mybuilds\\シンボル\\x86\\2128.chk\\シンボル\\sys\\acpi.dbg"。 デバッガーはでファイルを検索しようとしてこのディレクトリに acpi.dbg をという名前のファイルがないため、 \\ \\mybuilds\\シンボル\\x86\\2128.chk\\シンボル\\sys\\acpi.dbg します。

Refs.ptr の内容は、SymStore、いないのデバッガーでのみ使用されます。 このファイルには、このディレクトリで行われたすべてのトランザクションのレコードが含まれています。 Refs.ptr からのサンプル行は次のようになります。

```text
0000000026,ptr,\\mybuilds\symbols\x86\2128.chk\symbols\sys\acpi.dbg
```

これは、ことを示していますへのポインター \\ \\mybuilds\\シンボル\\x86\\2128.chk\\シンボル\\sys\\acpi.dbg トランザクション「0000000026」が追加されました。

一部のシンボル ファイルはさまざまな製品のビルドまたは特定の製品を通じて一定のままです。 この 1 つの例では、Windows 2000 のファイル msvcrt.pdb です。 ディレクトリ一覧\\ \\mybuilds\\symsrv\\msvcrt.pdb msvcrt.pdb だけ 2 つのバージョンがシンボル サーバーに追加されたことを示しています。

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb
10/06/1999  05:37p      <DIR>          .
10/06/1999  05:37p      <DIR>          ..
10/04/1999  11:19a      <DIR>          37a8f40e2
10/06/1999  05:37p      <DIR>          37f2c2272
```

ただし、ディレクトリの一覧の\\ \\mybuilds\\symsrv\\msvcrt.pdb\\37a8f40e2 その refs.ptr が含まれる複数のポインターを示しています。

```console
Directory of \\mybuilds\symsrv\msvcrt.pdb\37a8f40e2
10/05/1999  02:50p              54     file.ptr
10/05/1999  02:50p           2,039     refs.ptr
```

内容\\ \\mybuilds\\symsrv\\msvcrt.pdb\\37a8f40e2\\refs.ptr 次に示します。

```text
0000000001,ptr,\\mybuilds\symbols\x86\2137\symbols\dll\msvcrt.pdb
0000000002,ptr,\\mybuilds\symbols\x86\2137.chk\symbols\dll\msvcrt.pdb
0000000003,ptr,\\mybuilds\symbols\x86\2138\symbols\dll\msvcrt.pdb
0000000004,ptr,\\mybuilds\symbols\x86\2138.chk\symbols\dll\msvcrt.pdb
0000000005,ptr,\\mybuilds\symbols\x86\2139\symbols\dll\msvcrt.pdb
0000000006,ptr,\\mybuilds\symbols\x86\2139.chk\symbols\dll\msvcrt.pdb
0000000007,ptr,\\mybuilds\symbols\x86\2140\symbols\dll\msvcrt.pdb
0000000008,ptr,\\mybuilds\symbols\x86\2140.chk\symbols\dll\msvcrt.pdb
0000000009,ptr,\\mybuilds\symbols\x86\2136\symbols\dll\msvcrt.pdb
0000000010,ptr,\\mybuilds\symbols\x86\2136.chk\symbols\dll\msvcrt.pdb
0000000011,ptr,\\mybuilds\symbols\x86\2135\symbols\dll\msvcrt.pdb
0000000012,ptr,\\mybuilds\symbols\x86\2135.chk\symbols\dll\msvcrt.pdb
0000000013,ptr,\\mybuilds\symbols\x86\2134\symbols\dll\msvcrt.pdb
0000000014,ptr,\\mybuilds\symbols\x86\2134.chk\symbols\dll\msvcrt.pdb
0000000015,ptr,\\mybuilds\symbols\x86\2133\symbols\dll\msvcrt.pdb
0000000016,ptr,\\mybuilds\symbols\x86\2133.chk\symbols\dll\msvcrt.pdb
0000000017,ptr,\\mybuilds\symbols\x86\2132\symbols\dll\msvcrt.pdb
0000000018,ptr,\\mybuilds\symbols\x86\2132.chk\symbols\dll\msvcrt.pdb
0000000019,ptr,\\mybuilds\symbols\x86\2131\symbols\dll\msvcrt.pdb
0000000020,ptr,\\mybuilds\symbols\x86\2131.chk\symbols\dll\msvcrt.pdb
0000000021,ptr,\\mybuilds\symbols\x86\2130\symbols\dll\msvcrt.pdb
0000000022,ptr,\\mybuilds\symbols\x86\2130.chk\symbols\dll\msvcrt.pdb
0000000023,ptr,\\mybuilds\symbols\x86\2129\symbols\dll\msvcrt.pdb
0000000024,ptr,\\mybuilds\symbols\x86\2129.chk\symbols\dll\msvcrt.pdb
0000000025,ptr,\\mybuilds\symbols\x86\2128\symbols\dll\msvcrt.pdb
0000000026,ptr,\\mybuilds\symbols\x86\2128.chk\symbols\dll\msvcrt.pdb
0000000027,ptr,\\mybuilds\symbols\x86\2141\symbols\dll\msvcrt.pdb
0000000028,ptr,\\mybuilds\symbols\x86\2141.chk\symbols\dll\msvcrt.pdb
0000000029,ptr,\\mybuilds\symbols\x86\2142\symbols\dll\msvcrt.pdb
0000000030,ptr,\\mybuilds\symbols\x86\2142.chk\symbols\dll\msvcrt.pdb
```

同じ msvcrt.pdb に格納されている Windows 2000 のシンボルの複数のビルドに使用された表示\\ \\mybuilds\\symsrv します。

ファイル サービスおよびポインターの追加機能の組み合わせを格納するディレクトリの例を次に示します。

```console
Directory of E:\symsrv\dbghelp.dbg\38039ff439000
10/12/1999  01:54p         141,232     dbghelp.dbg
10/13/1999  04:57p              49     file.ptr
10/13/1999  04:57p             306     refs.ptr
```

この場合、refs.ptr では、次の内容があります。

```text
0000000043,file,e:\binaries\symbols\retail\dll\dbghelp.dbg
0000000044,file,f:\binaries\symbols\retail\dll\dbghelp.dbg
0000000045,file,g:\binaries\symbols\retail\dll\dbghelp.dbg
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

したがって、43、44、および 45 のトランザクションは、サーバー、およびトランザクション 46 と追加 47 ポインターに同じファイルを追加します。 43、44、および 45 のトランザクションが削除された場合、ファイル dbghelp.dbg はディレクトリから削除されます。 ディレクトリは、次の内容になります。

```console
Directory of e:\symsrv\dbghelp.dbg\38039ff439000
10/13/1999  05:01p                   49 file.ptr
10/13/1999  05:01p                 130 refs.ptr
```

File.ptr を含むようになりました"\\\\foo2\\bin\\シンボル\\小売\\dll\\dbghelp.dbg"、refs.ptr が含まれています

```text
0000000046,ptr,\\MyDir\bin\symbols\retail\dll\dbghelp.dbg
0000000047,ptr,\\foo2\bin\symbols\retail\dll\dbghelp.dbg
```

Refs.ptr の最終的なエントリが、ポインターは、ファイル file.ptr が存在し、関連付けられているファイルへのパスします。 Refs.ptr の最終的なエントリがファイルの場合、このディレクトリに file.ptr は存在しません。 そのため、refs.ptr で最終的なエントリを削除するため、削除操作が原因で file.ptr される作成、削除、または変更します。

 

 





