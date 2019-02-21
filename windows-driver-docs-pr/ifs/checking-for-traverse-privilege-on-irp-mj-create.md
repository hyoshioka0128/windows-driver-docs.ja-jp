---
title: Irp_mj_create 用の走査の権限のチェック
description: Irp_mj_create 用の走査の権限のチェック
ms.assetid: 9ba743d6-8e78-4f9a-9cb8-cb98f734c290
keywords:
- IRP_MJ_CREATE
- WDK のファイル システムの特権を走査します。
- セキュリティは、WDK のファイル システム、irp_mj_create 用を確認します。
- WDK のファイル システム権限
- WDK のファイル システムのパス
- 汎用的なセキュリティは、WDK のファイル システムを確認します。
- SeChangeNotifyPrivilege
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06de785fdbbed8272e54d7c7df2047cd0b159266
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530641"
---
# <a name="checking-for-traverse-privilege-on-irpmjcreate"></a>IRP の走査の権限のチェック\_MJ\_を作成します。


## <span id="ddk_checking_for_traverse_privilege_on_irp_mj_create_if"></span><span id="DDK_CHECKING_FOR_TRAVERSE_PRIVILEGE_ON_IRP_MJ_CREATE_IF"></span>


懸念事項の 1 つ[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)チェックは、呼び出し元が走査特権を持っているかどうか (には、呼び出し元がオブジェクトへのパスにアクセスする権限)。 ほとんどの呼び出し元に走査特権があるためにを走査特権ファイル システム内で通常実行される最初のチェックのいずれかの確認しています。

```cpp
    BOOLEAN traverseCheck = 
        !(IrpContext->IrpSp->Parameters.Create.SecurityContext->AccessState->Flags
            & TOKEN_HAS_TRAVERSE_PRIVILEGE);
```

走査の権限の確認が I/O マネージャーから、ファイル システムに渡される状態情報に依存して ことに注意してください。 この情報は、呼び出し元が SeChangeNotifyPrivilege を保持するかどうかに基づいています。 呼び出し元がこの特権を保持しない場合は、各ディレクトリの走査チェックを実行してください。 走査チェック次の例でを汎用ルーチンを使用して行う、通常ほとんどのセキュリティ チェックの使用します。

{

```cpp
    SeLockSubjectContext(
        &accessParams.AccessState->SubjectSecurityContext);
//
// Note: AccessParams is passed to us and is normally based on
//       the fields of the same name from the IRP
//

    granted = SeAccessCheck( Fcb->SecurityDescriptor,
        &AccessParams.AccessState->SubjectSecurityContext,
        TRUE,
        AccessParams.desiredAccess,
        0,
        &Privileges,
        IoGetFileObjectGenericMapping(),
        AccessParams.AccessMode,
        &AccessParams.GrantedAccess,
        &AccessParams.status );

    if (Privileges != NULL) {
        //
        // this changes the AccessState
        //
        (void) SeAppendPrivileges(AccessParams.AccessState, Privileges );
        SeFreePrivileges( Privileges );
        Privileges = NULL;
    }

    if (granted) {
        //
        // delete granted bits from desired bits
        //
        AccessParams.desiredAccess &= 
            ~(AccessParams.GrantedAccess | MAXIMUM_ALLOWED);
 
        if (!checkOnly) {
        //
        // the caller wants to modify the access state for this 
        // request
        //
            AccessParams.AccessState->PreviouslyGrantedAccess |= 
                AccessParams.GrantedAccess;

        if (maxDesired) {

            maxDelete = 
                (BOOLEAN)(AccessParams.AccessState->PreviouslyGrantedAccess & 
                    DELETE);
            maxReadAttr = 
                (BOOLEAN)(AccessParams.AccessState->PreviouslyGrantedAccess & 
                    FILE_READ_ATTRIBUTES);
        }
        AccessParams.AccessState->RemainingDesiredAccess &= 
            ~(AaccessParams.GrantedAccess | MAXIMUM_ALLOWED);
    }
    SeUnlockSubjectContext(&accessParams.AccessState->SubjectSecurityContext);  
}
```

この関数は、汎用的なセキュリティ チェックを実行します。 この関数は、その際に、次の問題を扱う必要があります。

-   チェックに使用する適切なセキュリティ記述子を指定する必要がある必要があります。

-   (これらは、操作を実行するエンティティの資格情報) のセキュリティ コンテキストに渡す必要があります。

-   セキュリティ チェックの結果に基づくアクセスの状態更新する必要があります。

-   最大値を考慮する必要があります\_許可されているオプション (詳細については、WDK を含むファイルを含める ntifs.h を参照してください)。 最大\_許可オプションは、ファイル システムがファイル システムで許可されている最大の可能なアクセスをアクセスを設定する必要がありますを指定します (読み取り/書き込み/削除など)。 ほとんどのアプリケーションでは、最大使用\_許可オプション FASTFAT ファイル システムでは、このオプションはサポートされていないためです。 最大\_許可されているオプションのビットがない、FASTFAT ファイル システムが認識するアクセス ビットのいずれか、指定されたファイルへのアクセス要求を拒否します。 最大値を使用して FASTFAT ボリューム上のファイルを開こうとするアプリケーション\_許可されているオプション セットは、要求が失敗したことを検索します。 詳細については、次を参照してください。、 **FatCheckFileAccess** 、WDK を含む FASTFAT サンプル コードの Acchksup.c ソース ファイル内の関数。

単純な走査チェックの要求のアクセス権があるファイルに注意してください\_走査とセキュリティ記述子であるディレクトリのを通過する元の IRPからのアクセスを要求しないため、呼び出し元が試みているを通じて\_。MJ\_IRP を作成します。

 

 




