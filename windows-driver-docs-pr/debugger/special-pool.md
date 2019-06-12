---
title: Special Pool
description: Special Pool
ms.assetid: 8904913d-78ed-4e5f-acef-3c21eeb87b8d
keywords:
- Special Pool
- 特別なプール, 概要
- GFlags、特別なプール
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0e21ba07f3506996d5ab113a70b32c6a949c813
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368092"
---
# <a name="special-pool"></a>Special Pool


**特別なプール**機能に構成予約済みのメモリ プールから Windows がメモリの割り当てを要求するメモリの指定したプール タグを割り当てることがまたはが指定されたサイズの範囲内とします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>spp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>(なし)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>(なし)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p>
<p>(Windows Vista 以降)システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idselectingapooltagspanspan-idselectingapooltagspanselecting-a-pool-tag"></a><span id="selecting_a_pool_tag"></span><span id="SELECTING_A_POOL_TAG"></span>プール タグを選択します。

特定のプール タグの特別なプールを要求するときに、ドライバーまたはその他のカーネル モードのプログラムがプールの一意のタグを使用することを確認します。

また、プール タグを作成するときに (などを使用して**exallocatepoolwithtag に**)、逆の順序でタグの文字を入力することを検討してください。 たとえば、タグは**Fred**、入力として**derF** (0x64657246)。 プール タグは、レジストリに格納されているし、デバッガーと順序を逆 (下のエンディアン) では、その他のツールに表示されます。 順方向順序 (0x46726564) に表示されている場合は逆の順序で入力と、

ドライバーを消費しているすべての特別なプールが疑われる場合、コードでの複数のプール タグの使用を検討してください。 テストできます、ドライバーを複数回テストごとに 1 つのプール タグへの特別なプールの割り当ています。

また、システムのページ サイズよりも大きい 16 進数の値を持つプール タグを選択します。 カーネル モード コードでは、プール タグを入力した場合のあるページより小さい値\_Gflags が特別なプールのサイズが、対応する範囲内にあるし、特別なプールのプールと同じタグを使用して割り当てを要求のすべての割り当てを要求するサイズ、します。 サイズを選択する場合など**30**、17 と 32 バイトとの間のすべての割り当てと、プール タグ 0x0030 割り当て特別のプールが使用されます。

### <a name="span-idselectinganallocationsizespanspan-idselectinganallocationsizespanselecting-an-allocation-size"></a><span id="selecting_an_allocation_size"></span><span id="SELECTING_AN_ALLOCATION_SIZE"></span>アロケーション サイズを選択します。

次のガイドラインを使用して、特別なプール機能の割り当てサイズを選択します。

X86 コンピューターでプロセッサ、ページ\_サイズは、0x1000、割り当てサイズの範囲が 8 バイトの長さ。 この範囲のサイズですべての割り当ての特別なプール機能を構成するには、この範囲と 8 の最大値に等しい数値を入力します。 (この数は常に 8 の倍数) です。次の表は、これらの値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サイズの範囲</th>
<th align="left">この数値を入力します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 から 8 バイト</p></td>
<td align="left"><p>10 (16 進数)</p></td>
</tr>
<tr class="even">
<td align="left"><p>9 ~ 16 バイト</p></td>
<td align="left"><p>18 (10 進 24)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17 ~ 24 バイト</p></td>
<td align="left"><p>20 (10 進数の 32)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFE9 に 0xFF0 バイト</p></td>
<td align="left"><p>FF8 (10 進 4088)</p></td>
</tr>
</tbody>
</table>

 

ページ、AMD x86 プロセッサを搭載したコンピューターで\_サイズは、0x1000、割り当てサイズの範囲が 16 バイトの長さ。 この範囲のサイズですべての割り当ての特別なプール機能を構成するには、この範囲と 16 の最大値に等しい数値を入力します。 (この数は常に 16 の倍数) です。次の表は、これらの値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サイズの範囲</th>
<th align="left">この数値を入力します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 ~ 16 バイト</p></td>
<td align="left"><p>20 (10 進数の 32)</p></td>
</tr>
<tr class="even">
<td align="left"><p>17 ~ 32 バイト</p></td>
<td align="left"><p>30 (48 個の 10 進数)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>33 ~ 48 バイト</p></td>
<td align="left"><p>40 (10 進数の 64)</p></td>
</tr>
<tr class="even">
<td align="left"><p>...</p></td>
<td align="left"><p>...</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFD1 に 0xFE0 バイト</p></td>
<td align="left"><p>FF0 (10 進 4080)</p></td>
</tr>
</tbody>
</table>

 

すべてのプロセッサを搭載したコンピューターには、アスタリスクを使用できます ( **\\** *) または 0x2A (10 進 42) システムで、すべてのメモリ割り当て用に特別なプール機能を構成します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

グローバル フラグ ダイアログ ボックスで、特別なプール機能を構成する方法については、次を参照してください。[特別なプールの構成](configuring-special-pool.md)します。 コマンドラインで特別なプール機能を構成する方法の詳細については、次を参照してください。 [ **GFlags コマンド**](gflags-commands.md)します。 例については、次を参照してください。[例 14。特別なプールを構成する](example-14---configuring-special-pool.md)します。

Gflags の特別なプール機能は、メモリの指定されたプール タグを割り当てることがまたはが指定されたサイズの範囲内に Windows をメモリ割り当ての要求に、予約済みのメモリ プールから指示します。 特定のドライバーが特別なプールのすべての割り当てを要求するには、Driver Verifier を使用します。 詳細については、Windows Driver Kit (WDK) の"Driver Verifier"セクションでは「特別なプール」トピックを参照してください。

Gflags、Driver Verifier の特別なプール機能を検出し、割り当てられたメモリ領域を超える書き込みや、既に解放されたメモリを参照するなど、カーネル プールの使用エラーの原因を特定できます。

すべての特別なプールの要求が満たされます。 特別なプールから各割り当ては、非ページングの物理メモリの 1 つのページと仮想アドレス空間の 2 つのページを使用します。 特別なプールがなくなった場合、特別なプールが再び使用可能になるまで、standard プールからメモリが割り当てられます。 特別なプールの要求は、標準的なプールからいっぱいになると、要求元の関数は、成功の状態を返します。 これは、エラーは返されません、割り当てが成功したため、特別なプールから、入力されていなくてもします。

特別なプールのサイズはシステム上の物理メモリ量を増加します。理想的には少なくとも 1 ギガバイト (GB) があります。 X86 マシン、仮想 (場合によってに物理また) 領域が消費されるため、使用しないでください、 **3 GB**特別なプールを使用する場合は、オプションを起動します。 2 または 3 の倍数でページファイルの最小値/最大数量を増やすことをお勧めします。

メモリ割り当て (「アンダーラン」) の前への参照または割り当て (「オーバーラン」) を超えるメモリへの参照を検出するためにメモリの割り当てを整列する特別なプール機能を構成することもできます。 この機能は、Windows のすべてのバージョンのグローバル フラグのダイアログ ボックスでのみ使用できます。 詳細については、次を参照してください。[オーバーランの検出とアンダーラン](detecting-overruns-and-underruns.md)します。

レジストリ設定を再起動が必要ですが、変更するか、またはカーネル フラグとして設定は、再起動まで有効なままになりますが、するまでは、有効では、Windows Vista および Windows の以降のバージョンでは、特別なプール機能を構成することができます。Windows をシャット ダウンまたは再起動します。 以前のバージョンの Windows では、特別なプールでは、レジストリ設定として利用可能なのみです。

Windows Vista と Windows の以降のバージョンでは、グローバル フラグのダイアログ ボックスを使用して、またはコマンドラインで特別なプール機能を構成できます。 以前のバージョンの Windows では、この機能は、グローバル フラグのダイアログ ボックスでのみ使用できます。

 

 





