---
title: net_send
description: Net_send 拡張機能は、ローカル ネットワーク経由でメッセージを送信します。
ms.assetid: 13d5fe3f-6477-4610-8928-020726ccb3c8
keywords:
- ネットワーク メッセージ
- Windows デバッグ net_send
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- net_send
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be6e30c5a3abe6024ac5edefc6dc383d86d7873a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574142"
---
# <a name="netsend"></a>! net\_送信


**! Net\_送信**拡張機能は、ローカル ネットワーク経由でメッセージを送信します。

```dbgcmd
!net_send SendingMachine TargetMachine Sender Message
```

## <a name="span-idddknetsenddbgspanspan-idddknetsenddbgspanparameters"></a><span id="ddk__net_send_dbg"></span><span id="DDK__NET_SEND_DBG"></span>パラメーター


<span id="_______SendingMachine______"></span><span id="_______sendingmachine______"></span><span id="_______SENDINGMACHINE______"></span> *SendingMachine*   
コマンドを処理しているコンピューターを指定します。 これが、デバッガーは、それ以外の場合、メッセージを送信する、ネットワークの構成が拒否されることがあるためで実行されているコンピューターの名前をあることをお勧めします。 *SendingMachine*バック スラッシュを含めることはできません (\\\)します。

<span id="_______TargetMachine______"></span><span id="_______targetmachine______"></span><span id="_______TARGETMACHINE______"></span> *切り替わりません*   
メッセージの送信先となるコンピューターを指定します。 *切り替わりません*バック スラッシュを含めることはできません (\\\)します。

<span id="_______Sender______"></span><span id="_______sender______"></span><span id="_______SENDER______"></span> *送信者*   
メッセージの送信者を指定します。 推奨されます*送信者*と同じにする*SendingMachine*、それ以外の場合、メッセージを送信する、ネットワークの構成が拒否されることがあるためです。 メッセージが表示されたら、この文字列は、メッセージの送信者として識別されます。

<span id="_______Message______"></span><span id="_______message______"></span><span id="_______MESSAGE______"></span> *メッセージ*   
メッセージ自体を指定します。 すべてのテキストの後、*送信者*パラメーターの一部として扱われます*メッセージ*が、スペースや引用符を含む、 [**セミコロン**](----command-separator-.md)は終了*メッセージ*し、新しいコマンドを開始します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





