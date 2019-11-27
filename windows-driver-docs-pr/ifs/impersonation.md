---
title: 偽装
description: 偽装
ms.assetid: 368c6741-b51a-4629-8ae6-a7848c07c0fc
keywords:
- セキュリティ WDK ファイルシステム、セキュリティチェックの追加
- セキュリティチェック WDK ファイルシステム、偽装
- 権限借用 WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e7ec8a6d06b6487c135b49f515eab9afa3226a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841206"
---
# <a name="impersonation"></a>偽装


## <span id="ddk_impersonation_if"></span><span id="DDK_IMPERSONATION_IF"></span>


ファイルシステムによっては、元の呼び出し元に代わって操作を実行すると便利な場合があります。 たとえば、ネットワークファイルシステムでは、ファイルを開いたときに呼び出し元のセキュリティ情報をキャプチャし、適切な資格情報を使用して後続の操作を実行できるようにすることが必要になる場合があります。 当然のことですが、この種の機能は、ファイルシステム内と特定のアプリケーションの両方で役に立ちます。

偽装に必要な主なルーチンは次のとおりです。

-   [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psimpersonateclient) [**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)は偽装を開始します。 特定のスレッドが指定されていない限り、偽装は現在のスレッドコンテキストで実行されます。

-   **Psreverttoself**--現在のスレッドコンテキスト内で偽装を終了します。

-   [**Psreferenceprimarytoken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psreferenceprimarytoken)--指定されたプロセスのプライマリ (プロセス) トークンに対する参照を保持します。 この関数は、システム上の任意のプロセスのトークンをキャプチャするために使用できます。

-   [**PsDereferencePrimaryToken**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-psdereferenceprimarytoken)--以前に参照されたプライマリトークンで参照を解放します。

-   [**SeCreateClientSecurityFromSubjectContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurityfromsubjectcontext)--クライアントのセキュリティコンテキストを返します。サブジェクトコンテキストからの権限借用に役立ちます ( **IRP\_MJ\_CREATE**処理中に FSD に提供されます)。

-   [**SeCreateClientSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-secreateclientsecurity)--システム上の既存のスレッドのセキュリティ資格情報に基づいて、クライアントのセキュリティコンテキストを作成します。

-   **ImpersonateSecurityContext**--カーネルセキュリティサービスである ksecdd .sys 内のセキュリティコンテキストを偽装します。

-   **RevertSecurityContext**--カーネルセキュリティサービスである ksecdd .sys 内の偽装を終了します。

偽装は、を実装するための簡単な方法です。 次のコード例は、基本的な偽装を示しています。

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
      // This is bad - we can't restore, we can't leave it this way 
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

この偽装コードには、ファイルシステムの開発者が使用できるさまざまなバリエーションがありますが、その手法の基本的な例を示します。

 

 




