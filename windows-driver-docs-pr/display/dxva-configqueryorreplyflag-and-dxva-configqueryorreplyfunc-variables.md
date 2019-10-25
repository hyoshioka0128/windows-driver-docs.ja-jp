---
title: DXVA_ConfigQueryOrReplyFlag と DXVA_ConfigQueryorReplyFunc
description: DXVA_ConfigQueryOrReplyFlag 変数と DXVA_ConfigQueryorReplyFunc 変数
ms.assetid: bfb1a98e-b9f0-4baa-b486-b2ff33a8bac5
keywords:
- ビデオデコード WDK DirectX VA、形式
- ビデオのデコード (WDK DirectX VA、形式)
- 画像デコード WDK DirectX VA、形式
- WDK DirectX VA の形式
- bDXVA_Func 変数 WDK DirectX VA
- DXVA_ConfigQueryOrReplyFlag
- DXVA_ConfigQueryorReplyFunc
- ビデオデコード WDK DirectX VA、構成のプローブとロック
- ビデオをデコードする WDK DirectX VA、構成のプローブとロック
- 画像デコード WDK DirectX VA、構成のプローブとロック
- 最小相互運用性構成セット WDK DirectX VA
- 構成のロック WDK DirectX VA
- 構成のプローブ (WDK DirectX VA)
- 構成のプローブとロック (WDK DirectX VA)
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 08309fc27a221f0184f12dcced5be49106443d01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838972"
---
# <a name="dxva_configqueryorreplyflag-and-dxva_configqueryorreplyfunc-variables"></a>DXVA\_ConfigQueryOrReplyFlag と DXVA\_ConfigQueryorReplyFunc 変数

*DXVA\_ConfigQueryOrReplyFlag*変数は、プローブおよびロックコマンドを使用する場合のクエリまたは応答の種類を示します。 次の構造体の**Dwfunction**メンバーの中で最も重要な24ビットに、 *DXVA\_ConfigQueryOrReplyFlag*変数が含まれています。

DXVA は、圧縮された画像デコード用の[**configpicture デコードを\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)します。

DXVA は、アルファブレンドデータの読み込みのための[**ConfigAlphaLoad\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)ます。

DXVA は、アルファブレンドの組み合わせに対して[**ConfigAlphaCombine\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)ます。

*DXVA\_ConfigQueryOrReplyFlag*変数の中で最も重要なものは、次のクエリと応答を指定することです。

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
<td align="left"><p>プローブコマンドとしてホストデコーダーによって送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF5</p></td>
<td align="left"><p>ロックコマンドとしてホストデコーダーによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFF8</p></td>
<td align="left"><p>プローブコマンドに対する S_OK 応答と共に、プローブされた構成のコピーと共に、アクセラレータによって送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF9</p></td>
<td align="left"><p>推奨される代替構成を使用して、プローブコマンドに対する S_OK 応答と共にアクセラレータによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFC</p></td>
<td align="left"><p>ロックコマンドに S_OK 応答を付けてアクセラレータによって送信され、ロックされた構成のコピーが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFFB</p></td>
<td align="left"><p>代替構成を提案して、プローブコマンドに対する S_FALSE 応答と共にアクセラレータによって送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFF</p></td>
<td align="left"><p>ロックコマンドに対する S_FALSE 応答と共にアクセラレータによって送信され、推奨される代替構成を使用します。</p></td>
</tr>
</tbody>
</table>

 

*DXVA\_ConfigQueryOrReplyFlag*変数の最下位4ビットは、クエリと応答に対して次の状態インジケーターを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">16-bit</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>これは、ホストデコーダーによって送信された場合は0、アクセラレータによって送信された場合は1です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>プローブに関連付けられている場合は0、ロックに関連付けられている場合は1です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>成功の場合は0、失敗の場合は1になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>重複する構成構造の場合は0、新しい構成構造の場合は1になります。</p></td>
</tr>
</tbody>
</table>

 

**Dwfunction**メンバーの最上位の8ビットは、 *bDXVA\_Func*変数です。 *DXVA\_ConfigQueryorReplyFunc*と共に使用する場合、 *bDXVA\_Func*変数はプローブおよびロック操作を示し、関連付けられている構成関数を指定します。

### <a name="span-idprobing_and_lockingspanspan-idprobing_and_lockingspanspan-idprobing_and_lockingspanprobing-and-locking"></a><span id="Probing_and_Locking"></span><span id="probing_and_locking"></span><span id="PROBING_AND_LOCKING"></span>プローブとロック

*BDXVA\_func*を使用して特定の DirectX VA 関数の構成をプローブおよびロックする場合、 *bDXVA\_Func*は、 *DXVA*\_*ConfigQueryorReplyFunc*変数の最下位8ビットに配置されます。 *DXVA*\_*ConfigQueryorReplyFunc*は、Microsoft Windows SDK で指定されているように、アクセラレータに伝達されます。

### <a name="span-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspecifying-a-configuration-to-be-probed-or-locked"></a><span id="Specifying_a_Configuration_To_Be_Probed_or_Locked"></span><span id="specifying_a_configuration_to_be_probed_or_locked"></span><span id="SPECIFYING_A_CONFIGURATION_TO_BE_PROBED_OR_LOCKED"></span>プローブまたはロックする構成の指定

*BDXVA\_func*を使用して、プローブまたは lock コマンドで渡される構成構造に関連付けられた関数を指定すると、 *bDXVA\_func*が DXVA の最下位8ビットに配置され *\_* 次のいずれかの構成構造の**dwfunction**メンバーの ConfigQueryorReplyFunc 変数。

DXVA は、圧縮された画像デコード用の[**configpicture デコードを\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)します。

DXVA は、アルファブレンドデータの読み込みのための[**ConfigAlphaLoad\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)ます。

DXVA は、アルファブレンドの組み合わせに対して[**ConfigAlphaCombine\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)ます。

### <a name="span-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspandxva_encryptprotocolfunc"></a><span id="DXVA_EncryptProtocolFunc"></span><span id="dxva_encryptprotocolfunc"></span><span id="DXVA_ENCRYPTPROTOCOLFUNC"></span>DXVA\_EncryptProtocolFunc

*DXVA\_EncryptProtocolFunc* DWORD 変数の最上位の24ビットは、次のように設定されます。

-   0xFFFF00 は、ホストソフトウェアデコーダーによって、DD の**Dwfunction**メンバーで、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)への呼び出しで、 [ **\_rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体によって送信されます。

-   [**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)構造体の**dwfunction**メンバーのビデオアクセラレータによって送信された0xffff08。

*DXVA\_EncryptProtocolFunc* DWORD 変数の最下位8ビットには、暗号化プロトコルに関連付けられている*bDXVA\_Func*の値が含まれています。 この使用に対してサポートされている唯一の値は、 *bDXVA\_Func* = 1 (圧縮画像デコード) です。

### <a name="span-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspecifying-an-operation-to-be-performed-by-ddmocomprender"></a><span id="Specifying_an_Operation_to_be_Performed_by_DdMoCompRender"></span><span id="specifying_an_operation_to_be_performed_by_ddmocomprender"></span><span id="SPECIFYING_AN_OPERATION_TO_BE_PERFORMED_BY_DDMOCOMPRENDER"></span>DdMoCompRender によって実行される操作の指定

*BDXVA\_func*を使用して実際の操作 (圧縮画像のデコード、アルファブレンドのデータの読み込み、アルファブレンドの組み合わせ、または画像の再サンプリング) を通知する場合、 *bDXVA\_func*は、によってアクセラレータに伝達されます。[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)の呼び出しで、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバー内の一連の*bDXVA\_Func* byte 値に含まれます。 最初の*bDXVA\_Func*操作は最上位バイトで指定され、次の操作は、次の最上位バイトに指定されます。 **Dwfunction**の残りのバイトは0に設定されます。

 

 





