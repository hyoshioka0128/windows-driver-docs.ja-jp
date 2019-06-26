---
title: ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し
description: ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し
ms.assetid: 1e4e19bb-eb4b-4db6-8947-429a1a414e4a
keywords:
- ProcAmp コントロール DDI WDK DirectX VA を呼び出す
- ユーザー モード コンポーネントは、WDK DirectX VA を呼び出します。
- ProcAmp WDK DirectX va なので、ユーザー モード コンポーネントからの呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fce8f52fe26f7588bc17295944dae044222feffb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384599"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>ユーザー モード コンポーネントからの ProcAmp コントロール DDI の呼び出し


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


VMR などのユーザー モード コンポーネントへの呼び出しを開始する、 [ProcAmp コントロール DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi)します。

VMR が ProcAmp コントロールの機能にアクセスできるように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](motion-compensation-callbacks.md)のメンバーが定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。

ドライバーの開発を簡素化するドライバー開発者は動き補正コード テンプレートを使用し、実装、 [ProcAmp コントロール サンプル関数](sample-functions-for-procamp-control.md)します。 動き補正テンプレートは、その ProcAmp コントロール ProcAmp コントロールの操作を実行するサンプル関数を呼び出します。 詳細については動き補正テンプレートを使用して、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

次の手順では、VMR ProcAmp コントロール DDI への呼び出しを開始する方法について説明します。

1.  VMR はフィルターのグラフに追加するときに、ドライバーによって提供されるへの呼び出しを開始します。 [ *DdMoCompGetGuids* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)ドライバーでサポートされているデバイスの一覧を取得するコールバック関数。 **GetMoCompGuids** DD のメンバー\_MOTIONCOMPCALLBACKS がこのコールバック関数をポイントします。 フィルターのグラフの詳細については、次を参照してください。 [KS ミニドライバー アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)します。

2.  VMR への呼び出しを開始するインター コンテナー デバイス GUID が存在する場合、 [ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)デバイスのインスタンスを作成するコールバック関数。 **CreateMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 **DdMoCompCreate**呼び出すには、GUID がで指定されたコンテナーのデバイスへのポインター、 **lpGuid**のメンバー、 [ **DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体。 コンテナー デバイス GUID の定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  VMR を ProcAmp コントロール デバイスの機能を確認するには、ドライバーによって提供されるへの呼び出しを開始します[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数。 **RenderMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)構造体。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA、入力パラメーターに渡し、ドライバーを指す、 [ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_ProcAmpControlCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolcaps)構造体。

    ドライバーが実装されている場合、 [ **ProcAmpControlQueryCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps)関数の場合、サンプル、 [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) コールバック関数の呼び出し**ProcAmpControlQueryCaps**します。

4.  VMR がドライバーによって提供されるへの呼び出しを開始する、ハードウェアでサポートされている各 ProcAmp 調整プロパティの**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction** DD のメンバー\_RENDERMOCOMPDATA します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_ProcAmpControlQueryRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolqueryrange)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_VideoPropertyRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videopropertyrange)構造体。

    ドライバーが実装されている場合、 [ **ProcAmpControlQueryRange** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange)関数の場合、サンプル、 [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) コールバック関数の呼び出し**ProcAmpControlQueryRange**します。

5.  VMR がハードウェアの ProcAmp 調整機能を特定した後への呼び出しを開始します。 [ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) ProcAmp コントロール デバイスのインスタンスを作成します。 *DdMoCompCreate*呼び出すには、GUID がで指定された ProcAmp 制御デバイスへのポインター、 **lpGuid** DD のメンバー\_CREATEMOCOMPDATA します。 GUID ProcAmp コントロール デバイスの定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    ドライバーが実装されている場合、 [ **ProcAmpControlOpenStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolopenstream)関数の場合、サンプル、 [ *DdMoCompCreate* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create) コールバック関数の呼び出し**ProcAmpControlOpenStream**します。

6.  操作を調整する各 ProcAmp、VMR はドライバーによって提供されるへの呼び出しを開始します**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction**のメンバー [ **DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)します。 **LpBufferInfo** DD のメンバー\_RENDERMOCOMPDATA が送信先と送信元のサーフェスを記述する 2 つのバッファーの配列を指します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_ProcAmpControlBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_procampcontrolblt)構造体。 ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ドライバーが実装されている場合、 [ **ProcAmpControlBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolblt)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**ProcAmpControlBlt**.

7.  VMR されなく必要がある場合、ドライバーによって提供される以上の ProcAmp コントロール操作を実行する[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)コールバック関数が呼び出されます。 **DestroyMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。

    ドライバーが実装されている場合、 [ **ProcAmpControlCloseStream** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-procampcontroldeviceclass-procampcontrolclosestream)関数の場合、サンプル、 **DdMoCompDestroy**コールバック関数の呼び出し**ProcAmpControlCloseStream**します。

8.  ドライバーは、ProcAmp コントロール デバイスによって使用されているリソースを解放します。

 

 





