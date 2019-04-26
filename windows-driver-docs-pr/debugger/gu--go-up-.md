---
title: gu (完了まで実行)
description: Gu コマンドでは、現在の関数が完了するまでに実行するターゲットを実行します。
ms.assetid: 10022292-92a4-4663-b277-26aa3c0d73a7
keywords:
- gu (移動する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gu (Go Up)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 840c33d31bc3bf7358d7fdda939a35d0f2a8bea6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342029"
---
# <a name="gu-go-up"></a>gu (完了まで実行)


**Gu**コマンドにより、現在の関数が完了するまでに実行するターゲット。

ユーザー モードの構文

```dbgcmd
[~Thread] gu 
```

カーネル モードの構文

```dbgcmd
gu
```

## <a name="span-idddkcmdgoupdbgspanspan-idddkcmdgoupdbgspanparameters"></a><span id="ddk_cmd_go_up_dbg"></span><span id="DDK_CMD_GO_UP_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
(ユーザー モードのみ)スレッドの実行を指定します。 このスレッドは、例外によって停止している必要があります。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

このコマンドと、関連するコマンドの概要を発行するには、他の方法を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

**Gu**コマンドは、現在の関数呼び出しが戻るまでにターゲットを実行します。

再帰的に、現在の関数が呼び出された場合、 **gu**コマンドまでの実行は停止されます、*現在インスタンス*現在の関数を返します。 この方法で**gu**とは異なります**g @$ ra**、いつでもこの関数の戻り値のアドレスをヒットを停止します。

**注**   、 **gu**コマンド呼び出しスタックの深さを測定することによって、関数の別のインスタンスを区別します。 引数と呼び出しの直前にスタックにプッシュされた後にモードのアセンブリでこのコマンドを実行すると、この測定値が正しくないありますにする場合があります。 コンパイラによって最適化関数を返します。 同様にこの戻り値の正しくないインスタンスで停止するには、このコマンドがあります。 これらのエラーは、まれで、再帰関数の呼び出し中にのみ発生することができます。

 

場合*スレッド*が指定されている、 **gu**コマンドを実行すると、指定されたスレッドのフリーズとフリーズ他のすべて。 たとえば場合、 **~ 123gu**、  **~ \#gu**、または **~ \*gu**コマンドを指定すると、指定されたスレッド固定されたでない他のすべてのユーザーが固定されているとします。

 

 





