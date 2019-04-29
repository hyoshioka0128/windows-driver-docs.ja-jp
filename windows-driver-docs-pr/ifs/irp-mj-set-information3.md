---
title: IRP_MJ_SET_INFORMATION
description: IRP_MJ_SET_INFORMATION
ms.assetid: 2a6c837c-85c9-46d8-85d8-d779f22be54e
keywords:
- IRP_MJ_SET_INFORMATION
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、IRP_MJ_SET_INFORMATION を確認します。
- WDK のファイル システム操作の名前を変更します。
- ハード リンク操作 WDK ファイル システム
- WDK の名前のファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f39466824de162db2b0b1e47447960bccaebe7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324468"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


名前の変更とハード リンクのケース セットの情報は、特定の状況でのセキュリティ チェックを必要があります。 具体的には、呼び出し元を設定して、名前の変更またはハード リンクのターゲットを削除する必要がある場合、 **ReplaceIfExists**フィールドを**TRUE**、ファイル システムは、呼び出し元が持つようにするためのセキュリティ チェックを実行する必要がありますターゲットを削除する適切なアクセスを許可します。 さらに、することができます、ファイル システム、ポリシーの問題として望んでいないこの方法で削除することを許可するファイルの特定の種類 (レジストリ ハイブとページング ファイル、たとえば)。 次のコード例では、呼び出し元がファイルを削除する適切なセキュリティ権限を持つかどうかを決定します。

```cpp
NTSTATUS FsdCheckDeleteFileAccess(POW_IRP_CONTEXT IrpContext, 
                                  PSECURITY_DESCRIPTOR targetSD, 
                                  PFCB ParentFcb)
{
    SECURITY_SUBJECT_CONTEXT SubjectContext;
    BOOLEAN Granted;
    NTSTATUS status = STATUS_SUCCESS;
    PPRIVILEGE_SET Privileges = NULL;
    ACCESS_MASK GrantedAccess;

    //
    // See if the user has DELETE access to the target.
    //
    SeCaptureSubjectContext( &SubjectContext );

    SeLockSubjectContext( &SubjectContext );

    Granted = SeAccessCheck(targetSD,           // Target's SD.
                            &SubjectContext,    // Captured security context.
                            TRUE,               // Tokens are locked.
                            DELETE,             // we only care about delete 
                            0,                  // previously granted access.
                            &Privileges,        // privilege_set
                            IoGetFileObjectGenericMapping(), // Generic mappings.
                            UserMode,           // Mode
                            &GrantedAccess,     // Granted access mask
                            &status );          // Error code

    //
    // Do not need privilege set, so release it.
    //
    if (Privileges != NULL) { 

        SeFreePrivileges( Privileges ); 
        Privileges = NULL;
    }

    if (!Granted) {

        status = STATUS_SUCCESS;

        //
        // The user does not have DELETE access to the target, but 
        // could have FILE_DELETE_CHILD access to the parent directory.
        //
        (void) FsdLoadSecurityDescriptor(IrpContext, ParentFcb);
        if (!ParentFcb->SecurityDescriptor) {
            //
            // fine - no security is fine - he gets to do what he wants 
            //
            SeUnlockSubjectContext( &SubjectContext );
            SeReleaseSubjectContext( &SubjectContext );
            return STATUS_SUCCESS;
        }

 
        Granted = SeAccessCheck(&ParentFcb->SecurityDescriptor,
                                &SubjectContext,   // Captured security context.
                                TRUE,              // Tokens are locked.
                                FILE_DELETE_CHILD, // we only care about delete 
                                0,                 // Previously granted access.
                                &Privileges,       // privilege_set
                                IoGetFileObjectGenericMapping(), // Generic mappings
                                UserMode,          // mode
                                &GrantedAccess,    // Granted access mask
                                &status );         // Error code
        //
        // Release privileges
        //
        if (Privileges != NULL) { 
            SeFreePrivileges( Privileges ); 
            Privileges = NULL;
        }
    }
    SeUnlockSubjectContext( &SubjectContext );
    SeReleaseSubjectContext( &SubjectContext );
    return status;
}
```

このコードは、名前の変更とハード リンクの作成の場合に使用できます。

削除されるファイルの種類に基づいて、削除を禁止するファイル システムを決定する、ポリシー レベル コードについて説明するには、このドキュメントのスコープの外側では注意してください。

 

 




