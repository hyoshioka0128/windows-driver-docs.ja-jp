---
title: SymStore トランザクション
description: SymStore トランザクション
ms.assetid: f0bb2f3f-0f6b-4ed6-809e-f55b1c537d7f
keywords:
- SymStore、トランザクション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4a657cd27e7a852210c6ae5f982e9f1e4390b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537005"
---
# <a name="symstore-transactions"></a>SymStore トランザクション


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


SymStore にすべての呼び出しは、トランザクションとして記録されます。 トランザクションの 2 種類があります。 追加および削除します。

シンボル ストアを作成すると、"000admin"と呼ばれる、ディレクトリは、サーバーのルートの下に作成されます。 000admin ディレクトリには、ログと、各トランザクションでは、1 つのファイルが含まれています。 server.txt と history.txt ファイル。 Server.txt ファイルには、現在、サーバー上にあるすべてのトランザクションの一覧が含まれています。 History.txt ファイルには、すべてのトランザクションの時系列の履歴が含まれています。

SymStore の格納方法や、シンボル ファイルを削除するたびに、新しいトランザクションの数が作成されます。 次に、名前は、このトランザクションの数が、ファイルは、000admin に作成されます。 このファイルには、すべてのファイルまたはこのトランザクション中にシンボル ストアに追加されたポインターの一覧が含まれています。 トランザクションが削除された場合は、SymStore を削除するファイルとポインターを判断するには、そのトランザクション ファイルを読み取ります。

**追加**と**del**オプションが追加または削除のトランザクションが実行するかどうかを指定します。 など、 **/p**追加操作のオプションは、ポインターがある追加するには; を省略することを指定します、 **/p**オプションは、実際のシンボル ファイルが追加されることを指定します。

2 つの別個の段階で、シンボル ストアを作成することもできます。 SymStore でを使用する最初の段階で、 **/x**インデックス ファイルを作成するオプション。 SymStore でを使用する 2 番目の段階で、 **/y**インデックス ファイル内の情報から、実際のストアのファイルまたはポインターを作成するオプション。

これは、さまざまな理由から便利な方法です。 たとえば、これにより、簡単に再作成する場合は、ストアが失われ、何らかの方法でインデックス ファイルがまだ存在する限り、シンボル ストアです。 または、おそらくシンボル ストアを作成するときに、コンピューターに低速ネットワーク接続されているシンボル ファイルを格納しているコンピューター。 この場合、シンボル ファイルと同じコンピューター上のインデックス ファイルを作成、インデックス ファイルを 2 つ目のマシンに転送、および 2 つ目のコンピューターで、ストアを作成します。

SymStore のすべてのパラメーターの完全な一覧については、次を参照してください。 [ **SymStore コマンド ライン オプション**](symstore-command-line-options.md)します。

**注**   SymStore は複数のユーザーからの同時トランザクションをサポートしていません。 その 1 つのユーザーが指定するをお勧め記号の「管理者」を格納し、すべてを担当する**追加**と**del**トランザクション。

 

### <a name="span-idtransactionexamplesspanspan-idtransactionexamplesspantransaction-examples"></a><span id="transaction_examples"></span><span id="TRANSACTION_EXAMPLES"></span>トランザクションの例

SymStore シンボルのポインターを Windows 2000 のビルド 2195 用の追加の 2 つの例をここでは\\ \\MyDir\\symsrv:

```console
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 free" /c "Sample add"
symstore add /r /p /f \\BuildServer\BuildShare\2195free\symbols\*.* /s \\MyDir\symsrv /t "Windows 2000" /v "Build 2195 x86 checked" /c "Sample add"
```

次の例では、SymStore が、アプリケーションのプロジェクトでの実際のシンボル ファイルを追加します\\ \\largeapp\\appserver\\にビンの\\ \\MyDir\\symsrv:。

```console
symstore add /r /f \\largeapp\appserver\bins\*.* /s \\MyDir\symsrv /t "Large Application" /v "Build 432" /c "Sample add"
```

インデックス ファイルの使用方法の例を示します。 最初に、SymStore はシンボル ファイルのコレクションに基づくインデックス ファイルを作成します。 \\ \\largeapp\\appserver\\ビン\\します。 3 番目のコンピューターにインデックス ファイルを配置するこの例では、 \\\\ハブ\\hubshare します。 使用する、 **/g**ファイルのプレフィックスを指定するオプション"\\\\largeapp\\appserver"今後変更される可能性があります。

```console
symstore add /r /p /g \\largeapp\appserver /f \\largeapp\appserver\bins\*.* /x \\hubserver\hubshare\myindex.txt
```

これで、マシンからのすべてのシンボル ファイルを移動するとします\\ \\largeapp\\appserver し、それらに\\\\ファイル\\appserver します。 インデックス ファイルからシンボル ストア自体を作成し、 \\\\ハブ\\hubshare\\myindex.txt として次のとおりです。

```console
symstore add /y \\hubserver\hubshare\myindex.txt /g \\myarchive\appserver /s \\MyDir\symsrv /p /t "Large Application" /v "Build 432" /c "Sample Add from Index"
```

最後に、前のトランザクションによって追加されたファイルを削除する SymStore の例を示します。 (この例では、0000000096) では、トランザクション ID を確認する方法の詳細については、以下の"server.txt と history.txt Files"セクションを参照してください。

```console
symstore del /i 0000000096 /s \\MyDir\symsrv
```

### <a name="span-idtheservertxtandhistorytxtfilesspanspan-idtheservertxtandhistorytxtfilesspanthe-servertxt-and-historytxt-files"></a><span id="the_server_txt_and_history_txt_files"></span><span id="THE_SERVER_TXT_AND_HISTORY_TXT_FILES"></span>Server.txt と history.txt ファイル

トランザクションが追加されたときに、情報のいくつかの項目は server.txt と history.txt 将来参照機能のために追加されます。 Server.txt と追加のトランザクションの history.txt 内の行の例を次に示します。

```text
0000000096,add,ptr,10/09/99,00:08:32,Windows Vista SP 1,x86 fre 1.156c-RTM-2,Added from \\mybuilds\symbols,
```

これは、コンマ区切りの線です。 フィールドは以下のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0000000096</p></td>
<td align="left"><p>トランザクション ID 番号、SymStore によって作成されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>追加</p></td>
<td align="left"><p>トランザクションのタイプ。 このフィールドは、いずれかを指定できます<strong>追加</strong>または<strong>del</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ptr</p></td>
<td align="left"><p>ファイルまたはポインターが追加されたかどうか。 このフィールドは、いずれかを指定できます<strong>ファイル</strong>または<strong>ptr</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10/09/99</p></td>
<td align="left"><p>トランザクションが発生した日付。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>00:08:32</p></td>
<td align="left"><p>トランザクションの開始時刻。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista SP 1</p></td>
<td align="left"><p>製品です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>x86 fre</p></td>
<td align="left"><p>(省略可能) のバージョンです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>追加</p></td>
<td align="left"><p>コメント (省略可能)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>未使用</p></td>
<td align="left"><p>(後で使用できる予約済み)。</p></td>
</tr>
</tbody>
</table>

 

トランザクション ファイル 0000000096 から一部のサンプル行を次に示します。 各行は、ディレクトリとファイルまたはディレクトリに追加されたポインターの場所を記録します。

```text
canon800.dbg\35d9fd51b000,\\mybuilds\symbols\sp4\dll\canon800.dbg
canonlbp.dbg\35d9fd521c000,\\mybuilds\symbols\sp4\dll\canonlbp.dbg
certadm.dbg\352bf2f48000,\\mybuilds\symbols\sp4\dll\certadm.dbg
certcli.dbg\352bf2f1b000,\\mybuilds\symbols\sp4\dll\certcli.dbg
certcrpt.dbg\352bf04911000,\\mybuilds\symbols\sp4\dll\certcrpt.dbg
certenc.dbg\352bf2f7f000,\\mybuilds\symbols\sp4\dll\certenc.dbg
```

使用する場合、 **del**に元に戻すトランザクション**追加**トランザクション、server.txt から次の行が削除されますおよび history.txt に次の行が追加されます。

```text
0000000105,del,0000000096
```

削除のトランザクションのフィールドは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0000000105</p></td>
<td align="left"><p>トランザクション ID 番号、SymStore によって作成されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>del</p></td>
<td align="left"><p>トランザクションのタイプ。 このフィールドは、いずれかを指定できます<strong>追加</strong>または<strong>del</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0000000096</p></td>
<td align="left"><p>削除されたトランザクション。</p></td>
</tr>
</tbody>
</table>

 

 

 





