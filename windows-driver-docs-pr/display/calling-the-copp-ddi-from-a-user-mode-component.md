---
title: ユーザー モード コンポーネントからの COPP DDI の呼び出し
description: ユーザー モード コンポーネントからの COPP DDI の呼び出し
ms.assetid: f7ce10d3-bf52-4bfd-9ae8-63213a59d1c9
keywords:
- COPP DDI WDK DirectX VA を呼び出す
- ユーザー モード コンポーネントは、WDK DirectX VA を呼び出します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7a054180da99e52402cc6958918973569dac0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572111"
---
# <a name="calling-the-copp-ddi-from-a-user-mode-component"></a>ユーザー モード コンポーネントからの COPP DDI の呼び出し


## <span id="ddk_calling_the_copp_ddi_from_a_user_mode_component_gg"></span><span id="DDK_CALLING_THE_COPP_DDI_FROM_A_USER_MODE_COMPONENT_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

VMR などのユーザー モード コンポーネントは、COPP DDI への呼び出しを開始します。

ディスプレイ ドライバーが実装する必要があります VMR が、グラフィックス アダプターのビデオ出力に保護を適用するビデオのミニポート ドライバーを通知するため、[補正コールバック関数のモーション](motion-compensation-callbacks.md)、のメンバーが定義されています。[**DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。

ドライバーの開発を簡素化するドライバー開発者は動き補正コード テンプレートを使用し、COPP Ioctl を実装し、 [COPP サンプル関数](sample-functions-for-copp.md)します。 ディスプレイ ドライバーとビデオのミニポート ドライバーは、COPP Ioctl を使用して通信します。 詳細については、次を参照してください。 [COPP DDI をディスプレイ ドライバーから呼び出す](calling-the-copp-ddi-from-the-display-driver.md)します。 動き補正コード テンプレートは、COPP サンプル関数の呼び出しを開始します。 詳細については動き補正コード テンプレートを使用して、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

次の手順では、VMR COPP DDI への呼び出しを開始する方法について説明します。

1.  フィルターのグラフに VMR を追加するときに、ドライバーによって提供される、表示するための呼び出しを開始します。 [ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)ドライバーでサポートされているデバイスの一覧を取得するコールバック関数。 **GetMoCompGuids** 、DD のメンバー\_MOTIONCOMPCALLBACKS このコールバック関数へのポインターを構造体します。 フィルターのグラフの詳細については、次を参照してください。 [KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)します。

2.  DirectX VA COPP デバイス GUID が存在するかどうかは、VMR への呼び出しを開始する、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656) COPP デバイスを現在のビデオ セッションを初期化するためにコールバック関数。 **CreateMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。 *DdMoCompCreate*呼び出すには、GUID がで指定された COPP デバイスへのポインター、 **lpGuid**のメンバー、 [ **DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)構造体。 GUID COPP デバイスの定義は次のとおりです。

    ```cpp
    DEFINE_GUID(DXVA_COPPDevice, 0xd2457add,0x8999,0x45ed,0x8a,0x8a,0xd1,0xaa,0x04,0x7b,0xa4,0xd5);
    ```

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPOpenVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539650)関数の場合、サンプル、 [ *DdMoCompCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff549656)コールバック関数への呼び出しを開始する**COPPOpenVideoSession**します。

3.  VMR を現在のビデオ セッションのために使用する必要があります可変長のグラフィックス ハードウェアの証明書の長さを確認するには、ドライバーによって提供される表示の呼び出しを開始します[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 **RenderMoComp**のメンバー [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)コールバック関数をポイントします。 **DdMoCompRender**を呼び出すには、 **dwFunction**のメンバー [ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693) 値に設定されています。**DXVA\_COPPGetCertificateLengthFnCode** (で定義されている*dxva.h*)。 この呼び出しで、ディスプレイ ドライバーが任意の入力を受信しませんつまり、 **lpInputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。 ディスプレイ ドライバーがを介して証明書の長さを返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData** DWORD データ型が参照します。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)関数の場合、サンプル、 **DdMoCompRender**コールバック関数は、への呼び出しを開始します。*COPPGetCertificateLength*します。

4.  VMR をグラフィックス ハードウェアで使用される証明書を取得するには、ドライバーによって提供される、表示するための呼び出しを開始する**DdMoCompRender**コールバック関数。 **DdMoCompRender**を呼び出すには、 **dwFunction** DD のメンバー\_値に設定されている RENDERMOCOMPDATA **DXVA\_COPPKeyExchangeFnCode** (定義されている*dxva.h*)。 この呼び出しで、ディスプレイ ドライバーが任意の入力を受信しませんつまり、 **lpInputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。 **LpBufferInfo** DD のメンバー\_RENDERMOCOMPDATA が証明書を格納する、ディスプレイ ドライバーに必要な領域を含む 1 つの RGB32 システム メモリ サーフェスを指します。 ディスプレイ ドライバーを使用して、生成される 128 ビットのランダムな数値を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA します。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPKeyExchange* ](https://msdn.microsoft.com/library/windows/hardware/ff539646)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数呼び出しを開始する*COPPKeyExchange*します。

5.  VMR を現在のビデオ セッションを保護モードを設定するには、ドライバーによって提供される表示の呼び出しを開始します[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 *DdMoCompRender*を呼び出すには、 **dwFunction** DD のメンバー\_値に設定されている RENDERMOCOMPDATA **DXVA\_COPPSequenceStartFnCode**(で定義されている*dxva.h*)。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA 入力コマンドと状態シーケンス開始コードに渡し、ディスプレイ ドライバー、完成したを指す[ **DXVA\_COPPSignature** ](https://msdn.microsoft.com/library/windows/hardware/ff563150)構造体。 ディスプレイ ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数呼び出しを開始する**COPPSequenceStart**します。

6.  VMR を DirectX VA COPP デバイスに関連付けられた物理コネクタでの保護レベルを設定するには、ドライバーによって提供される、表示するための呼び出しを開始する[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 *DdMoCompRender*を呼び出すには、 **dwFunction** DD のメンバー\_値に設定されている RENDERMOCOMPDATA **DXVA\_COPPCommandFnCode** (定義されている*dxva.h*)。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA は、完成したをポイントして、ディスプレイ ドライバーに入力パラメーターを渡します[ **DXVA\_COPPCommand**](https://msdn.microsoft.com/library/windows/hardware/ff563141)構造体。 ディスプレイ ドライバーには、任意の出力は返しません。つまり、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA は**NULL**します。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数呼び出しを開始する*COPPCommand*します。

7.  VMR を使用している物理コネクタに関する保護情報を取得するには、ドライバーによって提供される表示の呼び出しを開始します[ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数。 *DdMoCompRender*を呼び出すには、 **dwFunction** DD のメンバー\_値に設定されている RENDERMOCOMPDATA **DXVA\_COPPQueryStatusFnCode** (定義されている*dxva.h*)。 **LpInputData** DD のメンバー\_RENDERMOCOMPDATA は、完成したをポイントして、ディスプレイ ドライバーに入力パラメーターを渡します[ **DXVA\_COPPStatusInput**](https://msdn.microsoft.com/library/windows/hardware/ff563899)構造体。 ディスプレイ ドライバーを通じてその出力を返します、 **lpOutputData** DD のメンバー\_RENDERMOCOMPDATA;**lpOutputData**を指す、 [ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)構造体。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)関数の場合、サンプル、 [ *DdMoCompRender* ](https://msdn.microsoft.com/library/windows/hardware/ff550248)コールバック関数呼び出しを開始する*COPPQueryStatus*します。

8.  VMR COPP 操作を実行する必要がなくなった、ときに、ディスプレイ ドライバーによって提供される[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)コールバック関数が呼び出されます。 **DestroyMoComp** DD のメンバー\_MOTIONCOMPCALLBACKS がコールバック関数を指します。

    ディスプレイ ドライバーは、COPP IOCTL を使用して、ビデオのミニポート ドライバーと通信する必要があります。 ビデオのミニポート ドライバーが実装されている場合、 [ *COPPCloseVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539638)関数の場合、サンプル、 **DdMoCompDestroy** への呼び出しを開始するコールバック関数*COPPCloseVideoSession*します。

9.  ドライバーは、DirectX VA COPP デバイスによって使用されているリソースを離します。

 

 





