---
title: Content Protection DDI
description: Content Protection DDI
ms.assetid: 770e0fce-d3b5-4599-8165-eadf3f23f9dc
keywords:
- ビデオコンテンツの保護 WDK Windows 7 ディスプレイ、Content Protection DDI
- ビデオコンテンツの保護 WDK Windows Server 2008 R2 ディスプレイ、Content Protection DDI
- ビデオコンテンツ WDK Windows 7 ディスプレイ、Content Protection DDI
- ビデオコンテンツ WDK Windows Server 2008 R2 ディスプレイ、Content Protection DDI
- ビデオコンテンツ WDK Windows Server 2008 R2 の表示、保護
- Content Protection DDI WDK Windows 7 ディスプレイ
- Content Protection DDI WDK Windows Server 2008 R2 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a474587ad8988ba53756d0501556ca72d27d9553
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839045"
---
# <a name="content-protection-ddi"></a>Content Protection DDI


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

Content Protection DDI は、ビデオを保護する[Direct3D バージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)の拡張機能です。 Content Protection DDI は、このセクションで説明されているエントリポイントで構成されています。

### <a name="span-idrequired_content_protection_ddi_functionsspanspan-idrequired_content_protection_ddi_functionsspanrequired-content-protection-ddi-functions"></a><span id="required_content_protection_ddi_functions"></span><span id="REQUIRED_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>必須 Content Protection DDI 関数

コンテンツ保護がユーザーモード表示ドライバーで実装されている場合、ドライバーは次の Content Protection DDI 機能をサポートする必要があります。

-   [**Create認証 atedchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createauthenticatedchannel)関数は、Direct3D ランタイムとドライバーが保護を設定および照会するために使用できるチャネルを作成します。

-   認証[**Atedchannelkeyexchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_authenticatedchannelkeyexchange)関数は、セッションキーをネゴシエートします。

-   [**Queryauthenticated Atedchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryauthenticatedchannel)関数は、認証されたチャネルに対して、機能と状態の情報を照会します。

-   [**ConfigureAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)関数は、認証されたチャネル内で状態を設定します。

-   [**Destroy認証 Atedchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyauthenticatedchannel)関数は、認証されたチャネルのリソースを解放します。

-   [**CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)関数は、セッションキーを管理し、保護されたメモリとの間で暗号化操作を実行するために、Direct3D ランタイムが使用する暗号化セッションを作成します。

-   [**Cryptosessionkeyexchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_cryptosessionkeyexchange)関数は、セッションキーをネゴシエートします。

-   [**Destroycryptosession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycryptosession)関数は、暗号化セッションのリソースを解放します。

### <a name="span-idcontent_protection_capabilitiesspanspan-idcontent_protection_capabilitiesspancontent-protection-capabilities"></a><span id="content_protection_capabilities"></span><span id="CONTENT_PROTECTION_CAPABILITIES"></span>Content Protection の機能

ユーザーモードの表示ドライバーは、前述の必須 Content Protection DDI 関数をそれぞれサポートしている場合にのみ、コンテンツ保護機能を報告します。 次の[**D3DDDICAPS\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)値は、ユーザーモード表示ドライバーがサポートするコンテンツ保護機能に関する情報を取得するために、Direct3D ランタイムによって使用されます。 ランタイムは、この D3DDDICAPS\_TYPE 値を[**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**type**メンバーに設定します。これは、ランタイムが**getcaps**を呼び出したときに、ドライバーの[**getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の*pData*パラメーターが指すようにします。

<span id="D3DDDICAPS_GETCONTENTPROTECTIONCAPS"></span><span id="d3dddicaps_getcontentprotectioncaps"></span>D3DDDICAPS\_GETCONTENTPROTECTIONCAPS  
ランタイムは、ドライバーが使用する特定の暗号化とデコードの組み合わせに対して、 [**Ddicontentprotectioncaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicontentprotectioncaps)構造体へのポインターを提供します。 ドライバーは、暗号化とデコードの組み合わせに対応するドライバーのコンテンツ保護機能を記述する、設定された D3DCONTENTPROTECTIONCAPS 構造体へのポインターを返します。 D3DCONTENTPROTECTIONCAPS の詳細については、DirectX SDK のドキュメントを参照してください。

<span id="D3DDDICAPS_GETCERTIFICATESIZE"></span><span id="d3dddicaps_getcertificatesize"></span>D3DDDICAPS\_GET ESIZE  
ドライバーは、チャネルまたは暗号の種類に使用されるドライバーの証明書のサイズ (バイト単位) を指定する数値へのポインターを提供します。 次に、Direct3D ランタイムは、このサイズを使用して、ランタイムが D3DDDICAPS\_GETCAPS で[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)を呼び出したときにランタイムが受け取る証明書情報を保持するバッファーを割り当てます。

<span id="D3DDDICAPS_GETCERTIFICATE"></span><span id="d3dddicaps_getcertificate"></span>D3DDDICAPS\_GETCERTIFICATE  
ランタイムは、ドライバーが取得する証明書を記述する[**DDICERTIFICATEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicertificateinfo)構造体へのポインターを提供します。

認証済みチャネルの場合、ドライバーは既存の[OPM](opm-features.md)証明書を使用します。これは、Microsoft によって署名された x.509 証明書です。

アプリケーションでは、ドライバーの証明書に対してクエリを実行し、次の情報を確認できます。

-   ドライバーが信頼されているかどうか。

-   ドライバーが失効しているかどうか。

-   ドライバーの公開キー。 アプリケーションは、ドライバーの公開キーを使用して、認証に使用される認証済みチャネルのセッションキーを確立します。

このチャネルでは証明書または認証がサポートされていないため、Direct3D 9 認証チャネルに対して呼び出された場合、D3DDDICAPS\_GETCAPS set を使用した[**Getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)の呼び出しは失敗します。

暗号化セッションの場合、ドライバーは指定された暗号化の種類に対応する証明書を返します。 使用される暗号化の種類とキー交換によっては、証明書が使用される場合と使用されない場合があります。 また、さまざまな暗号化の種類で異なる証明書を使用できる可能性もあります。

### <a name="span-idoptional_content_protection_ddi_functionsspanspan-idoptional_content_protection_ddi_functionsspanoptional-content-protection-ddi-functions"></a><span id="optional_content_protection_ddi_functions"></span><span id="OPTIONAL_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>オプションの Content Protection DDI 関数

ドライバーは、必要に応じて次の Content Protection DDI 機能をサポートできます。

-   [**Encryptionblt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)関数は、保護されたサーフェイスから暗号化されたデータを読み取ります。

-   [**Getpitch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getpitch)関数は、保護されたサーフェイスのピッチを取得します。

-   [**Startsessionkeyrefresh**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_startsessionkeyrefresh)関数は、デコーダー/アプリケーションとドライバー/ハードウェアが、その後、セッションキーで排他的 OR 演算 (XOR) を実行するために使用できるランダムな数値を返します。

-   [**Finish Sessionkeyrefresh**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_finishsessionkeyrefresh)関数は、その時点のすべてのバッファーが、更新されたセッションキー値を使用することを示します。

-   [**Getencryptionbltkey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getencryptionbltkey)関数は、ドライバーの[**encryptionblt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)関数が返すデータの暗号化を解除するために使用するキーを返します。

-   [**DecryptionBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decryptionblt)関数は、保護されたサーフェイスにデータを書き込みます。

### <a name="span-idcontent_protected_resourcesspanspan-idcontent_protected_resourcesspan-content-protected-resources"></a><span id="content_protected_resources"></span><span id="CONTENT_PROTECTED_RESOURCES"></span>コンテンツ保護されたリソース

次の[**D3DDDI\_resourceflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)フラグは、保護されたコンテンツの Direct3D ランタイムによって使用されます。 ランタイムは、 [**D3DDDIARG\_createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**flags**メンバー内のこれらの D3DDDI\_resourceflags フラグを設定します。これは、ドライバーの[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数の*presource*パラメーターが、ランタイムは**Createresource**を呼び出します。

<span id="RestrictedContent"></span><span id="restrictedcontent"></span><span id="RESTRICTEDCONTENT"></span>**RestrictedContent**  
リソースには、保護されたコンテンツが含まれる場合があります。 アプリケーションがリソースを作成する前に、コンテンツ保護が明示的に有効になっている場合があります。 ドライバーは、ランタイムがリソースの割り当てを、保護できるメモリプールに配置するようにします。 ドライバーは、ロック可能な保護されたリソースの作成を許可する必要があります。 ただし、ドライバーは、コンテンツ保護が有効になっている間、[**ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)関数の呼び出しを明示的に失敗させて、これらのサーフェイスをロックする必要があります。

<span id="RestrictSharedAccess"></span><span id="restrictsharedaccess"></span><span id="RESTRICTSHAREDACCESS"></span>**RestrictSharedAccess**  
共有リソースへのアクセスが許可されるのは、特定のプロセスだけです。

ドライバーは、このリソースへの共有アクセスを制限する必要があります。 ランタイムは、ドライバーの[**Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数を呼び出して、リソースを作成したプロセス内、または認証されたを介して明示的にアクセスが許可されたデバイスで、このリソースを開くことができ**ます。** チャンネル.

 

 





