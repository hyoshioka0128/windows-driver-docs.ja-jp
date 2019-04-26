---
title: オブジェクトの ACL の判別
description: オブジェクトの ACL の判別
ms.assetid: 8dcd4f5a-1415-4a58-bfb1-fd3cbd58cc56
keywords:
- アクセス制御リスト (ACL)
- ACL (アクセス制御リスト)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e43c405d40b0768ac348dc0aeed0be372a5529b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346308"
---
# <a name="determining-the-acl-of-an-object"></a>オブジェクトの ACL の判別


## <span id="ddk_determining_the_acl_of_an_object_dbg"></span><span id="DDK_DETERMINING_THE_ACL_OF_AN_OBJECT_DBG"></span>


デバッガーを使用すると、オブジェクトのアクセス制御リスト (ACL) を確認します。

カーネル デバッグを実行している場合は、次のメソッドを使用できます。 これを使用して、ユーザー モードのデバッグを実行している間、コントロールをカーネル デバッガーにリダイレクトする必要があります。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

まず、使用して、 [ **! オブジェクト**](-object.md)デバッガー拡張機能を対象のオブジェクトの名前。

```dbgcmd
kd> !object \BaseNamedObjects\AgentToWkssvcEvent
Object: ffbb8a98  Type: (80e30e70) Event
    ObjectHeader: ffbb8a80
    HandleCount: 2  PointerCount: 3
    Directory Object: e14824a0  Name: AgentToWkssvcEvent
```

これは、アドレス 0xFFBB8A80 をオブジェクトのヘッダーがあることを示しています。 使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドには、このアドレスと**nt!\_オブジェクト\_ヘッダー**構造体名。

```dbgcmd
kd> dt nt!_OBJECT_HEADER ffbb8a80
   +0x000 PointerCount     : 3
   +0x004 HandleCount      : 2
   +0x004 NextToFree       : 0x00000002
 +0x008 Type             : 0x80e30e70
   +0x00c NameInfoOffset   : 0x10 '
 +0x00d HandleInfoOffset : 0 '
   +0x00e QuotaInfoOffset  : 0 '
   +0x00f Flags            : 0x20 ' '
   +0x010 ObjectCreateInfo : 0x8016b460
   +0x010 QuotaBlockCharged : 0x8016b460
   +0x014 SecurityDescriptor : 0xe11f08b6
   +0x018 Body             : _QUAD
```

セキュリティ記述子のポインター値は、0xE11F08B6 として表示されます。 この値の最下位の 3 つのビットは、それらを無視するために過去のこの構造体の先頭オフセットを表します。 つまり、セキュリティ\_0xE11F08B6 で記述子構造体が実際に開始されます (& a) ~ 0x7 します。 使用して、 [ **! sd** ](-sd.md)このアドレスで拡張機能。

```dbgcmd
kd> !sd e11f08b0
->Revision: 0x1
->Sbz1    : 0x0
->Control : 0x8004
            SE_DACL_PRESENT
 SE_SELF_RELATIVE
->Owner   : S-1-5-32-544
->Group   : S-1-5-18
->Dacl    : 
->Dacl    : ->AclRevision: 0x2
->Dacl    : ->Sbz1       : 0x0
->Dacl    : ->AclSize    : 0x44
->Dacl    : ->AceCount   : 0x2
->Dacl    : ->Sbz2       : 0x0
->Dacl    : ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[0]: ->AceFlags: 0x0
->Dacl    : ->Ace[0]: ->AceSize: 0x14
->Dacl    : ->Ace[0]: ->Mask : 0x001f0003
->Dacl    : ->Ace[0]: ->SID: S-1-5-18

->Dacl    : ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[1]: ->AceFlags: 0x0
->Dacl    : ->Ace[1]: ->AceSize: 0x18
->Dacl    : ->Ace[1]: ->Mask : 0x00120001
->Dacl    : ->Ace[1]: ->SID: S-1-5-32-544

->Sacl    :  is NULL
```

これには、このオブジェクトのセキュリティ情報が表示されます。

 

 





