---
title: ユーザーモードコンポーネントからの COPP DDI の呼び出し
description: ユーザーモードコンポーネントからの COPP DDI の呼び出し
ms.assetid: f7ce10d3-bf52-4bfd-9ae8-63213a59d1c9
keywords:
- COPP DDI WDK DirectX VA を呼び出しています
- ユーザーモードコンポーネントが WDK DirectX VA を呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d7b9f793812abb7383804ce5c239298d1cd33b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839820"
---
# <a name="calling-the-copp-ddi-from-a-user-mode-component"></a>ユーザーモードコンポーネントからの COPP DDI の呼び出し


## <span id="ddk_calling_the_copp_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

VMR などのユーザーモードコンポーネントによって、COPP DDI への呼び出しが開始されます。

VMR がビデオミニポートドライバーに対して、グラフィックスアダプターのビデオ出力に保護を適用するように通知できるように、表示ドライバーは、DD のメンバーによって定義された[モーション補正コールバック関数](motion-compensation-callbacks.md)を実装する必要があり[ **\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。

ドライバーの開発を簡単にするために、ドライバー作成者は、モーション補正コードテンプレートを使用して、COPP Ioctl および[copp サンプル関数](sample-functions-for-copp.md)を実装できます。 ディスプレイドライバーとビデオミニポートドライバーは、COPP Ioctl を使用して通信します。 詳細については、「[表示ドライバーからの COPP DDI の呼び出し](calling-the-copp-ddi-from-the-display-driver.md)」を参照してください。 モーション補正コードテンプレートは、COPP サンプル関数への呼び出しを開始します。 モーション補正コードテンプレートの使用方法の詳細については、「 [DIRECTX VA デバイスのコード例](example-code-for-directx-va-devices.md)」を参照してください。

次の手順では、VMR が COPP DDI の呼び出しを開始する方法について説明します。

1.  VMR がフィルターグラフに追加されると、ドライバーでサポートされているデバイスの一覧を取得するために、ディスプレイドライバーが提供する[*Ddmocompgetguids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)コールバック関数の呼び出しが開始されます。 DD\_MOTIONCOMPCALLBACK 構造体の**Getmocompguids**メンバーは、このコールバック関数を指します。 フィルターグラフの詳細については、「 [KS ミニドライバー Architecture](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)」を参照してください。

2.  DirectX VA COPP デバイス GUID が存在する場合、VMR は、現在のビデオセッションで COPP デバイスを初期化するために、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数への呼び出しを開始します。 DD\_MOTIONCOMPCALLBACKS の**Createmocomp**メンバーは、コールバック関数をポイントします。 *Ddmocompcreate*呼び出しでは、copp デバイス GUID へのポインターが、 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体の**lpguid**メンバーに指定されています。 COPP デバイス GUID は、次のように定義されています。

    ```cpp
    DEFINE_GUID(DXVA_COPPDevice, 0xd2457add,0x8999,0x45ed,0x8a,0x8a,0xd1,0xaa,0x04,0x7b,0xa4,0xd5);
    ```

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーが[*coppopenvideosession*](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)サンプル関数を実装している場合は、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数によって、 **coppopenvideosession**への呼び出しが開始されます。

3.  現在のビデオセッションで使用する可変長グラフィックスハードウェア証明書の長さを決定するために、VMR は、ディスプレイドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 [**DD\_MOTIONCOMPCALLBACK**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)の**rendermocomp**メンバーは、コールバック関数を指します。 **Ddmocomprender**呼び出しでは、 [**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)の**Dwfunction**メンバーは、 **DXVA\_COPPGetCertificateLengthFnCode** ( *DXVA*で定義) の値に設定されます。 この呼び出しでは、表示ドライバーは入力を受け取りません。つまり、DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは**NULL**になります。 表示ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを介して証明書の長さを返します。**Lpoutputdata**は DWORD データ型を指します。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーで[*COPPGetCertificateLength*](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength) sample 関数が実装されている場合、 **Ddmocomprender**コールバック関数によって*COPPGetCertificateLength*への呼び出しが開始されます。

4.  グラフィックスハードウェアによって使用される証明書を取得するために、VMR は、ディスプレイドライバーが提供する**Ddmocomprender**コールバック関数の呼び出しを開始します。 **Ddmocomprender**呼び出しでは、DD\_RENDERMOCOMPDATA の**dwfunction**メンバーは、 **DXVA\_COPPKeyExchangeFnCode** ( *DXVA*で定義) の値に設定されます。 この呼び出しでは、表示ドライバーは入力を受け取りません。つまり、DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは**NULL**になります。 DD\_RENDERMOCOMPDATA の**Lpbufferinfo**メンバーは、表示ドライバーが証明書を格納するために必要な領域を含む単一の RGB32 システムメモリサーフェイスを指します。 表示ドライバーは、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーを通じて生成された128ビットの乱数を返します。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーで[*COPPKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange) sample 関数が実装されている場合、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数によって*COPPKeyExchange*への呼び出しが開始されます。

5.  現在のビデオセッションを保護モードに設定するために、VMR は、ディスプレイドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、DD\_RENDERMOCOMPDATA の**dwfunction**メンバーは、 **DXVA\_COPPSequenceStartFnCode** ( *DXVA*で定義) の値に設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_coppsignature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsignature)構造体を指すことによって、入力コマンドとステータスシーケンスの開始コードを表示ドライバーに渡します。 ディスプレイドライバーは出力を返しません。つまり、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーは**NULL**になります。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーが[*coppsequencestart*](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)サンプル関数を実装している場合は、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数によって、 **coppsequencestart**への呼び出しが開始されます。

6.  DirectX VA COPP デバイスに関連付けられている物理コネクタの保護レベルを設定するために、VMR は、ディスプレイドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、DD\_RENDERMOCOMPDATA の**dwfunction**メンバーは、 **DXVA\_COPPCommandFnCode** ( *DXVA*で定義) の値に設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_coppcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)構造をポイントすることによって、入力パラメーターをディスプレイドライバーに渡します。 ディスプレイドライバーは出力を返しません。つまり、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーは**NULL**になります。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーが[*coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)サンプル関数を実装している場合は、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数によって、 *coppcommand*への呼び出しが開始されます。

7.  使用されている物理コネクタに関する保護情報を取得するために、VMR は、ディスプレイドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、DD\_RENDERMOCOMPDATA の**dwfunction**メンバーは、 **DXVA\_COPPQueryStatusFnCode** ( *DXVA*で定義) の値に設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_coppstatusinput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体を指すことによって、入力パラメーターをディスプレイドライバーに渡します。 表示ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを通じて出力を返します。**Lpoutputdata**は、 [**DXVA\_coppstatusoutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)構造体を指します。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーで[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus) sample 関数が実装されている場合、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数によって*COPPQueryStatus*への呼び出しが開始されます。

8.  VMR がそれ以上の COPP 操作を実行する必要がなくなった場合は、ディスプレイドライバーによって指定された[*Ddmocompdestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)コールバック関数が呼び出されます。 DD\_MOTIONCOMPCALLBACK の**Destroymocomp**メンバーは、コールバック関数を指します。

    ディスプレイドライバーは、COPP IOCTL を使用してビデオミニポートドライバーと通信する必要があります。 ビデオミニポートドライバーが[*coppclosevideosession*](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)サンプル関数を実装している場合は、 **Ddmocompdestroy**コールバック関数によって、 *coppclosevideosession*への呼び出しが開始されます。

9.  ドライバーは、DirectX VA COPP デバイスで使用されているすべてのリソースを解放します。

 

 





