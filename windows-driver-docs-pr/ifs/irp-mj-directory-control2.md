---
title: IRP_MJ_DIRECTORY_CONTROL
description: IRP_MJ_DIRECTORY_CONTROL
ms.assetid: 27c2de1c-5550-4211-97cc-4c66f18d3b99
keywords:
- IRP_MJ_DIRECTORY_CONTROL
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、IRP_MJ_DIRECTORY_CONTROL を確認します。
- ディレクトリ制御 WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1455a0d7b5d65c1deeb0cd1931ead06facf9fec7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553324"
---
# <a name="irpmjdirectorycontrol"></a>IRP\_MJ\_ディレクトリ\_コントロール


セキュリティは、特定のディレクトリの管理操作を処理するときの考慮事項、特にを扱うこれらの変更通知。 セキュリティ上の問題は、ディレクトリ変更通知が変更された特定のファイルに関する情報を返す可能性があります。 ユーザーがディレクトリへのパスを走査するための権限を持たない場合、変更に関する情報をユーザーに返さことはできません。 それ以外の場合、ユーザーは、ディレクトリを知らせずに、ユーザーに関する追加情報を学習するためのメカニズムをようになりました。

ファイル システムのランタイム ライブラリでディレクトリ変更通知をサポートすることにより、ファイル システム ディレクトリの変更通知を返す前に、走査チェックを実行するためのコールバック関数を指定します。 このコールバック関数では、多くのパラメーターを受け取ります。 セキュリティの考慮事項は、次の 3 つのパラメーターが重要です。

-   *NotifyContext*--変更通知がアクティブなディレクトリのコンテキスト。 これになります、 *FsContext*への呼び出しに渡されるパラメーター **FsRtlNotifyFilterChangeDirectory**します。 なお**FsRtlNotifyFilterChangeDirectory**以降を Windows XP で使用します。 使用されるシステムを Windows 2000、 **FsRtlNotifyFullChangeDirectory**関数と似ています。

-   *TargetContext*-変更されたファイルのコンテキスト。 これになります、 *TargetContext*を呼び出すときに、ファイル システムでパラメーターが渡される**が**します。

-   *SubjectContext*--ディレクトリを要求しているスレッドのセキュリティ コンテキストの変更通知します。 これは、サブジェクト セキュリティ コンテキストに、ディレクトリ変更通知の呼び出しが行われた時点で、ファイル システムでキャプチャされた**FsRtlNotifyFilterChangeDirectory**します。

変更されたときに、ファイル システムは、ファイル システムのランタイム ライブラリにこれを示します。 後、ファイル システムのランタイム ライブラリは、呼び出し元は変更に関する情報であることを確認するファイル システムによって提供されるコールバック関数を呼び出します。 ファイル システムがのみこのチェックが呼び出し元が必要な場合は、コールバック関数を登録する必要があるに注意してください。 これは、トークンで示されている、呼び出し元が有効になっている、SeChangeNotifyPrivilege を持たない場合、該当\_HAS\_走査\_呼び出し元のセキュリティ トークンの権限。

コールバック関数内でファイル システムで指定されたディレクトリから走査チェックを実行する必要があります、 *NotifyContext*パラメーターを変更で指定されたファイルを*TargetContext*パラメーター。 次のルーチンの例では、このようなチェックを行います。

```cpp
BOOLEAN 
FsdNotifyTraverseCheck ( 
    IN PDIRECTORY_CONTEXT OriginalDirectoryContext, 
    IN PFILE_CONTEXT ModifiedDirectoryContext,      
    IN PSECURITY_SUBJECT_CONTEXT SubjectContext
    )
{
  BOOLEAN AccessGranted = TRUE;
  PFILE_CONTEXT CurrentDirectoryContext;
  ACCESS_MASK GrantedAccess;
  NTSTATUS Status;
  PPRIVILEGE_SET Privileges = NULL;
  PFILE_CONTEXT TopDirectory;


  //
  //  Nothing to do  if there is no file context.
  //
  if (ModifiedDirectoryContext == NULL) {
 
    return TRUE;
  }
 
  //
  // If the directory that changed is the original directory, 
  // we can return , since the caller has access. 
  // Note that the directory  context is unique to the specific 
  // open instance, while the modified directory context 
  // represents the per-file/directory context. 
  // How these data structures work in your file system will vary.
  //
  if (OriginalDirectoryContext->FileContext == ModifiedDirectoryContext) {
    return TRUE;
  }
 
  //
  // Lock the subject context.
  //
  SeLockSubjectContext(SubjectContext);
 
 
  for( TopDirectory = OriginalDirectoryContext->FileContext,
          CurrentDirectoryContext = ModifiedDirectoryContext;
          CurrentDirectoryContext == TopDirectory || !AccessGranted;
          CurrentDirectoryContext = CurrentDirectoryContext->ParentDirectory) {
    //
    // Ensure we have the current security descriptor loaded for 
    // this directory.
    //
    FsdLoadSecurity( NULL, CurrentDirectoryContext);
 
    //
    // Perform traverse check.
    //
    AccessGranted = SeAccessCheck( 
            CurrentDirectoryContext->SecurityDescriptor,
            SubjectContext,
            TRUE,
            FILE_TRAVERSE,
            0,
            &Privileges,
            IoGetFileObjectGenericMapping(),
            UserMode,
            &GrantedAccess,
            &Status);
 
    //
    // At this point, exit the loop if access was not granted, 
    // or if the parent directory is the same as where the change 
    // notification was made.
    //
 
  }
 
  //
  // Unlock subject context.
  //
  SeUnlockSubjectContext(SubjectContext);
 
  return AccessGranted;
}
```

このルーチンがあるセキュリティの情報をキャッシュするファイル システムに大きく異なる可能性があります、またはファイルとディレクトリを追跡するためのさまざまなデータ構造がある (たとえば、ファイル間のリンクを追跡するための構造体を使用してファイルとディレクトリ)。 例では、簡略化するためには、このサンプルでのリンクをサポートするファイル システムは考慮されません。

 

 




