---
title: ユーザー モード コンポーネントから DDI ProcAmp コントロールを呼び出す
description: ユーザー モード コンポーネントから DDI ProcAmp コントロールを呼び出す
ms.assetid: 1e4e19bb-eb4b-4db6-8947-429a1a414e4a
keywords:
- ProcAmp コントロール DDI WDK DirectX VA を呼び出す
- ユーザー モード コンポーネントは、WDK DirectX VA を呼び出します。
- ProcAmp WDK DirectX va なので、ユーザー モード コンポーネントからの呼び出し
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a6fd20cf863b0e7bac842b1ec421b149891ee44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537222"
---
# <a name="calling-the-procamp-control-ddi-from-a-user-mode-component"></a>ユーザー モード コンポーネントから DDI ProcAmp コントロールを呼び出す


## <span id="ddk_calling_the_procamp_control_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_PROCAMP_CONTROL_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


VMR などのユーザー モード コンポーネントへの呼び出しを開始する、 [ProcAmp コントロール DDI](https://msdn.microsoft.com/library/windows/hardware/ff569186)します。

VMR が ProcAmp コントロールの機能にアクセスできるように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](motion-compensation-callbacks.md)のメンバーが定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。

ドライバーの開発を簡素化するドライバー開発者は動き補正コード テンプレートを使用し、実装、 [ProcAmp コントロール サンプル関数](sample-functions-for-procamp-control.md)します。 動き補正テンプレートは、その ProcAmp コントロール ProcAmp コントロールの操作を実行するサンプル関数を呼び出します。 詳細については動き補正テンプレートを使用して、[DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)を参照してください。

次の手順では、VMR ProcAmp コントロール DDI への呼び出しを開始する方法について説明します。

1.  VMR はフィルターのグラフに追加するときに、ドライバーによって提供されるへの呼び出しを開始します。 [ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)ドライバーでサポートされているデバイスの一覧を取得するコールバック関数。 **GetMoCompGuids** DD のメンバー\_MOTIONCOMPCALLBACKS がこのコールバック関数をポイントします。 フィルターのグラフの詳細については、[KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)を参照してください。

2.  VMR への呼び出しを開始するインター コンテナー デバイス GUID が存在する場合、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)デバイスのインスタンスを作成するコールバック関数。 **CreateMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 **DdMoCompCreate**呼び出すには、GUID がで指定されたコンテナーのデバイスへのポインター、 **lpGuid**のメンバー、 [ **DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)構造体。 コンテナー デバイス GUID の定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  VMR を ProcAmp コントロール デバイスの機能を確認するには、ドライバーによって提供されるへの呼び出しを開始します[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 **RenderMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA、入力パラメーターに渡し、ドライバーを指す、 [ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_ProcAmpControlCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff564019)構造体。

    ドライバーが実装されている場合、 [ **ProcAmpControlQueryCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563949)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248) コールバック関数の呼び出し**ProcAmpControlQueryCaps**します。

4.  VMR がドライバーによって提供されるへの呼び出しを開始する、ハードウェアでサポートされている各 ProcAmp 調整プロパティの**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction** DD のメンバー\_RENDERMOCOMPDATA します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_ProcAmpControlQueryRange**](https://msdn.microsoft.com/library/windows/hardware/ff564032)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_VideoPropertyRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564083)構造体。

    ドライバーが実装されている場合、 [ **ProcAmpControlQueryRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563950)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248) コールバック関数の呼び出し**ProcAmpControlQueryRange**します。

5.  VMR がハードウェアの ProcAmp 調整機能を特定した後への呼び出しを開始します。 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656) ProcAmp コントロール デバイスのインスタンスを作成します。 *DdMoCompCreate*呼び出すには、GUID がで指定された ProcAmp 制御デバイスへのポインター、 **lpGuid** DD のメンバー\_CREATEMOCOMPDATA します。 GUID ProcAmp コントロール デバイスの定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVA_ProcAmpControlDevice, 0x9f200913,0x2ffd,0x4056,0x9f,0x1e,0xe1,0xb5,0x08,0xf2,0x2d,0xcf); 
    ```

    ドライバーが実装されている場合、 [ **ProcAmpControlOpenStream** ](https://msdn.microsoft.com/library/windows/hardware/ff564026)関数の場合、サンプル、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656) コールバック関数の呼び出し**ProcAmpControlOpenStream**します。

6.  操作を調整する各 ProcAmp、VMR はドライバーによって提供されるへの呼び出しを開始します**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction**のメンバー [ **DD\_RENDERMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551693)します。 **LpBufferInfo** DD のメンバー\_RENDERMOCOMPDATA が送信先と送信元のサーフェスを記述する 2 つのバッファーの配列を指します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_ProcAmpControlBlt**](https://msdn.microsoft.com/library/windows/hardware/ff564015)構造体。 ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ドライバーが実装されている場合、 [ **ProcAmpControlBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff564022)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**ProcAmpControlBlt**.

7.  VMR されなく必要がある場合、ドライバーによって提供される以上の ProcAmp コントロール操作を実行する[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)コールバック関数が呼び出されます。 **DestroyMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。

    ドライバーが実装されている場合、 [ **ProcAmpControlCloseStream** ](https://msdn.microsoft.com/library/windows/hardware/ff564025)関数の場合、サンプル、 **DdMoCompDestroy**コールバック関数の呼び出し**ProcAmpControlCloseStream**します。

8.  ドライバーは、ProcAmp コントロール デバイスによって使用されているリソースを解放します。

 

 





