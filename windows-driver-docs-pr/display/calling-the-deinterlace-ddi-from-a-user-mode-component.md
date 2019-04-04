---
title: ユーザー モード コンポーネントからのデインターレース DDI の呼び出し
description: ユーザー モード コンポーネントからのデインターレース DDI の呼び出し
ms.assetid: 3ec18c7e-02dc-4607-b280-3ca1bc5d2839
keywords:
- 呼び出すは、DDI WDK DirectX VA インター レースを解除します。
- ユーザー モード コンポーネントは、WDK DirectX VA を呼び出します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cab21db2eb07227204e536c95ce28e053a5d05f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572336"
---
# <a name="calling-the-deinterlace-ddi-from-a-user-mode-component"></a>ユーザー モード コンポーネントからのデインターレース DDI の呼び出し


## <span id="ddk_calling_the_deinterlace_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_DEINTERLACE_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


VMR などのユーザー モード コンポーネントは、デインター レース DDI への呼び出しを開始します。

VMR インター レースを解除して、ビデオ コンテンツのフレーム レートの変換を実行できる、ように、ディスプレイ ドライバーが実装する必要があります、[補正コールバック関数のモーション](motion-compensation-callbacks.md)のメンバーが定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。

ドライバーの開発を簡素化するドライバー開発者は動き補正コード テンプレートを使用し、実装、[サンプル関数をデインター レース](sample-functions-for-deinterlacing.md)します。 動き補正テンプレートでは、ビデオ コンテンツ デインター レース、フレーム レートの変換を実行するデインター レース サンプル関数を呼び出します。 詳細については動き補正テンプレートを使用して、[DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)を参照してください。

次の手順では、VMR インター DDI への呼び出しを開始する方法について説明します。

1.  VMR はフィルターのグラフに追加するときに、ドライバーによって提供されるへの呼び出しを開始します。 [ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)ドライバーでサポートされているデバイスの一覧を取得するコールバック関数。 **GetMoCompGuids** 、DD のメンバー\_MOTIONCOMPCALLBACKS このコールバック関数へのポインターを構造体します。 フィルターのグラフの詳細については、[KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)を参照してください。

2.  VMR への呼び出しを開始するインター コンテナー デバイス GUID が存在する場合、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)デバイスのインスタンスを作成するコールバック関数。 **CreateMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 *DdMoCompCreate*呼び出すには、GUID がで指定されたコンテナーのデバイスへのポインター、 **lpGuid**のメンバー、 [ **DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)構造体。 コンテナー デバイス GUID の定義は次のとおりです。
    ```cpp
    DEFINE_GUID(DXVA_DeinterlaceContainerDevice, 0x0e85cb93,0x3046,0x4ff0,0xae,0xcc,0xd5,0x8c,0xb5,0xf0,0x35,0xfd);
    ```

3.  VMR を特定の入力ビデオ形式の使用可能なデインター レースまたはフレーム レート変換モードを決定するには、ドライバーによって提供されるへの呼び出しを開始する[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 **RenderMoComp**のメンバー [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)コールバック関数をポイントします。 **DdMoCompRender**を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction**のメンバー、 [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)構造体。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_DeinterlaceQueryAvailableModes** ](https://msdn.microsoft.com/library/windows/hardware/ff563951)構造体。

    ドライバーが実装されている場合、 [ **DeinterlaceQueryAvailableModes** ](https://msdn.microsoft.com/library/windows/hardware/ff563943)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**DeinterlaceQueryAvailableModes**します。

4.  VMR がドライバーによって提供されるへの呼び出しを開始する各インター レース、ドライバーによってサポートされているモードを解除の**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **DXVA\_DeinterlaceQueryModeCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction** DD のメンバー\_RENDERMOCOMPDATA します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_DeinterlaceQueryModeCaps**](https://msdn.microsoft.com/library/windows/hardware/ff563956)構造体。 ドライバーはその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)構造体。

    ドライバーが実装されている場合、 [ **DeinterlaceQueryModeCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563946)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**DeinterlaceQueryModeCaps**します。

5.  インター レース モード (たとえば、bob デインター レース) の特定の機能を解除 VMR が、デインター レースを決定した後への呼び出しが開始[ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)のインスタンスを作成しますインター レース モードのデバイス (たとえば、インター bob デバイス) を解除します。 *DdMoCompCreate*呼び出すには、GUID がで指定されたインター モードのデバイスへのポインター、 **lpGuid** DD のメンバー\_CREATEMOCOMPDATA します。 インター bob デバイス GUID の定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVAp_DeinterlaceBobDevice, 0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
    ```

    ドライバーが実装されている場合、 [ **DeinterlaceOpenStream** ](https://msdn.microsoft.com/library/windows/hardware/ff563935)関数の場合、サンプル、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656) コールバック関数の呼び出し**DeinterlaceOpenStream**します。

6.  VMR デインター レース操作ごとに、ドライバーによって提供されるへの呼び出しを開始する[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 *DdMoCompRender*を呼び出すには、 **DXVA\_ProcAmpControlQueryCapsFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction** DD のメンバー\_RENDERMOCOMPDATA します。 **LpBufferInfo** DD のメンバー\_RENDERMOCOMPDATA が宛先表面、および各入力ビデオのソースのサンプルについて説明するバッファーの配列を指します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563912)構造体。 ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ドライバーが実装されている場合、 [ **DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563924)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**DeinterlaceBlt**します。

7.  各組み合わせデインター レース、サブストリーム複合操作の場合、VMR Microsoft Windows Server 2003 SP1 以降と Windows XP SP2、ドライバーによって提供されるへの呼び出しを後で開始[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 *DdMoCompRender*を呼び出すには、 **DXVA\_DeinterlaceBltExFnCode**定数 (で定義されている*dxva.h*) 設定されている、 **dwFunction** DD のメンバー\_RENDERMOCOMPDATA します。 **LpBufferInfo** DD のメンバー\_RENDERMOCOMPDATA が宛先表面と各入力ビデオ ソース サンプルのサーフェスを説明するバッファーの配列を指します。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA がドライバーに完成したをポイントして、入力パラメーターを渡します[ **DXVA\_DeinterlaceBltEx**](https://msdn.microsoft.com/library/windows/hardware/ff563915)構造体。 ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ドライバーが実装されている場合、 [ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)関数の場合、サンプル、 **DdMoCompRender**コールバック関数の呼び出し**DeinterlaceBltEx**.

8.  VMR を実行する必要がなくなったときにいずれかのよりインター レースを解除操作は、ドライバーによって提供される[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)コールバック関数が呼び出されます。 **DestroyMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。

    ドライバーが実装されている場合、 [ **DeinterlaceCloseStream** ](https://msdn.microsoft.com/library/windows/hardware/ff563931)関数の場合、サンプル、 [ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664) コールバック関数の呼び出し**DeinterlaceCloseStream**します。

9.  ドライバーは、インター モードのデバイスで使用されたリソースを解放します。

 

 





