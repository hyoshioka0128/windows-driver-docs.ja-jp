---
title: SetupAPI を使用して、ドライバーの Authenticode 署名を検証するには
description: SetupAPI を使用して、ドライバーの Authenticode 署名を検証するには
ms.assetid: 2019d77d-2d98-4bae-8d9d-aa41e47f3811
keywords:
- SetupAPI 関数 WDK、署名の検証
- Authenticode 署名 WDK
- WDK、Authenticode の署名
- デジタル署名、WDK Authenticode
- Authenticode 署名の検証
- Authenticode 署名を確認
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6710e892a5dae0827394540786ae5bba00e6e19d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527431"
---
# <a name="using-setupapi-to-verify-driver-authenticode-signatures"></a>SetupAPI を使用して、ドライバーの Authenticode 署名を検証するには





次の手順を使用するには、ドライバーが有効な Authenticode であることを確認する[デジタル署名](digital-signatures.md)します。 これらのプロシージャは、Microsoft Windows Server 2003 以降はサポートされています。

### <a name="to-determine-whether-a-driver-has-a-valid-authenticode-signature"></a>ドライバーが有効な Authenticode 署名を持つかどうかを判断するには

DNF_AUTHENTICODE_SIGNED フラグを確認します。

Windows がこのフラグを設定するドライバーに有効な Authenticode 署名がある場合、**フラグ**のドライバー ノードのメンバー [ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)構造体。 (また、ドライバーがある場合、Windows が DNF_INF_IS_SIGNED フラグを設定する、 [WHQL リリース署名](whql-release-signature.md)Authenticode 署名がある場合、またはシステム提供のドライバーである場合)。

### <a name="to-verify-that-an-inf-file-has-a-valid-authenticode-signature"></a>INF ファイルを有効な Authenticode 署名があることを確認するには

1.  呼び出す、[関数を処理する INF ファイル](inf-file-processing-functions.md) **SetupVerifyInfFile**します。

2.  関数によって返されたエラー コードを確認します。

    INF ファイル システムがないし、有効な WHQL デジタル署名がありませんが、有効な Authenticode 署名が**SetupVerifyInfFile**返します**FALSE**と[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)次のエラー コードのいずれかを返します。

    <a href="" id="error-authenticode-trusted-publisher"></a>ERROR_AUTHENTICODE_TRUSTED_PUBLISHER  
    発行元の証明書がインストールされているため、発行元が信頼されていることを示します、[信頼された発行元証明書ストア](trusted-publishers-certificate-store.md)します。

    <a href="" id="error-authenticode-trust-not-established"></a>ERROR_AUTHENTICODE_TRUST_NOT_ESTABLISHED  
    ある信頼ことはできませんが自動的に確立されている発行元の署名証明書が信頼された発行元の証明書ストアにインストールされていないためにことを示します。 ただし、これは必ずしもエラー。 代わりに、呼び出し元がパブリッシャーでの信頼を確立するために呼び出し元に固有のポリシーを適用する必要がありますを示します。

INF ファイルに有効な Authenticode 署名がある場合**SetupVerifyInfFile** SP_INF_SIGNER_INFO 出力構造体の次の情報を返します。

-   **DigitalSigner**メンバー署名者の名前に設定されます。

-   **CatalogFile**メンバーは、対応する署名済みカタログ ファイルの完全なパスに設定します。

ただし、注意を**SetupVerifyInfFile**のバージョンは返されません、 **DigitalSignerVersion**メンバー。

### <a name="to-verify-that-a-file-has-a-valid-authenticode-signature"></a>ファイルに有効な Authenticode 署名があることを確認するには

SetupAPI 関数を呼び出す**SetupScanFileQueue** SPQ_SCAN_USE_CALLBACK_SIGNERINFO フラグを使用します。

**SetupScanFileQueue**呼び出し元のコールバック ルーチンを SPFILENOTIFY_QUEUESCAN_SIGNERINFO 要求を送信し、FILEPATHS_SIGNERINFO 構造体へのポインターを渡します。 ファイルは、有効な Authenticode 署名で署名されて、関数によって、エラー コードが適切な ERROR_AUTHENTICODE_Xxx 値にファイルをコールバック ルーチンを呼び出す前に設定します。 この関数は、FILEPATHS_SIGNERINFO 構造で、次の情報を設定します。

-   **DigitalSigner**メンバー署名者の名前に設定されます。

-   **CatalogFile**メンバーは、対応する署名済みカタログ ファイルの完全なパスに設定します。

ただし、バージョン設定されていないことに注意する、**バージョン**メンバー。

**SetupScanFileQueue**は、このトピックで前述したように、同じ方法で ERROR_AUTHENTICODE_Xxx エラー コードを設定**SetupVerifyInfFile**します。

 

 





