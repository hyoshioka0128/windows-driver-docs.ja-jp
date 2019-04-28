---
title: ib、iw、id (ポートから入力)
description: Ib、インフォメーション ワーカー、および id のコマンドは、読み取りし、バイト、単語、または選択したポートからダブル ワードを表示します。
ms.assetid: 68f9e0c2-3cfd-46e1-a513-5a96c93de63c
keywords:
- ib、インフォメーション ワーカーは、id (ポートからの入力) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ib, iw, id (Input from Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b7e5a6658f9bcb46e0e5e3616e3f7ef3c3a56f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381035"
---
# <a name="ib-iw-id-input-from-port"></a>ib、iw、id (ポートから入力)


**Ib**、 **iw**、および**id**コマンドは、読み取り、バイト、単語、または選択したポートからダブル ワードを表示します。

```dbgcmd
ib Address 
iw Address 
id Address
```

## <a name="span-idddkcmdinputfromportdbgspanspan-idddkcmdinputfromportdbgspanparameters"></a><span id="ddk_cmd_input_from_port_dbg"></span><span id="DDK_CMD_INPUT_FROM_PORT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ポートのアドレス。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>x86 ベースのコンピューターのみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Ib**コマンドは、1 バイトを読み取ります、 **iw**コマンド、単語の読み取りおよび**id**コマンドは、ダブル ワードを読み取ります。

読み取りを行っているデバイスの動作に影響しません、I/O ポートを読み取っていることを確認します。 一部のデバイスは、読み取り専用のポートが読み取られた後に状態を変更します。 必要がありますもないしようとするこの長さの値が許可されないポートから word またはダブル ワードを読み取る。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**ob、od、ow (ポートに出力)**](ob--ow--od--output-to-port-.md)

 

 






