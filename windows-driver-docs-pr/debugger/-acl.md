---
title: acl
description: Acl の拡張機能では、書式設定し、アクセス制御リスト (ACL) の内容を表示します。
ms.assetid: 591f56b6-5a70-4037-a285-a1bffd5bd387
keywords:
- acl が Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- acl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d54dc14c65e72cd0ca43b4536305ea354bedc0f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527896"
---
# <a name="acl"></a>! acl


**! Acl**拡張機能は、書式設定し、アクセス制御リスト (ACL) の内容を表示します。

構文

```dbgcmd
    !acl Address [Flags] 
```

## <a name="span-idddkacldbgspanspan-idddkacldbgspanparameters"></a><span id="ddk__acl_dbg"></span><span id="DDK__ACL_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ACL の 16 進数のアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
場合、ACL のフレンドリ名を表示の値*フラグ*は 1 です。 このフレンドリ名には、セキュリティ識別子 (SID) の種類と、SID のドメインとユーザー名が含まれています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アクセス制御リストの詳細については、次を参照してください[ **! sid**](-sid.md)、 [ **! sd**](-sd.md)、および[オブジェクトの ACL の決定。](determining-the-acl-of-an-object.md). また、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

次の例は、 **! acl**拡張機能。

```console
kd> !acl e1bf35d4 1
ACL is:
ACL is: ->AclRevision: 0x2
ACL is: ->Sbz1       : 0x0
ACL is: ->AclSize    : 0x40
ACL is: ->AceCount   : 0x2
ACL is: ->Sbz2       : 0x0
ACL is: ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
ACL is: ->Ace[0]: ->AceFlags: 0x0
ACL is: ->Ace[0]: ->AceSize: 0x24
ACL is: ->Ace[0]: ->Mask : 0x10000000
ACL is: ->Ace[0]: ->SID: S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)

ACL is: ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
ACL is: ->Ace[1]: ->AceFlags: 0x0
ACL is: ->Ace[1]: ->AceSize: 0x14
ACL is: ->Ace[1]: ->Mask : 0x10000000
ACL is: ->Ace[1]: ->SID: S-1-5-18 (Well Known Group: NT AUTHORITY\SYSTEM)
```

 

 





