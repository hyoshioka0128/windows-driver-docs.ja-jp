---
title: bDXVA_Func 変数
description: bDXVA_Func 変数
ms.assetid: 6db9fa71-7bc2-4eb6-afcb-b16df48f7e8b
keywords:
- ビデオのデコード WDK DirectX va なので、書式設定します。
- ビデオの WDK DirectX va なので、形式のデコード
- WDK の DirectX va なので、形式をデコードする画像
- WDK DirectX VA を書式設定します。
- bDXVA_Func 変数 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92174b1651c0da6fc2ec8496930572a716848ee4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558208"
---
# <a name="bdxvafunc-variable"></a>bDXVA\_Func 変数


## <span id="ddk_bdxva_func_variable_gg"></span><span id="DDK_BDXVA_FUNC_VARIABLE_GG"></span>


**BDXVA\_Func**変数は、次のように DirectX VA 操作に関連付けられている 8 ビット値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bDXVA_Func Value</th>
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
<td align="left"><p>アルファ ブレンド データの読み込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>アルファ ブレンドの組み合わせ</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>画像が再サンプリングします</p></td>
</tr>
</tbody>
</table>

 

**BDXVA\_Func**変数は、次のタスクを実行するために使用します。

-   プローブし、特定の DirectX VA 機能の構成をロックします。 これを行うなどを**bDXVA\_Func**で、 **DXVA\_ConfigQueryOrReplyFlag**変数と、 **DXVA\_ConfigQueryOrReplyFlag**変数これらの変数が送信されると、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)への呼び出しで構造体[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。

-   含めることによって、プローブまたはロック コマンドで渡される構成構造に関連付けられている関数を指定する**DXVA\_ConfigQueryOrReplyFlag**で変数を**DXVA\_ConfigQueryOrReplyFlag**で送信される変数、 **dwFunction**以下の構造体のメンバー。[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)を圧縮する画像のデコード[ **DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129) を読み込み、アルファブレンドデータ[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126)アルファ ブレンドの組み合わせ
-   含めることによって、特定の DirectX VA 関数の暗号化プロトコルの初期化、 **DXVA\_EncryptProtocolFunc**で送信される変数、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体への呼び出しで[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。

-   含めることで、暗号化プロトコルに関連付けられている関数を指定、 **dwFunction**のメンバー、 [ **DXVA\_EncryptProtocolHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff563965)構造体。

-   一連の信頼で実行される操作の通知**bDXVA\_Func**バイト値、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体への呼び出しで[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)します。 最初の**bDXVA\_Func**操作は、最上位バイトで指定されて、次の操作を指定で、[次へ] 最上位バイト、します。 残りのバイト**dwFunction**通知操作が 0 に設定するのには使用されません。

 

 





