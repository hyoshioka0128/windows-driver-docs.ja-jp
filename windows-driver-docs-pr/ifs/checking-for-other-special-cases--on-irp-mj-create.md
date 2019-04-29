---
title: その他の特殊なケースで irp_mj_create 用のチェック
description: その他の特殊なケースで irp_mj_create 用のチェック
ms.assetid: e6af44c2-fd39-469b-8530-cf88edb329f7
keywords:
- IRP_MJ_CREATE
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae199707dd666930830389a644e4f366124bcc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386332"
---
# <a name="checking-for-other-special-cases-on-irpmjcreate"></a>IRP の他の特殊なケースについてチェック\_MJ\_を作成します。


## <span id="ddk_checking_for_other_special_cases_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_OTHER_SPECIAL_CASES_ON_IRP_MJ_CREATE_IF"></span>


その他の特殊なケースの処理は IRP の中に発生する必要があります\_MJ\_呼び出し元が SeChangeNotifyPrivilege を持っていない場合は、ファイル システム内で処理を作成します。 たとえば、そのファイルの ID またはオブジェクト ID を使用して開くことができるファイルでは、呼び出し元が走査ディレクトリ ツリーの構造を使用して、オブジェクトを取得するためのアクセス許可がないので、そのファイルへのパスを取得する呼び出し元が許可されて可能性があります。

この場合は、ファイル システムを検討することがあります。

-   **ファイル\_オープン\_BY\_ファイル\_ID** -ファイルの名前いない利用できるように、呼び出し元にします。 IRP の中に、ファイル システムで走査のアクセス許可についてを計算する必要がありますので、この情報 (アクセス許可の走査) では、作成操作中にのみ認識、ファイル情報のクエリの呼び出し中に利用できませんが、\_MJ\_作成します。

-   **SL\_オープン\_ターゲット\_ディレクトリ** : ターゲット ファイルが存在しない、ファイルの作成のアクセスには、ディレクトリを確認する必要があります。 ターゲットが存在する場合は、削除のアクセス確認が必要があります。 IRP の中に名前変更操作時に削除のアクセス チェックを実行する通常\_MJ\_設定\_情報の処理。

-   **ファイル\_優先的**と**ファイル\_上書き** -場合でも、呼び出し元が明示的に要求に破壊的な操作は、追加のアクセス権が必要です。 たとえば、ファイル システムでは、優先的操作を実行するために削除のアクセスを必要があります。

-   **ファイル\_作成**、**ファイル\_オープン\_場合**、および**ファイル\_上書き\_場合** 建設的な操作には、新しいオブジェクトが作成される親ディレクトリへのアクセスが必要です。 これは、格納されているディレクトリで、オブジェクト自体、およびそのため、以前に同様のコード サンプルではなく確認できます。

-   **SL\_FORCE\_アクセス\_確認** -カーネル モードではなく、ユーザー モードから呼び出す場合と、チェックを実行する必要がありますこの値が、I/O スタックの場所に設定されている場合。 そのため、セキュリティの監視ルーチンの呼び出しを指定する必要があります**UserMode**カーネル モードのサーバー内で、呼び出しが発生した場合でもです。

-   *ファイル/ディレクトリの削除* -ファイルの ACL の状態に基づいてこの可能性があります (たとえば、ファイル\_書き込み\_データ アクセスが暗黙的に削除を許可; 有効な削除がある場合は、データを削除します。ファイルのアクセス許可)、ディレクトリの ACL の状態と同様 (ファイル\_削除\_例については、格納されているディレクトリのアクセス許可を子)。

次のコード例は、特殊なケースのファイルの処理を示します\_優先的とファイル\_上書き、どちらの場合も、追加のアクセスが暗黙的に必要な呼び出し元によって要求されていなかった場合でもです。

```cpp
{
ULONG NewAccess = Supersede ? DELETE : FILE_WRITE_DATA;
ACCESS_MASK AddedAccess = 0;
PACCESS_MASK DesiredAccess = 
    &IrpSp->Paramters.Create.SecurityContext->DesiredAccess;

//
// If the caller does not have restore privilege, they must have write
// access to the EA and attributes for overwrite or supersede.
//
if (0 == (AccessState->Flags & TOKEN_HAS_RESTORE_PRIVILEGE)) {
    *DesiredAccess |= FILE_WRITE_EA | FILE_WRITE_ATTRIBUTES;

    //
    // Does the caller already have this access?
    //
    if (AccessState->PreviouslyGrantedAccess & NewAccess) {

        //
        // No - they need this as well
        //
        *DesiredAccess |= NewAccess;

    }

    //
    // Now check access using SeAccessCheck (omitted)
    //

}
```

このコード サンプルは、適切なファイル システムのポリシーが優先の例です。 呼び出し元が、削除のアクセスまたはファイルに要求しなかった\_書き込み\_データ アクセスがこのようなアクセスは、ファイル システムのセマンティクスをに基づいて実行される操作に固有です。

 

 




