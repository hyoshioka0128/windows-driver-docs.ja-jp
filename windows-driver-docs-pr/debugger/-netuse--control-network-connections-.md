---
title: .netuse (ネットワーク接続の制御)
description: .Netuse コマンドは、ネットワーク共有への接続を追加します。
ms.assetid: f27e5ae5-1beb-4d2b-987e-5e91d0742e2d
keywords:
- .netuse (コントロール ネットワーク接続) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .netuse (Control Network Connections)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9574f14e6be8e9f5805337786f30f63f49a30acb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570837"
---
# <a name="netuse-control-network-connections"></a>.netuse (ネットワーク接続の制御)


**.Netuse**コマンドは、ネットワーク共有への接続を追加します。

```dbgcmd
.netuse /a "[Local]" "Remote" "[User]" "[Password]" 
```

## <a name="span-idddkmetacontrolnetworkconnectionsdbgspanspan-idddkmetacontrolnetworkconnectionsdbgspanparameters"></a><span id="ddk_meta_control_network_connections_dbg"></span><span id="DDK_META_CONTROL_NETWORK_CONNECTIONS_DBG"></span>パラメーター


<span id="________a______"></span><span id="________A______"></span> **/a**   
新しい接続を追加します。 常に使用する必要があります、 **/a**スイッチします。

<span id="_______Local______"></span><span id="_______local______"></span><span id="_______LOCAL______"></span> *地元の*   
接続に使用するドライブ文字を指定します。 囲む必要があります*ローカル*引用符で囲んで指定します。 このパラメーターを省略した場合は、パラメーターとして空の 1 対の引用符を含める必要があります。

<span id="_______Remote______"></span><span id="_______remote______"></span><span id="_______REMOTE______"></span> *リモート*   
接続されている共有の UNC パスを指定します。 囲む必要があります*リモート*引用符で囲んで指定します。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span> *ユーザー*   
接続を確立するために権限を持つアカウントのユーザー名を指定します。 囲む必要があります*ユーザー*引用符で囲んで指定します。 このパラメーターを省略した場合は、パラメーターとして空の 1 対の引用符を含める必要があります。

<span id="_______Password______"></span><span id="_______password______"></span><span id="_______PASSWORD______"></span> *パスワード*   
関連付けられているパスワードを指定します、*ユーザー*アカウント。 囲む必要があります*パスワード*引用符で囲んで指定します。 このパラメーターを省略した場合は、パラメーターとして空の 1 対の引用符を含める必要があります。

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**.Netuse**コマンドのように動作、 **net** Microsoft MS-DOS コマンド。

使用する場合 **.netuse**リモートのデバッグ セッション中にこのコマンドはデバッグのクライアントではなく、デバッグ、サーバーに影響します。

このコマンドは、次の例です。

```dbgcmd
0:000> .netuse "m:" "\\myserver\myshare" "" "" 
```

 

 





