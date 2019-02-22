---
title: DXVA_ConfigQueryOrReplyFlag and DXVA_ConfigQueryorReplyFunc
description: DXVA_ConfigQueryOrReplyFlag and DXVA_ConfigQueryorReplyFunc Variables
ms.assetid: bfb1a98e-b9f0-4baa-b486-b2ff33a8bac5
keywords:
- ビデオのデコード WDK DirectX va なので、書式設定します。
- ビデオの WDK DirectX va なので、形式のデコード
- WDK の DirectX va なので、形式をデコードする画像
- WDK DirectX VA を書式設定します。
- bDXVA_Func 変数 WDK DirectX VA
- DXVA_ConfigQueryOrReplyFlag
- DXVA_ConfigQueryorReplyFunc
- ビデオのデコード WDK DirectX va なので、構成のプローブとロック
- ビデオの WDK DirectX va なので、構成のプローブとロックのデコード
- WDK の DirectX va なので、構成のプローブとロックをデコードする画像
- 最小限の相互運用性の構成設定の WDK DirectX VA
- ロック構成 WDK DirectX VA
- WDK DirectX VA の構成のプローブ
- 構成のプローブと WDK DirectX VA のロック
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 68d0c0727156b80ffac718897cd1e3e9d1b8a6e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560585"
---
# <a name="dxvaconfigqueryorreplyflag-and-dxvaconfigqueryorreplyfunc-variables"></a>DXVA\_ConfigQueryOrReplyFlag と DXVA\_ConfigQueryorReplyFunc 変数

*DXVA\_ConfigQueryOrReplyFlag*変数がクエリの種類を示しますまたはプローブとロックを使用するときの応答コマンドします。 最も重要な 24 ビット、 **dwFunction**以下の構造体のメンバーが含まれています、 *DXVA\_ConfigQueryOrReplyFlag*変数。

[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)圧縮された画像をデコードします。

[**DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)アルファ ブレンド データを読み込むためです。

[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126)アルファ ブレンドの組み合わせ。

最上位 20 のビット、 *DXVA\_ConfigQueryOrReplyFlag*変数は、次のクエリと応答を指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xFFFF1</p></td>
<td align="left"><p>プローブをコマンドとしてホスト デコーダーによって送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF5</p></td>
<td align="left"><p>ロック コマンドとしてホスト デコーダーによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFF8</p></td>
<td align="left"><p>プローブ コマンド、プローブの構成のコピーに S_OK 応答をアクセラレータによって送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF9</p></td>
<td align="left"><p>推奨される代替の構成のプローブのコマンドに S_OK 応答をアクセラレータによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFC</p></td>
<td align="left"><p>ロック コマンド、ロックされている構成のコピーに S_OK 応答をアクセラレータによって送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFFB</p></td>
<td align="left"><p>推奨される代替の構成のプローブのコマンドに S_FALSE 応答をアクセラレータによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xfffff</p></td>
<td align="left"><p>推奨される代替の構成でのロック コマンドに S_FALSE 応答をアクセラレータによって送信されます。</p></td>
</tr>
</tbody>
</table>

 

最下位 4 ビット、 *DXVA\_ConfigQueryOrReplyFlag*変数がクエリと応答の次のステータス インジケーターを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>これは、ホスト デコーダーとアクセラレータから送信されたときに 1 が送信する場合、0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>これは、プローブ、およびロックに関連付けられている場合は 1 に関連付けられている場合は 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>これは、成功、0 と 1 の障害を。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>ときに、重複する構成構造体、および 1 は、その新しい構成構造の場合は 0 です。</p></td>
</tr>
</tbody>
</table>

 

最下位の 8 ビット、 **dwFunction**メンバーは、 *bDXVA\_Func*変数。 *BDXVA\_Func*を使用すると、変数*DXVA\_ConfigQueryorReplyFunc*、プローブ、およびロック操作を示しますおよび関連する構成を指定します関数。

### <a name="span-idprobingandlockingspanspan-idprobingandlockingspanspan-idprobingandlockingspanprobing-and-locking"></a><span id="Probing_and_Locking"></span><span id="probing_and_locking"></span><span id="PROBING_AND_LOCKING"></span>プローブとロック

ときに*bDXVA\_Func*プローブし、特定の DirectX VA 関数の構成をロックするために使用*bDXVA\_Func*最下位の 8 ビット、に*DXVA*\_*ConfigQueryorReplyFunc*変数。 *DXVA*\_*ConfigQueryorReplyFunc* Microsoft Windows SDK で指定されているアクセラレータに伝達されます。

### <a name="span-idspecifyingaconfigurationtobeprobedorlockedspanspan-idspecifyingaconfigurationtobeprobedorlockedspanspan-idspecifyingaconfigurationtobeprobedorlockedspanspecifying-a-configuration-to-be-probed-or-locked"></a><span id="Specifying_a_Configuration_To_Be_Probed_or_Locked"></span><span id="specifying_a_configuration_to_be_probed_or_locked"></span><span id="SPECIFYING_A_CONFIGURATION_TO_BE_PROBED_OR_LOCKED"></span>検出されたか、ロックの構成を指定します。

ときに*bDXVA\_Func*プローブまたはロックのコマンドで渡される構成構造に関連付けられている関数を指定するために使用*bDXVA\_Func*は 8 に配置されます最下位の*DXVA\_ConfigQueryorReplyFunc*変数、 **dwFunction**構成構造体を次のいずれかのメンバー。

[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)圧縮された画像をデコードします。

[**DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)アルファ ブレンド データを読み込むためです。

[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126)アルファ ブレンドの組み合わせ。

### <a name="span-iddxvaencryptprotocolfuncspanspan-iddxvaencryptprotocolfuncspanspan-iddxvaencryptprotocolfuncspandxvaencryptprotocolfunc"></a><span id="DXVA_EncryptProtocolFunc"></span><span id="dxva_encryptprotocolfunc"></span><span id="DXVA_ENCRYPTPROTOCOLFUNC"></span>DXVA\_EncryptProtocolFunc

最も重要な 24 ビット、 *DXVA\_EncryptProtocolFunc* DWORD 変数は次のように設定されます。

-   0xFFFF00 ホスト ソフトウェア デコーダーによって送信されると、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体への呼び出しで[*DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。

-   0xFFFF08 でビデオ アクセラレータによって送信されたときに、 **dwFunction**のメンバー、 [ **DXVA\_EncryptProtocolHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff563965)構造体。

最下位の 8 ビット、 *DXVA\_EncryptProtocolFunc* DWORD 変数の値を格納する*bDXVA\_Func*暗号化プロトコルに関連付けられています。 このような使用はサポートされている値だけ*bDXVA\_Func* = 1 (圧縮された画像のデコード)。

### <a name="span-idspecifyinganoperationtobeperformedbyddmocomprenderspanspan-idspecifyinganoperationtobeperformedbyddmocomprenderspanspan-idspecifyinganoperationtobeperformedbyddmocomprenderspanspecifying-an-operation-to-be-performed-by-ddmocomprender"></a><span id="Specifying_an_Operation_to_be_Performed_by_DdMoCompRender"></span><span id="specifying_an_operation_to_be_performed_by_ddmocomprender"></span><span id="SPECIFYING_AN_OPERATION_TO_BE_PERFORMED_BY_DDMOCOMPRENDER"></span>DdMoCompRender により実行される操作を指定します。

ときに*bDXVA\_Func*を使用して実行する実際の操作の通知 (画像をデコード、アルファ ブレンドのデータの読み込み、アルファ ブレンドの組み合わせ、または画像が再サンプリングを圧縮) *bDXVA\_Func*のシリーズを含めることによって、アクセラレータに伝達されます*bDXVA\_Func*バイト値、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体への呼び出しで[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。 最初の*bDXVA\_Func*操作は、最上位バイトで指定されて、次の操作を指定で、[次へ] 最上位バイト、します。 残りのバイト**dwFunction**が 0 に設定します。

 

 





