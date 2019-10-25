---
title: ユーザーモードコンポーネントからのノンインターレース DDI の呼び出し
description: ユーザーモードコンポーネントからのノンインターレース DDI の呼び出し
ms.assetid: 3ec18c7e-02dc-4607-b280-3ca1bc5d2839
keywords:
- ノンインターレース DDI WDK DirectX VA を呼び出しています
- ユーザーモードコンポーネントが WDK DirectX VA を呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83a277076d3e93d74347250d3e8a6d083c3e16dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839818"
---
# <a name="calling-the-deinterlace-ddi-from-a-user-mode-component"></a>ユーザーモードコンポーネントからのノンインターレース DDI の呼び出し


## <span id="ddk_calling_the_deinterlace_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_DEINTERLACE_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


VMR などのユーザーモードコンポーネントによって、ノンインターレース DDI の呼び出しが開始されます。

VMR がビデオコンテンツに対してフレームレート変換をインターレース解除して実行できるように、表示ドライバーは、 [**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体のメンバーによって定義される[モーション補正コールバック関数](motion-compensation-callbacks.md)を実装する必要があります.

ドライバーの開発を簡単にするために、ドライバーライターは、モーション補正コードテンプレートを使用して、[インターレース解除サンプル関数](sample-functions-for-deinterlacing.md)を実装できます。 モーション補正テンプレートは、インターレース解除のサンプル関数を呼び出して、ビデオコンテンツに対してインターレース解除やフレームレート変換を実行します。 モーション補正テンプレートの使用方法の詳細については、「 [DIRECTX VA デバイスのコード例](example-code-for-directx-va-devices.md)」を参照してください。

次の手順では、VMR がノンインターレース DDI の呼び出しを開始する方法について説明します。

1.  VMR がフィルターグラフに追加されると、ドライバーが提供する[*Ddmocompgetguids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)コールバック関数への呼び出しが開始され、ドライバーでサポートされているデバイスの一覧が取得されます。 DD\_MOTIONCOMPCALLBACK 構造体の**Getmocompguids**メンバーは、このコールバック関数を指します。 フィルターグラフの詳細については、「 [KS ミニドライバー Architecture](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)」を参照してください。

2.  ノンインターレースコンテナーデバイス GUID が存在する場合、VMR は、デバイスのインスタンスを作成するために、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数への呼び出しを開始します。 DD\_MOTIONCOMPCALLBACKS の**Createmocomp**メンバーは、コールバック関数をポイントします。 *Ddmocompcreate*呼び出しでは、コンテナーデバイス GUID へのポインターが、 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体の**lpguid**メンバーに指定されています。 コンテナーデバイス GUID は、次のように定義されています。
    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  VMR は、特定の入力ビデオ形式に対して使用可能なノンインターレースまたはフレームレート変換モードを特定するために、ドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 [**DD\_MOTIONCOMPCALLBACK**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)の**rendermocomp**メンバーは、コールバック関数を指します。 **Ddmocomprender**呼び出しでは、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 ( *DXVA*で定義されています) が、 [**DD\_Rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを通じて出力を返します。**Lpoutputdata**は、 [**DXVA\_DeinterlaceQueryAvailableModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)構造体を指します。

    ドライバーが[**DeinterlaceQueryAvailableModes**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes) sample 関数を実装している場合、 **Ddmocomprender**コールバック関数は**DeinterlaceQueryAvailableModes**を呼び出します。

4.  ドライバーでサポートされているノンインターレースモードごとに、VMR はドライバーが提供する**Ddmocomprender**コールバック関数の呼び出しを開始します。 **Ddmocomprender**呼び出しでは、 **DXVA\_DeinterlaceQueryModeCapsFnCode**定数 (DXVA で定義されてい*ます*) が、DD\_Rendermocompdata の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequerymodecaps)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを通じて出力を返します。**Lpoutputdata**は、 [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体を指します。

    ドライバーが[**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps) sample 関数を実装している場合、 **Ddmocomprender**コールバック関数は**DeinterlaceQueryModeCaps**を呼び出します。

5.  VMR が特定のノンインターレースモード (たとえば、bob ノンインターレース) のノンインターレース機能を決定した後、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)への呼び出しを開始して、ノンインターレースモードデバイスのインスタンスを作成します (たとえば、インターレース bobデバイス)。 *Ddmocompcreate*呼び出しでは、ノンインターレースモードデバイス GUID へのポインターが、DD\_CREATEMOCOMPDATA の**lpguid**メンバーに指定されています。 インターレース解除 bob デバイス GUID は、次のように定義されています。

    ```cpp
    DEFINE_GUID(DXVAp_DeinterlaceBobDevice, 0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
    ```

    ドライバーが[**DeinterlaceOpenStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream) sample 関数を実装している場合、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数は**DeinterlaceOpenStream**を呼び出します。

6.  VMR は、各インターレース解除操作に対して、ドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (DXVA で定義されてい*ます*) が、DD\_Rendermocompdata の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpbufferinfo**メンバーは、ターゲットサーフェスと各入力ビデオソースのサンプルを記述するバッファーの配列を指します。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは出力を返しません。つまり、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーは**NULL**になります。

    ドライバーが[**DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt) sample 関数を実装している場合、 **Ddmocomprender**コールバック関数は**DeinterlaceBlt**を呼び出します。

7.  各組み合わせのノンインターレース化およびサブストリーム合成操作では、Microsoft Windows Server 2003 SP1 以降および Windows XP SP2 以降の VMR が、ドライバーによって提供された[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 *Ddmocomprender*呼び出しでは、 **DXVA\_DeinterlaceBltExFnCode**定数 (DXVA で定義されてい*ます*) が、DD\_Rendermocompdata の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpbufferinfo**メンバーは、各入力ビデオソースのサンプルのターゲットサーフェスとサーフェスを記述するバッファーの配列を指します。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは出力を返しません。つまり、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーは**NULL**になります。

    ドライバーが[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex) sample 関数を実装している場合、 **Ddmocomprender**コールバック関数は**DeinterlaceBltEx**を呼び出します。

8.  VMR がより多くのノンインターレース操作を実行する必要がなくなった場合、ドライバーによって提供された[*Ddmocompdestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)のコールバック関数が呼び出されます。 DD\_MOTIONCOMPCALLBACK の**Destroymocomp**メンバーは、コールバック関数を指します。

    ドライバーが[**DeinterlaceCloseStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream) sample 関数を実装している場合、 [*Ddmocompdestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)コールバック関数は**DeinterlaceCloseStream**を呼び出します。

9.  次に、ドライバーは、ノンインターレースモードデバイスで使用されているすべてのリソースを解放します。

 

 





