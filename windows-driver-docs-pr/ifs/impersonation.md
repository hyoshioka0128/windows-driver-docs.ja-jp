---
title: 権限借用
description: 権限借用
ms.assetid: 368c6741-b51a-4629-8ae6-a7848c07c0fc
keywords:
- セキュリティ WDK ファイル システム、セキュリティ チェックを追加します。
- セキュリティは、WDK のファイル システム、権限借用を確認します。
- 権限借用 WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cb46eb45aa8c3e5ed52a70f2f78c97fa97a5ba5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549118"
---
# <a name="impersonation"></a>権限借用


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


一部のファイル システムに役に立つ最初の呼び出し元の代わりに操作を実行します。 たとえば、ネットワーク ファイル システムは、適切な資格情報を使用して、後続の操作を実行できるように、ファイルを開いた時点で、呼び出し元のセキュリティの情報をキャプチャする必要があります。 さまざまな他の特殊なケースこの種の機能が便利ですが、特定のアプリケーションと同様にもファイル システム内で両方がある間違いありません。

キーのルーチンに必要な権限の借用が含まれます。

-   [**PsImpersonateClient**](https://msdn.microsoft.com/library/windows/hardware/ff551907) [**SeImpersonateClientEx**](https://msdn.microsoft.com/library/windows/hardware/ff556659)--偽装を開始します。 特定のスレッドは、指定した場合を除き、権限の借用は、現在のスレッド コンテキストで行われます。

-   **PsRevertToSelf**--現在のスレッド コンテキスト内で権限借用を終了します。

-   [**PsReferencePrimaryToken**](https://msdn.microsoft.com/library/windows/hardware/ff551930)--指定されたプロセスのプライマリ (プロセス) トークンの参照を保持します。 この関数は、システム上のどのプロセスのトークンをキャプチャを使用できます。

-   [**PsDereferencePrimaryToken**](https://msdn.microsoft.com/library/windows/hardware/ff551896)-参照されている以前のプライマリ トークンの参照を解放します。

-   [**SeCreateClientSecurityFromSubjectContext**](https://msdn.microsoft.com/library/windows/hardware/ff556598)--クライアントに返しますサブジェクト コンテキストからの権限借用のための便利なセキュリティ コンテキスト (中に、FSD に提供される、 **IRP\_MJ\_を作成します。** 処理など)。

-   [**SeCreateClientSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff556595)--システム上の既存のスレッドのセキュリティ資格情報に基づいたクライアントのセキュリティ コンテキストを作成します。

-   **ImpersonateSecurityContext**--ksecdd.sys、カーネルのセキュリティ サービス内でのセキュリティ コンテキストの権限を借用します。

-   **RevertSecurityContext**--ksecdd.sys、カーネルのセキュリティ サービス内で権限借用を終了します。

権限借用には、実装するために簡単です。 次のコード例では、基本的な権限の借用を示しています。

```cpp
NTSTATUS PerformSpecialTask(IN PFSD_CONTEXT Context)
{
  BOOLEAN CopyOnOpen;
  BOOLEAN EffectiveOnly;
  SECURITY_IMPERSONATION_LEVEL ImpersonationLevel;
  NTSTATUS Status;
  PACCESS_TOKEN oldToken;

  //
  // We need to perform a task in the system process context
  //
  if (NULL == Context->SystemProcess) {

    return STATUS_NO_TOKEN;

  }

  //
  // Save the existing token, if any (otherwise NULL)
  //
  oldToken = PsReferenceImpersonationToken(PsGetCurrentThread(),
                                           &CopyOnOpen,
                                           &EffectiveOnly,
                                           &ImpersonationLevel);

  Status = PsImpersonateClient( PsGetCurrentThread(),
                                Context->SystemProcess,
                                TRUE,
                                TRUE,
                                SecurityImpersonation);
  if (!NT_SUCCESS(Status)) {

    if (oldToken)
        PsDereferenceImpersonationToken(oldToken);
    return Status;

  }

  //
  // Perform task - whatever it is
  //


  //
  // Restore to previous impersonation level
  //
  if (oldToken) {
    Status = PsImpersonateClient(PsGetCurrentThread(),
                                 oldToken,
                                 CopyOnOpen,
                                 EffectiveOnly,
                                 ImpersonationLevel);

    if (!NT_SUCCESS(Status)) {
      //
      // This is bad - we can&#39;t restore, we can&#39;t leave it this way 
      //
      PsRevertToSelf();
    }
    PsDereferenceImpersonationToken(oldToken);
  } else {
    PsRevertToSelf();
  }

  return Status;
}
```

ファイル システムの開発者が利用できるは、この権限借用のコードのさまざまなバリエーションがありますが、この方法の基本的な説明を提供します。

 

 




