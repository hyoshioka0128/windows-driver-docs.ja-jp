---
title: IRP_MJ_SET_INFORMATION (IFS)
description: IRP_MJ_SET_INFORMATION
ms.assetid: 2a6c837c-85c9-46d8-85d8-d779f22be54e
keywords:
- IRP_MJ_SET_INFORMATION
- セキュリティ WDK ファイルシステム、セキュリティチェックの追加
- セキュリティチェック WDK ファイルシステム、IRP_MJ_SET_INFORMATION
- 名前変更の操作 (WDK ファイルシステム)
- ハードリンク操作 WDK ファイルシステム
- WDK ファイルシステムの名前
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a1cd88248b1c7a328fb18f7f71cd2be7423500
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141320"
---
# <a name="irp_mj_set_information-ifs"></a>IRP_MJ_SET_INFORMATION (IFS)

設定情報の名前変更とハードリンクのケースでは、特定の状況下でセキュリティチェックが必要になる場合があります。 具体的には、呼び出し元が**置換 Eifexists**フィールドを**TRUE**に設定して、名前の変更またはハードリンクのターゲットを削除する場合、ファイルシステムはセキュリティチェックを実行して、ターゲットを削除するための適切なアクセス許可が呼び出し元に与えられていることを確認する必要があります。 さらに、ポリシーに関係なくファイルシステムがこの方法での削除を許可しないファイルの種類が存在する場合があります (レジストリハイブやページングファイルなど)。 次のコード例では、呼び出し元に、ファイルを削除するための適切なセキュリティアクセス許可があるかどうかを判断します。

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
            // fine - no security is fine - the user gets to do what they want
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

このコードは、名前変更とハードリンク作成ケースの両方に使用できます。

このドキュメントでは、削除するファイルの種類に基づいてファイルシステムで削除が禁止されていると判断されたポリシーレベルのコードについて説明します。
