---
title: ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し
description: ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し
ms.assetid: 1e4e19bb-eb4b-4db6-8947-429a1a414e4a
keywords:
- ProcAmp control DDI WDK DirectX VA を呼び出しています
- ユーザーモードコンポーネントが WDK DirectX VA を呼び出す
- ProcAmp WDK DirectX VA、ユーザーモードコンポーネントからの呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b35db8836b310f35abc334ca4805defce94690
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839059"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


VMR などのユーザーモードコンポーネントは、 [ProcAmp CONTROL DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi)の呼び出しを開始します。

VMR が ProcAmp 制御機能にアクセスできるようにするには、表示ドライバーが、 [**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体のメンバーによって定義される[モーション補正コールバック関数](motion-compensation-callbacks.md)を実装する必要があります。

ドライバーの開発を簡単にするために、ドライバー作成者は、モーション補正コードテンプレートを使用して、 [ProcAmp コントロールのサンプル関数](sample-functions-for-procamp-control.md)を実装できます。 モーション補正テンプレートは、ProcAmp コントロールのサンプル関数を呼び出して、ProcAmp の制御操作を実行します。 モーション補正テンプレートの使用方法の詳細については、「 [DIRECTX VA デバイスのコード例](example-code-for-directx-va-devices.md)」を参照してください。

次の手順では、VMR が ProcAmp Control DDI の呼び出しを開始する方法について説明します。

1.  VMR がフィルターグラフに追加されると、ドライバーが提供する[*Ddmocompgetguids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)コールバック関数への呼び出しが開始され、ドライバーでサポートされているデバイスの一覧が取得されます。 DD\_MOTIONCOMPCALLBACK の**Getmocompguids**メンバーは、このコールバック関数を指します。 フィルターグラフの詳細については、「 [KS ミニドライバー Architecture](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)」を参照してください。

2.  ノンインターレースコンテナーデバイス GUID が存在する場合、VMR は、デバイスのインスタンスを作成するために、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数への呼び出しを開始します。 DD\_MOTIONCOMPCALLBACKS の**Createmocomp**メンバーは、コールバック関数をポイントします。 **Ddmocompcreate**呼び出しでは、コンテナーデバイス GUID へのポインターが、 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体の**lpguid**メンバーに指定されています。 コンテナーデバイス GUID は、次のように定義されています。

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  VMR は、ProcAmp コントロールデバイスの機能を確認するために、ドライバーが提供する[*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数の呼び出しを開始します。 DD\_MOTIONCOMPCALLBACK の**Rendermocomp**メンバーは、コールバック関数を指します。 **Ddmocomprender**呼び出しでは、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 ( *DXVA*で定義されています) が、 [**DD\_Rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、 [**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを通じて出力を返します。**Lpoutputdata**は、 [**DXVA\_ProcAmpControlCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)構造体を指します。

    ドライバーが[**ProcAmpControlQueryCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps) sample 関数を実装している場合、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数は**ProcAmpControlQueryCaps**を呼び出します。

4.  ハードウェアでサポートされている各 ProcAmp 調整プロパティについて、VMR はドライバーが提供する**Ddmocomprender**コールバック関数の呼び出しを開始します。 **Ddmocomprender**呼び出しでは、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (DXVA で定義されてい*ます*) が、DD\_Rendermocompdata の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolqueryrange)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは、DD\_RENDERMOCOMPDATA; の**Lpoutputdata**メンバーを通じて出力を返します。**Lpoutputdata**は、 [**DXVA\_videopropertyrange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videopropertyrange)構造体を指します。

    ドライバーが[**ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange) sample 関数を実装している場合、 [*Ddmocomprender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数は**ProcAmpControlQueryRange**を呼び出します。

5.  VMR は、ハードウェアの ProcAmp 調整機能を決定した後、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)への呼び出しを開始して ProcAmp コントロールデバイスのインスタンスを作成します。 *Ddmocompcreate*呼び出しでは、ProcAmp コントロールデバイス GUID へのポインターが、DD\_CREATEMOCOMPDATA の**lpguid**メンバーに指定されています。 ProcAmp コントロールデバイス GUID は、次のように定義されています。

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    ドライバーが[**ProcAmpControlOpenStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream) sample 関数を実装している場合、 [*Ddmocompcreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)コールバック関数は**ProcAmpControlOpenStream**を呼び出します。

6.  ProcAmp の調整操作ごとに、VMR はドライバーが提供する**Ddmocomprender**コールバック関数の呼び出しを開始します。 **Ddmocomprender**呼び出しでは、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 ( *DXVA*で定義されています) が、 [**DD\_rendermocompdata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)の**dwfunction**メンバーで設定されます。 DD\_RENDERMOCOMPDATA の**Lpbufferinfo**メンバーは、コピー先とコピー元のサーフェイスを記述する2つのバッファーの配列を指します。 DD\_RENDERMOCOMPDATA の**Lpinputdata**メンバーは、完了した[**DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolblt)構造体を指すことによって、入力パラメーターをドライバーに渡します。 ドライバーは出力を返しません。つまり、DD\_RENDERMOCOMPDATA の**Lpoutputdata**メンバーは**NULL**になります。

    ドライバーが[**ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt) sample 関数を実装している場合、 **Ddmocomprender**コールバック関数は**ProcAmpControlBlt**を呼び出します。

7.  VMR がそれ以上の ProcAmp 制御操作を実行する必要がなくなった場合、ドライバーによって提供された[*Ddmocompdestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)のコールバック関数が呼び出されます。 DD\_MOTIONCOMPCALLBACK の**Destroymocomp**メンバーは、コールバック関数を指します。

    ドライバーが[**ProcAmpControlCloseStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream) sample 関数を実装している場合、 **Ddmocompdestroy**コールバック関数は**ProcAmpControlCloseStream**を呼び出します。

8.  ドライバーは、ProcAmp コントロールデバイスによって使用されているすべてのリソースを解放します。

 

 





