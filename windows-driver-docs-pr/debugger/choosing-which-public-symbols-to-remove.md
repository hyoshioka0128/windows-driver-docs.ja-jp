---
title: 削除するパブリック シンボルの選択
description: 削除するパブリック シンボルの選択
ms.assetid: 0de89f65-ebb5-4186-a6f9-6676f86a75f1
keywords:
- PDBCopy、パブリック シンボルを削除します。
- シンボル、AgeStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1037cf0da20c92921234a65836c71b57a7c262db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375100"
---
# <a name="choosing-which-public-symbols-to-remove"></a>削除するパブリック シンボルの選択


対象ユーザーが、デバッグを実行するためにアクセスする必要があるシンボルのみを離れることから削除されたシンボル ファイルでは、パブリック シンボルの任意のセットを削除することができるように、PDBCopy は-f および-f オプションを提供します。

PDBCopy の一般的な用途では、その Online Crash Analysis (OCA) プログラムで特別なバージョンの Microsoft によって使用されるシンボル ファイルを作成します。 OCA として特定の関数を指定できます*模擬*ことを示す場合は、関数がスタックにあるトレースが無視されます。 関数は通常宣言するラッパーまたは重要な計算を実行しない「パススルー」関数では単純にする場合にのみ。 失敗の分析でスタックにこのような関数が見つかった場合は、ことは、この関数自体が、エラー、スタックで先ほどルーチンから受信したデータが無効であるか破損している渡さ多くて想定できます。 このような関数を無視することでと、OCA は、実際のエラーまたは破損の原因を見つけやすくなります。

当然ながら、「模擬」を宣言したい任意の関数は、OCA によって使用されるシンボル ファイルのパブリック シンボル テーブルに含まれる必要があります。 ただし、関数、例を次に示すようにインクルードする必要があるだけではありません。

たとえば Windows ドライバーを作成して、PDBCopy を使用して、以外のシンボル ファイルからのすべてのパブリック シンボルを削除する**FunctionOne**と**FunctionSix**、2 つの模擬関数。 期待されている場合は、いずれか**FunctionOne**または**FunctionSix**上にあるスタック クラッシュの後、OCA では無視されます。 ドライバーの他の部分がスタック上にある場合は、Microsoft で対応するメモリ アドレスを指定し、アドレスを使用するには、ドライバーをデバッグします。

ただしには、ドライバーが次のレイアウトでメモリを占有と仮定しましょう。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Address</th>
<th align="left">メモリの内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>モジュールのベース アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>先頭<strong>FunctionOne</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>終了<strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>先頭<strong>FunctionSix</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>終了<strong>FunctionSix</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>メモリ内のモジュールの終了</p></td>
</tr>
</tbody>
</table>

 

デバッガーには、スタック上のアドレスが検出されると、[次へ] の下のアドレスを持つ記号を選択します。 パブリック シンボル テーブルに各シンボル情報は含まれないサイズのアドレスが格納されているために、デバッガーがアドレスが実際には、シンボルの特定の境界内にあるかどうかを知る方法はありません。

そのため、アドレス 0x2031 で障害が発生した場合に、Microsoft OCA によって正常に実行するデバッガー識別内にあるとしてエラー **FunctionOne**します。 これは、模擬の関数であるため、デバッガーは、クラッシュの原因を特定するスタック ウォークを継続します。

ただし、0x2052 で障害が発生した場合、デバッガーとまだ一致にこのアドレス**FunctionOne**に設定 (0x203F) この関数の実際の末尾を越える場合でも、します。

その結果、関数を公開するだけでなく、これらの関数の直後に続くシンボル、削除されたシンボル ファイルに含める必要があります。 この例では公開する**FunctionOne**、 **FunctionTwo**、 **FunctionSix**、および**FunctionSeven**:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Address</th>
<th align="left">メモリの内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>モジュールのベース アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>先頭<strong>FunctionOne</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>終了<strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2040</p></td>
<td align="left"><p>先頭<strong>FunctionTwo</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>先頭<strong>FunctionSix</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>終了<strong>FunctionSix</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3060</p></td>
<td align="left"><p>先頭<strong>FunctionSeven</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>メモリ内のモジュールの終了</p></td>
</tr>
</tbody>
</table>

 

これらの関数の 4 つすべてを削除されたシンボル ファイルに含めるかどうかは、Microsoft OCA 分析のアドレスの一部として 0x2052 を誤って処理はしません**FunctionOne**します。 この例で見なされますこのアドレスが含まれている**FunctionTwo**が、その登録していないため、重要ではありません**FunctionTwo** OCA 模擬関数として使用します。 重要な点は 0x2052 アドレスは、模擬関数内でも該当しないとして認識、したがって OCA はこれをドライバー内で意味のあるエラーとして認識し、エラーを通知できます。

各模擬関数を次の関数の名前を公開したくない場合は、これらの関数の名前は、パブリック シンボル ファイルに含めることができるように、各模擬関数を次のコードに重要でない関数を挿入できます。 エントリのいくつかの最適化のルーチンが、これを変更するか、またはもいくつかの関数を完全に削除から、これらの追加の関数は、バイナリのアドレス空間でのみ、関数がに従って実際ことを確認してください。

 

 





