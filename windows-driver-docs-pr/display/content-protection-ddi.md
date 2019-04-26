---
title: Content Protection DDI
description: Content Protection DDI
ms.assetid: 770e0fce-d3b5-4599-8165-eadf3f23f9dc
keywords:
- ビデオ コンテンツ WDK Windows 7 の表示、コンテンツ保護 DDI を保護します。
- ビデオ コンテンツ WDK Windows Server 2008 R2 の表示、コンテンツ保護 DDI を保護します。
- ビデオ コンテンツ WDK Windows 7 の表示、コンテンツ保護 DDI
- ビデオ コンテンツのコンテンツ保護 DDI、WDK の Windows Server 2008 R2 の表示
- WDK の Windows Server 2008 R2 のビデオ コンテンツを表示、保護します。
- コンテンツ保護 DDI WDK Windows 7 の表示
- コンテンツ保護 DDI WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d177af3b3b118490083c46791b315b94bb30857c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356250"
---
# <a name="content-protection-ddi"></a>Content Protection DDI


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

コンテンツの保護 DDI は拡張機能、 [Direct3D のバージョン 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)ビデオを保護します。 このセクションに記載されているエントリ ポイントのコンテンツの保護 DDI で構成されます。

### <a name="span-idrequiredcontentprotectionddifunctionsspanspan-idrequiredcontentprotectionddifunctionsspanrequired-content-protection-ddi-functions"></a><span id="required_content_protection_ddi_functions"></span><span id="REQUIRED_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>必須の Content Protection DDI 関数

ユーザー モードのディスプレイ ドライバーでは、コンテンツの保護が実装されている場合、ドライバーは、次のコンテンツ保護 DDI 関数をサポートする必要があります。

-   [ **CreateAuthenticatedChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540591)関数は、Direct3D ランタイムと、ドライバーは、保護の照会や設定に使用できるチャネルを作成します。

-   [ **AuthenticatedChannelKeyExchange** ](https://msdn.microsoft.com/library/windows/hardware/ff538241)関数は、セッション キーをネゴシエートします。

-   [ **QueryAuthenticatedChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff569213)関数は、機能と状態情報については、認証済みチャネルを照会します。

-   [ **ConfigureAuthenticatedChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff539572)関数は、認証済みチャネル内の状態を設定します。

-   [ **DestroyAuthenticatedChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff552741)関数は、チャネルの認証済みのリソースを解放します。

-   [ **CreateCryptoSession** ](https://msdn.microsoft.com/library/windows/hardware/ff540609)関数は、Direct3D のランタイムを使用してセッション キーを管理する暗号化セッションを作成し、保護されたメモリの入出力の暗号化の操作を実行します。

-   [ **CryptoSessionKeyExchange** ](https://msdn.microsoft.com/library/windows/hardware/ff540791)関数は、セッション キーをネゴシエートします。

-   [ **DestroyCryptoSession** ](https://msdn.microsoft.com/library/windows/hardware/ff552752)関数は、暗号化、セッションにリソースを解放します。

### <a name="span-idcontentprotectioncapabilitiesspanspan-idcontentprotectioncapabilitiesspancontent-protection-capabilities"></a><span id="content_protection_capabilities"></span><span id="CONTENT_PROTECTION_CAPABILITIES"></span>コンテンツの保護機能

ユーザー モードのディスプレイ ドライバーは、前に必要なコンテンツ保護 DDI 関数をサポートしている場合にのみコンテンツの保護機能を報告します。 次[ **D3DDDICAPS\_型**](https://msdn.microsoft.com/library/windows/hardware/ff544132)値は、ユーザー モードにドライバーでは表示されるコンテンツの保護機能についての情報を取得する Direct3D のランタイムによって使用されます。 ランタイム設定これら D3DDDICAPS\_で値型、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体、 *pData*のドライバーのパラメーター [ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)関数ランタイムが呼び出すときに指す**GetCaps**します。

<span id="D3DDDICAPS_GETCONTENTPROTECTIONCAPS"></span><span id="d3dddicaps_getcontentprotectioncaps"></span>D3DDDICAPS\_GETCONTENTPROTECTIONCAPS  
ランタイムへのポインターを提供する、 [ **DDICONTENTPROTECTIONCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549568)特定の暗号化用の構造し、ドライバーが使用する組み合わせをデコードします。 ドライバーでは、暗号化用のドライバーのコンテンツ保護の機能を説明するデータが設定された D3DCONTENTPROTECTIONCAPS 構造体へのポインターを返しますおよび組み合わせをデコードします。 D3DCONTENTPROTECTIONCAPS の詳細については、DirectX SDK のドキュメントを参照してください。

<span id="D3DDDICAPS_GETCERTIFICATESIZE"></span><span id="d3dddicaps_getcertificatesize"></span>D3DDDICAPS\_GETCERTIFICATESIZE  
ドライバーは、チャネルまたは暗号化の種類に使用される、ドライバーの証明書のバイト単位のサイズを指定する数値にポインターを提供します。 Direct3D ランタイムは、ランタイムが呼び出すと、ランタイムが受信する証明書情報を保持するバッファーを割り当てるためこのサイズを使用する、 [ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762) D3DDDICAPS で\_GETCERTIFICATE します。

<span id="D3DDDICAPS_GETCERTIFICATE"></span><span id="d3dddicaps_getcertificate"></span>D3DDDICAPS\_GETCERTIFICATE  
ランタイムへのポインターを提供する、 [ **DDICERTIFICATEINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff549552)ドライバーを取得する証明書を記述する構造体。

ドライバーが、認証済みチャネルによって、既存を使用して[OPM](opm-features.md)証明書は Microsoft によって署名されたルートである X.509 証明書です。

アプリケーションは、次の情報を確認するドライバーの証明書にクエリを実行します。

-   ドライバーが信頼されているかどうか。

-   かどうか、ドライバーは失効します。

-   ドライバーの公開キー。 アプリケーションでは、ドライバーの公開キーを使用して、認証に使用される認証済みのチャネルのセッション キーを確立します。

呼び出し[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762) D3DDDICAPS で\_Direct3D 9 は、このチャネルは、証明書または認証をサポートしていないためにチャネルを認証するために呼び出された場合、GETCERTIFICATE セットが失敗します。

暗号化セッションで、ドライバーは、指定した暗号化型の証明書を返します。 暗号化の種類と使用されるキー交換の場合は、によって、証明書には、使用できない場合あります。 さまざまな暗号化の種類が異なる証明書を使用できることもできます。

### <a name="span-idoptionalcontentprotectionddifunctionsspanspan-idoptionalcontentprotectionddifunctionsspanoptional-content-protection-ddi-functions"></a><span id="optional_content_protection_ddi_functions"></span><span id="OPTIONAL_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>省略可能なコンテンツ保護 DDI 関数

ドライバーでは、次のコンテンツの保護 DDI 関数をオプションでサポートできます。

-   [ **EncryptionBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564153)関数は、保護された画面から暗号化されたデータを読み取ります。

-   [ **GetPitch** ](https://msdn.microsoft.com/library/windows/hardware/ff566799)関数は、保護されている画面のピッチを取得します。

-   [ **StartSessionKeyRefresh** ](https://msdn.microsoft.com/library/windows/hardware/ff569729)関数を返します、ランダムな番号をデコーダー/アプリケーションとドライバーのハードウェア/セッションで排他的 OR 演算 (XOR) に使用できますキー。

-   [ **FinishSessionKeyRefresh** ](https://msdn.microsoft.com/library/windows/hardware/ff565671)関数では、その特定の時点からのすべてのバッファーが更新されたセッション キーの値を使用することを示します。

-   [ **GetEncryptionBltKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566787)関数は、データを復号化に使用されるキーを返しますドライバーの[ **EncryptionBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564153)関数を返します。

-   [ **DecryptionBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff551823)関数は、保護されている画面にデータを書き込みます。

### <a name="span-idcontentprotectedresourcesspanspan-idcontentprotectedresourcesspan-content-protected-resources"></a><span id="content_protected_resources"></span><span id="CONTENT_PROTECTED_RESOURCES"></span> 保護されたリソースのコンテンツ

次[ **D3DDDI\_RESOURCEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544644) Direct3D ランタイムによって保護されたコンテンツにフラグを使用します。 ランタイム設定これら D3DDDI\_RESOURCEFLAGS でフラグを設定、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体、*pResource*のドライバーのパラメーター [ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数ランタイムが呼び出すときに指す**CreateResource**.

<span id="RestrictedContent"></span><span id="restrictedcontent"></span><span id="RESTRICTEDCONTENT"></span>**RestrictedContent**  
リソースには、保護されたコンテンツが含まれます。 アプリケーションが明示的に有効にしていないコンテンツ保護、アプリケーションがリソースを作成する前に、可能性があります。 ドライバーでは、ランタイムが保護可能なメモリ プールのリソースの割り当てを配置することを確認してください。 ドライバーは、ロック保護されたリソースの作成を許可する必要があります。 ただし、ドライバーにはへの呼び出しが失敗する必要があります明示的にその[**ロック**](https://msdn.microsoft.com/library/windows/hardware/ff568213)コンテンツ保護が有効になっているときに、これらのサーフェスをロックする関数。

<span id="RestrictSharedAccess"></span><span id="restrictsharedaccess"></span><span id="RESTRICTSHAREDACCESS"></span>**RestrictSharedAccess**  
特定のプロセスには、共有リソースへのアクセスを許可する必要があります。

ドライバーは、このリソースへの共有のアクセスを制限する必要があります。 ランタイムは、ドライバーを呼び出すことができますのみ[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)ディスプレイ デバイスにこのリソースを開きます (**hDevice**) リソースを作成するプロセス内またはこれらのデバイスで、認証済みチャネルを使用してアクセスを明示的に付与するされました。

 

 





