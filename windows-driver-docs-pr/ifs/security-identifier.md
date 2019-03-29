---
title: セキュリティ識別子
description: セキュリティ識別子
ms.assetid: e4c39d83-6f32-406c-b8d5-d41305a8976f
keywords:
- WDK のセキュリティ記述子のファイル システム、セキュリティ識別子
- WDK の記述子ファイル システム、セキュリティ識別子
- WDK のファイル システムのセキュリティ識別子
- ファイル システムの Sid の WDK
- WDK のよく知られた識別子はファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95918109cb6c931fdfdd257262246ec703a2a48f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573275"
---
# <a name="security-identifier"></a>セキュリティ識別子


## <span id="ddk_security_identifier_if"></span><span id="DDK_SECURITY_IDENTIFIER_IF"></span>


セキュリティ識別子は、1 つ別のエンティティのセキュリティを区別するために、Windows によって、最終的な値として使用されます。 たとえば、一意なセキュリティ識別子は、システム上の個々 のユーザー用に作成された新しい各アカウントに割り当てられます。 ファイル システムでは、この SID のみが実際に使用されます。

次の図は、セキュリティ識別子の構造を示しています。

![セキュリティ識別子の構造を示す図](images/fssecurity-02.png)

だけでなく、一意の Sid は、Windows システムは、よく知られた識別子のセットを定義します。 たとえば、ローカル管理者が、このような既知の SID。 Windows では、カーネル環境内で名を Sid とユーザー間で変換するためのカーネルのメカニズムを提供します。 これらの関数呼び出しユーザー モードのヘルパー サービスを使用してこれらの関数を実装する ksecdd によるシール ドライバーから利用できます。 したがって、ファイル システムでの使用法はユーザー モードのサービスとの通信の通常の規則に従う必要があります。 これらの呼び出しは、ページング ファイル I/O 中は使用できません。

関数は、次のとおりです。

-   [**SecMakeSPN**](https://msdn.microsoft.com/library/windows/hardware/ff556584)-特定のセキュリティ サービス プロバイダーと通信するときに使用できるサービス プロバイダー名文字列を作成します。

-   [**SecMakeSPNEx**](https://msdn.microsoft.com/library/windows/hardware/ff556585)-拡張のバージョンの**SecMakeSPN**します。 この関数は、Microsoft Windows XP と以降のバージョンの Windows で使用できます。

-   [**SecMakeSPNEx2**](https://msdn.microsoft.com/library/windows/hardware/ff556592)-拡張のバージョンの**SecMakeSPNEx**します。 この関数は、Windows Vista、Windows Server 2008、および以降のバージョンの Windows で使用できます。

-   [**SecLookupAccountSid**](https://msdn.microsoft.com/library/windows/hardware/ff556579)-SID を指定するには、このルーチンは、アカウント名が返すされます。 この関数は、以降 Windows XP で利用可能です。

-   [**SecLookupAccountName**](https://msdn.microsoft.com/library/windows/hardware/ff554795): アカウント名を指定すると、このルーチンは SID が取得されます。 この関数は、以降 Windows XP で利用可能です。

-   [**SecLookupWellKnownSid**](https://msdn.microsoft.com/library/windows/hardware/ff556582)-既知の SID の種類を指定するには、このルーチンは、適切な SID を返すは。 この関数は、以降 Windows Server 2003 で利用可能です。

さらに、カーネル ドライバーでは、次の標準ランタイム ライブラリ ルーチンを使用して、SID を作成することがあります。

-   [**RtlInitializeSid**](https://msdn.microsoft.com/library/windows/hardware/ff552998)-新しい SID のバッファーを初期化します。

-   [**RtlLengthSid**](https://msdn.microsoft.com/library/windows/hardware/ff553085): 指定されたバッファーに保存されている SID のサイズを決定します。

-   [**RtlValidSid**](https://msdn.microsoft.com/library/windows/hardware/ff553314): 指定された SID バッファーが有効な書式設定されたバッファーであるかどうか。

なお**RtlLengthSid**と**RtlValidSid** SID の 8 バイトの固定ヘッダーが存在することを前提としています。 したがって、ドライバーは、これらの関数を呼び出す前にこの SID ヘッダーの長さの最小確認する必要があります。

その他のいくつかの RTL 関数もありますが、これらは、主な機能に必要な SID を構築するときに。

次のコード例では、「ローカル システム」のエンティティの SID を作成する方法を示します。

```cpp
{
    //
    // temporary stack-based storage for an SID
    //
    UCHAR sidBuffer[128];
    PISID localSid = (PISID) sidBuffer;
    SID_IDENTIFIER_AUTHORITY localSidAuthority = 
        SECURITY_NT_AUTHORITY;

    //
    // build the local system SID
    //
    RtlZeroMemory(sidBuffer, sizeof(sidBuffer));
 
    localSid->Revision = SID_REVISION;
    localSid->SubAuthorityCount = 1;
    localSid->IdentifierAuthority = localSidAuthority;
    localSid->SubAuthority[0] = SECURITY_LOCAL_SYSTEM_RID;
 
    //
    // make sure it is valid
    //
    if (!RtlValidSid(localSid)) {
        DbgPrint("no dice - SID is invalid\n");
        return(1);
    }
}
```

これでしたも行ったことに注意してください、単純な関数を使用して**SecLookupWellKnownSid** Windows Server 2003 で導入されました。

次のコード例に示しますを使用して SID を作成する方法、 **SecLookupWellKnownSid** 「ローカル システム」のエンティティの関数。

```cpp
{
    UCHAR sidBuffer[128];
    PISID localSid = (PISID) sidBuffer;
    SIZE_T sidSize;
    status = SecLookupWellKnownSid(WinLocalSid,
                                   &localSid,
                                   sizeof(sidBuffer),
                                   &sidSize);

    if (!NT_SUCCESS(status)) {
      //
      // error handling
      //
    }
  }
```

後者のコードをお勧めですが、これらの方法のいずれかの機能が有効でします。 これらのコード例が SID を格納するためのローカル バッファーを使用することに注意してください。 これらのバッファーは、現在の呼び出しコンテキストの外部は使用できません。 SID のバッファーは、永続的にする必要がある場合は、プールのメモリからバッファーを割り当てる必要があります。

 

 




