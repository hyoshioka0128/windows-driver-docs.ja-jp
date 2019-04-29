---
title: アクセス制御リスト
description: アクセス制御リスト
ms.assetid: e682c2cc-ddd7-482b-b4f2-3e163d914752
keywords:
- WDK のセキュリティ記述子、ファイル システム アクセス制御リスト
- WDK の記述子、ファイル システム アクセス制御リスト
- アクセス制御リストの WDK ファイル システム
- ACL の WDK ファイル システム
- 随意 ACL WDK ファイル システム
- システム ACL WDK ファイル システム
- 必須のコントロール WDK ファイル システム
- WDK のファイル システムの保護されたオブジェクト
- オブジェクト セキュリティ WDK ファイル システム
- アクセス制御エントリの WDK ファイル システム
- ACE の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7e1c83f54da0f8fce1905d078080d171078cfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323141"
---
# <a name="access-control-list"></a>アクセス制御リスト


## <span id="ddk_access_control_list_if"></span><span id="DDK_ACCESS_CONTROL_LIST_IF"></span>


アクセス制御リスト (ACL) は、何らかの (保護された) 特定のオブジェクトに関連付けられているセキュリティ動作を制御するオペレーティング システムによって作成された Ace のリストです。 Windows では、Acl の 2 つの種類があります。

-   **随意 ACL**-これは、保護されているオブジェクトのアクセス権を表す 0 個以上の Ace のリスト。 アクセスが、所有者または適切な権限を持つすべてのユーザーの判断では許可されているために、随意です。

-   **システム ACL**-これは、監査をについて説明し、保護されているオブジェクトのポリシーのアラームを 0 個以上の Ace のリスト。

「任意」という用語は、必須および任意のコントロールの違いを指します。 必須のコントロールを使用する環境でオブジェクトの所有者のオブジェクトへのアクセスを許可していない場合があります。 任意の環境で、Windows など、オブジェクトの所有者は許可されてこのようなアクセスを許可します。 必須のコントロールは、通常、区画を持つセキュリティは、システムが同じシステム上のユーザー間で機密情報の漏えいを防ぐ必要がありますを使用している、非常に強固なセキュリティ環境に関連付けられます。

ACL を作成するドライバーは、いくつかの主要な手順に従ってください。

1.  ACL の記憶域を割り当てます。

2.  ACL を初期化します。

3.  ACL には、0 (または複数) の Ace を追加します。

次のコード例では、ACL を作成する方法を示します。

```cpp
    dacl = ExAllocatePool(PagedPool, PAGE_SIZE);
    if (!dacl) {
        return;
    }
    status = RtlCreateAcl(dacl, PAGE_SIZE, ACL_REVISION);
    if (!NT_SUCCESS(status)) {
        ExFreePool(dacl);
        return;
    }
```

前のコード フラグメントでは、空の ACL を作成します。 コード サンプルでは、ACL の必要なサイズがわからないために、大量のメモリが割り当てられます。

この時点では、ACE のエントリがあるないためには、ACL が空です。 空の ACL は、このようなアクセス権を付与するエントリがないため、オブジェクトにアクセスしようとしています。 すべてのユーザー アクセスを拒否します。 次のコード フラグメントでは、この ACL に ACE を追加します。

```cpp
    status = RtlAddAccessAllowedAce(dacl, ACL_REVISION,  FILE_ALL_ACCESS, SeExports->SeWorldSid);
    if (!NT_SUCCESS(status)) {
        ExFreePool(dacl);
        return;
    }
```

このエントリは、オブジェクトにアクセスするすべてのエンティティへのアクセスに与えるようになりました。 これは、他の Windows システム ユーティリティで"Everyone"アクセスと、通常、表される SID (SeWorldSid) アクセスの目的です。

Acl を作成するときに、順序へのアクセスが拒否 ACE エントリ、ACL の先頭にはことに注意してくださいし、アクセス許可 ACL の末尾に ACE エントリ。 これは、セキュリティ参照モニターが、ACL の評価が本物でアクセス拒否 Ace が見つかる前に、アクセスを許可する ACE が見つかるかどうかがあるためにです。 この動作が、Microsoft Windows SDK にも記載されているが、セキュリティ参照モニターを使用してアクセスを許可または拒否するかどうかを決定する特定のメカニズムに関連します。

 

 




