---
title: threadtoken
description: Threadtoken 拡張機能は、現在のスレッドの偽装状態を表示します。
ms.assetid: df16bdb5-0834-4e07-ad5f-a712f9282bb0
keywords:
- threadtoken Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- threadtoken
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b43026e988abdcd6cb5f9d5b2358a2f42cb5baf
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025156"
---
# <a name="threadtoken"></a>!threadtoken


**! Threadtoken**拡張機能は、現在のスレッドの偽装状態を表示します。

```dbgcmd
!threadtoken
```

## <span id="ddk__threadtoken_dbg"></span><span id="DDK__THREADTOKEN_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts .dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドと権限借用の詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンによる*Microsoft Windows の内部構造*を参照してください。

<a name="remarks"></a>コメント
-------

**! Threadtoken**拡張機能は、windows XP 以降のバージョンの windows では廃止されています。 代わりに[ **! token**](-token.md)を使用してください。

現在のスレッドが偽装している場合は、このスレッドが使用しているトークンが表示されます。

それ以外の場合は、"スレッドが偽装されていません" というメッセージが表示されます。 次に、プロセストークンが表示されます。

トークンは、トークン[**ハンドル**](-handle.md)を表示するときにが使用するのと同じ形式で表示されます。

以下に例を示します。

```dbgcmd
0:000> ~
.  0  id: 1d0.55c   Suspend: 1 Teb 7ffde000 Unfrozen
#  1  id: 1d0.1a4   Suspend: 1 Teb 7ffdd000 Unfrozen

0:000> !threadtoken

***Thread is not impersonating, using process token***
    Auth Id    0 : 0x1c93d
    Type       Primary
    Imp Level  Anonymous
     Token Id  0 : 0x5e8c19
     Mod Id    0 : 0x5e8c12
     Dyn Chg   0x1f4
     Dyn Avail 0x1a4
     Groups    26
     Privs     17
     User      S-1-5-21-2127521184-1604012920-1887927527-74790
     Groups    26
               S-1-5-21-2127521184-1604012920-1887927527-513
               S-1-1-0
               S-1-5-32-544
               S-1-5-32-545
               S-1-5-21-2127521184-1604012920-1887927527-277551
               S-1-5-21-2127521184-1604012920-1887927527-211604
               S-1-5-21-2127521184-1604012920-1887927527-10546
               S-1-5-21-2127521184-1604012920-1887927527-246657
               S-1-5-21-2127521184-1604012920-1887927527-277552
               S-1-5-21-2127521184-1604012920-1887927527-416040
               S-1-5-21-2127521184-1604012920-1887927527-96548
               S-1-5-21-2127521184-1604012920-1887927527-262644
               S-1-5-21-2127521184-1604012920-1887927527-155802
               S-1-5-21-2127521184-1604012920-1887927527-158763
               S-1-5-21-2127521184-1604012920-1887927527-279132
               S-1-5-21-2127521184-1604012920-1887927527-443952
               S-1-5-21-2127521184-1604012920-1887927527-175772
               S-1-5-21-2127521184-1604012920-1887927527-388472
               S-1-5-21-2127521184-1604012920-1887927527-443950
               S-1-5-21-2127521184-1604012920-1887927527-266975
               S-1-5-21-2127521184-1604012920-1887927527-158181
               S-1-5-21-2127521184-1604012920-1887927527-279435
               S-1-5-5-0-116804
               S-1-2-0
               S-1-5-4
               S-1-5-11
     Privileges    17
               SeUndockPrivilege ( Enabled Default )
               SeTakeOwnershipPrivilege ( )
               SeShutdownPrivilege ( )
               SeDebugPrivilege ( )
               SeIncreaseBasePriorityPrivilege ( )
               SeAuditPrivilege ( )
               SeSyncAgentPrivilege ( )
               SeLoadDriverPrivilege ( )
               SeSystemEnvironmentPrivilege ( Enabled )
               SeRemoteShutdownPrivilege ( )
               SeProfileSingleProcessPrivilege ( )
               SeCreatePagefilePrivilege ( )
               SeCreatePermanentPrivilege ( )
               SeSystemProfilePrivilege ( Enabled )
               SeBackupPrivilege ( )
               SeMachineAccountPrivilege ( )
               SeEnableDelegationPrivilege ( Enabled )
```

 

 





