---
title: sd
description: Sd 拡張機能では、指定したアドレスにセキュリティ記述子を表示します。
ms.assetid: 67c72bdb-7bfc-42d6-9b65-31a07dc67729
keywords:
- sd の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6a19fabf60c052308b7e5b3d8254143339615c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550719"
---
# <a name="sd"></a>! sd


**! Sd**拡張機能は、指定したアドレスにセキュリティ記述子を表示します。

構文

```dbgcmd
!sd Address [Flags] 
```

## <a name="span-idddksddbgspanspan-idddksddbgspanparameters"></a><span id="ddk__sd_dbg"></span><span id="DDK__SD_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
セキュリティの 16 進数のアドレスを指定します\_記述子構造体。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
これは、1 に設定されている場合は、フレンドリ名が表示されます。 これには、セキュリティ識別子 (SID) の種類と、SID のドメインとユーザー名が含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アプリケーションとこのコマンドの例では、次を参照してください。[オブジェクトの ACL の決定](determining-the-acl-of-an-object.md)します。 セキュリティ記述子の詳細については、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 参照してください[ **! sid** ](-sid.md)と[ **! acl**](-acl.md)します。

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
kd> !sd e1a96a80 1
->Revision: 0x1
->Sbz1    : 0x0
->Control : 0x8004
            SE_DACL_PRESENT
            SE_SELF_RELATIVE
->Owner   : S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)
->Group   : S-1-5-21-518066528-515770016-299552555-513 (Group: MYDOMAIN\Domain Users)
->Dacl    :
->Dacl    : ->AclRevision: 0x2
->Dacl    : ->Sbz1       : 0x0
->Dacl    : ->AclSize    : 0x40
->Dacl    : ->AceCount   : 0x2
->Dacl    : ->Sbz2       : 0x0
->Dacl    : ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[0]: ->AceFlags: 0x0
->Dacl    : ->Ace[0]: ->AceSize: 0x24
->Dacl    : ->Ace[0]: ->Mask : 0x001f0003
->Dacl    : ->Ace[0]: ->SID: S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)

->Dacl    : ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[1]: ->AceFlags: 0x0
->Dacl    : ->Ace[1]: ->AceSize: 0x14
->Dacl    : ->Ace[1]: ->Mask : 0x001f0003
->Dacl    : ->Ace[1]: ->SID: S-1-5-18 (Well Known Group: NT AUTHORITY\SYSTEM)

->Sacl    :  is NULL
```

 

 





