---
title: dskheap
description: Dskheap 拡張機能は、指定されたセッションのデスクトップヒープ情報を表示します。
ms.assetid: e49c816f-963c-4383-a3bf-c03b2c0cfa39
keywords:
- デスクトップ
- dskheap Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dskheap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f640ae7501110efd8c1bba2def61cf2e6dc72b32
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025260"
---
# <a name="dskheap"></a>!dskheap


**! Dskheap**拡張機能は、指定されたセッションのデスクトップヒープ情報を表示します。

```dbgcmd
!dskheap [-v] [-s SessionID]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
表示により詳細な出力が含まれるようにします。

<span id="_______-s_SessionID"></span><span id="_______-s_sessionid"></span><span id="_______-S_SESSIONID"></span> **-s** ****  *SessionID*  
セッションを指定します。 このパラメーターを省略すると、セッション0のデスクトップヒープ情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デスクトップまたはデスクトップヒープの詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンによる*Microsoft Windows の内部構造*に関するドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

セッションのデスクトップヒープ情報は、ウィンドウステーション別に配置されます。

次に例をいくつか示します。

```dbgcmd
kd> !dskheap -s 3
##   Winstation\Desktop            Heap Size(KB)   Used Rate(%)

  WinSta0\Screen-saver              3072                 0%
  WinSta0\Default                   3072                 0%
  WinSta0\Disconnect                  64                 4%
##   WinSta0\Winlogon                   128                 5%

                Total Desktop: (    6336 KB -   4 desktops)
#                 Session ID:  3

kd> !dskheap
##   Winstation\Desktop            Heap Size(KB)   Used Rate(%)

  WinSta0\Default                   3072                 0%
  WinSta0\Disconnect                  64                 4%
  WinSta0\Winlogon                   128                 9%
  Service-0x0-3e7$\Default           512                 4%
  Service-0x0-3e5$\Default           512                 0%
  Service-0x0-3e4$\Default           512                 1%
##   SAWinSta\SADesktop                 512                 0%

                Total Desktop: (    5312 KB -   7 desktops)
#                 Session ID:  0
```









