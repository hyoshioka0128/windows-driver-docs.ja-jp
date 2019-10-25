---
title: セキュリティ識別子
description: セキュリティ識別子
ms.assetid: e4c39d83-6f32-406c-b8d5-d41305a8976f
keywords:
- セキュリティ記述子 WDK ファイルシステム、セキュリティ識別子
- 記述子 WDK ファイルシステム、セキュリティ識別子
- セキュリティ識別子 WDK ファイルシステム
- Sid WDK ファイルシステム
- 既知の識別子 (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a340e5283e0abb6f023938035542d688c6f54816
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840970"
---
# <a name="security-identifier"></a>セキュリティ識別子


## <span id="ddk_security_identifier_if"></span><span id="DDK_SECURITY_IDENTIFIER_IF"></span>


セキュリティ識別子は、セキュリティエンティティどうしを区別するための明確な値として Windows によって使用されます。 たとえば、システムの個々のユーザーに対して作成された新しいアカウントごとに、一意のセキュリティ識別子が割り当てられます。 ファイルシステムの場合は、この SID だけが実際に使用されます。

次の図は、セキュリティ識別子の構造を示しています。

![セキュリティ識別子の構造を示す図](images/fssecurity-02.png)

一意の Sid に加えて、Windows システムは既知の一連の識別子を定義します。 たとえば、ローカル管理者はよく知られた SID です。 Windows には、カーネル環境内の Sid とユーザー名を変換するためのカーネル内メカニズムが用意されています。 これらの関数呼び出しは、ksecdd ドライバーから使用できます。これらの関数は、ユーザーモードヘルパーサービスを使用してこれらの関数を実装します。 したがって、ファイルシステム内での使用は、ユーザーモードサービスとの通信に関する通常の規則に従う必要があります。 これらの呼び出しは、ページングファイル i/o 中には使用できません。

関数には、次のようなものがあります。

-   [**SecMakeSPN**](https://msdn.microsoft.com/library/windows/hardware/ff556584)-特定のセキュリティサービスプロバイダーと通信するときに使用できるサービスプロバイダー名文字列を作成します。

-   [**SecMakeSPNEx**](https://msdn.microsoft.com/library/windows/hardware/ff556585)— **SecMakeSPN**の拡張バージョンです。 この機能は、Microsoft Windows XP 以降のバージョンの Windows で使用できます。

-   [**SecMakeSPNEx2**](https://msdn.microsoft.com/library/windows/hardware/ff556592)— **SecMakeSPNEx**の拡張バージョンです。 この機能は、windows Vista、Windows Server 2008、およびそれ以降のバージョンの Windows で使用できます。

-   [**SecLookupAccountSid**](https://msdn.microsoft.com/library/windows/hardware/ff556579)— SID が指定されている場合、このルーチンはアカウント名を返します。 この機能は、Windows XP 以降で使用できます。

-   [**SecLookupAccountName**](https://msdn.microsoft.com/library/windows/hardware/ff554795)—アカウント名を指定すると、このルーチンは SID を取得します。 この機能は、Windows XP 以降で使用できます。

-   [**SecLookupWellKnownSid**](https://msdn.microsoft.com/library/windows/hardware/ff556582)—既知の sid の種類を指定した場合、このルーチンは正しい sid を返します。 この機能は、Windows Server 2003 以降で使用できます。

また、次の標準ランタイムライブラリルーチンを使用して、すべてのカーネルドライバーで SID を作成することもできます。

-   [**Rtlinitializesid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlinitializesid)—新しい SID のバッファーを初期化します。

-   [**RtlLengthSid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtllengthsid)—指定したバッファー内に格納されている SID のサイズを決定します。

-   [**Rtlvalidsid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlvalidsid)—指定した SID バッファーが有効な形式のバッファーであるかどうかを判断します。

**RtlLengthSid**と**RTLVALIDSID**は、SID の8バイトの固定ヘッダーが存在すると想定しています。 そのため、ドライバーは、これらの関数を呼び出す前に、SID ヘッダーの最小の長さを確認する必要があります。

他にもいくつかの RTL 関数がありますが、これらは SID を構築するときに必要な主な機能です。

次のコード例は、"local system" エンティティの SID を作成する方法を示しています。

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

これは、Windows Server 2003 で導入されたより単純な関数**SecLookupWellKnownSid**を使用して行うこともできます。

次のコード例は、"local system" エンティティに対して**SecLookupWellKnownSid**関数を使用して SID を作成する方法を示しています。

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

どちらの方法も有効ですが、後者のコードはお勧めします。 これらのコード例では、SID を格納するためにローカルバッファーを使用することに注意してください。 これらのバッファーは、現在の呼び出しコンテキストの外部では使用できません。 SID バッファーを永続化する必要がある場合は、バッファーをプールメモリから割り当てる必要があります。

 

 




