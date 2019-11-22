---
title: bDXVA_Func 変数
description: bDXVA_Func 変数
ms.assetid: 6db9fa71-7bc2-4eb6-afcb-b16df48f7e8b
keywords:
- ビデオデコード WDK DirectX VA、形式
- ビデオのデコード (WDK DirectX VA、形式)
- 画像デコード WDK DirectX VA、形式
- WDK DirectX VA の形式
- bDXVA_Func 変数 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b538fb2e2e9d7a276b9c264872e2b1af0c57d437
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839067"
---
# <a name="bdxva_func-variable"></a>bDXVA\_Func 変数


## <span id="ddk_bdxva_func_variable_gg"></span><span id="DDK_BDXVA_FUNC_VARIABLE_GG"></span>


**BDXVA\_Func**変数は、次のように、DirectX VA 操作に関連付けられた8ビット値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bDXVA_Func 値</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>圧縮された画像のデコード</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>アルファブレンドデータの読み込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>アルファブレンドの組み合わせ</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>画像の再サンプリング</p></td>
</tr>
</tbody>
</table>

 

**BDXVA\_Func**変数は、次のタスクを実行するために使用されます。

-   特定の DirectX VA 機能の構成をプローブしてロックします。 これを行うには、 **bDXVA\_Func**を**DXVA\_ConfigQueryOrReplyFlag**変数に含め、 **DXVA\_ConfigQueryOrReplyFlag**変数に追加します。これらの変数は、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)の呼び出しで、 [**DD\_rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバーで送信されます。

-   プローブまたはロックコマンドで渡された構成構造に関連付けられている関数を指定します。これには、次の構造体の**Dwfunction**メンバーで送信された**DXVA\_ConfigQueryOrReplyFlag**変数に**DXVA\_ConfigQueryOrReplyFlag**変数を含めます。 [**DXVA\_configpicture デコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode) [**for\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload)データ読み込み DXVA [ **\_ConfigAlphaLoad**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)アルファブレンドの組み合わせ
-   特定の DirectX VA 関数の暗号化プロトコルを初期化します。これには、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバーで送信される**DXVA\_EncryptProtocolFunc**変数に、を[*呼び出します。DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)。

-   暗号化プロトコルに関連付けられている関数を、 [**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)構造体の**dwfunction**メンバーに含めて指定します。

-   \_、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)の呼び出しで、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバーに含まれる一連の**bDXVA の Func** byte 値に含めることによって実行される操作を通知します。 最初の**bDXVA\_Func**操作は最上位バイトで指定され、次の操作は、次の最上位バイトに指定されます。 **Dwfunction**の残りのバイトは、操作が0に設定されていることを知らせるために使用されていません。

 

 





