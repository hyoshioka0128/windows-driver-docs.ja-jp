---
title: AGP ヒープの管理
description: AGP ヒープの管理
ms.assetid: edeed3bc-c107-4286-9d5a-7fdef89cc4e1
keywords:
- ヒープ WDK DirectDraw
- メモリ WDK DirectDraw、ヒープを表示する
- 非ローカルディスプレイメモリ WDK DirectDraw、ヒープ
- AGP WDK DirectDraw、ヒープ
- AGP サポート WDK DirectDraw、ヒープの描画
- DirectDraw AGP サポート WDK Windows 2000 display、ヒープ
- メモリ WDK DirectDraw AGP、ヒープ
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4e562657bf9cf299c47fc183959ccc29f84912
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840585"
---
# <a name="managing-agp-heaps"></a>AGP ヒープの管理


## <span id="ddk_managing_agp_heaps_gg"></span><span id="DDK_MANAGING_AGP_HEAPS_GG"></span>


**このトピックは、Windows NT ベースのオペレーティングシステムにのみ適用されます。**

ドライバーは、DirectX ランタイムから受信した通知を使用して AGP ヒープを管理できます。 ドライバーは、次の値を使用する**GetDriverInfo2**要求としてランタイムからの通知を受信します。

-   D3DGDI2\_TYPE\_遅延\_AGP\_認識

-   D3DGDI2\_TYPE\_FREE\_遅延\_AGP

-   D3DGDI2\_TYPE\_\_AGP\_の解放を遅延します

**GetDriverInfo2**要求の詳細については、「 [GetDriverInfo2 のサポート](supporting-getdriverinfo2.md)」を参照してください。

ディスプレイデバイスが作成されると、ディスプレイドライバーは、D3DGDI2\_\_\_\_TYPE を使用して**GetDriverInfo2**要求を受信します。この要求は、ドライバーが他のデバイスを無効にする必要があるかどうかを判断するために使用します。AGP ヒープを処理するメカニズムを使用し、代わりに D3DGDI2\_TYPE\_使用すると、\_遅延\_AGP および D3DGDI2\_の種類が解放され、それ以降にランタイムが送信する通知が解放されます。 D3DGDI2\_の種類\_遅延\_AGP\_に対応する通知を使用すると、DirectX ランタイムは、の**Lpvdata**メンバー内にある、 [**DD\_遅延\_の agp\_対応\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_deferred_agp_aware_data)構造へのポインターを提供します。[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体。

ドライバーは、表示モードの変更が発生する前に、\_AGP\_\_を延期すること\_で、 **GetDriverInfo2**要求を受信することがあります。 DirectX ランタイムは、ランタイムが表示モードの変更を実行する場合にのみ、この通知を送信します。 ドライバーは、サーフェイスを作成したプロセスに対してサーフェスを破棄するプロセスのプロセス識別子 (PID) を確認する必要があります。 Pid が異なる場合は、アプリケーションがメモリを使用している可能性があるため、ドライバーは AGP メモリのユーザーモードマッピングを破棄しないようにする必要があります。

このドライバーは、プロセス内のすべてのディスプレイデバイスがサーフェイス、テクスチャ、頂点バッファー、およびインデックスバッファーを使用して停止したときに、D3DGDI2\_TYPE\_\_\_を使用して、 **GetDriverInfo2**要求を受信します。表示モードの変更時にロックされていた。 この通知は、AGP メモリのすべてのユーザーモードマッピングを安全に破棄できることをドライバーに通知します。

D3DGDI2\_の種類では\_\_の AGP\_解放および D3DGDI2\_を延期\_の\_の遅延\_を延期\_、ランタイムは、DD\_解放 @no__ を指すポインターを提供[**t_12_ AGP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_free_deferred_agp_data) 、DD\_GETDRIVERINFODATA データ構造の**Lpvdata**メンバーのデータ構造です。 DD\_FREE\_遅延\_AGP\_データの**Dwprocessid**メンバーは、agp メモリを破棄するプロセスの PID を指定します。

アプリケーションを終了するには、ランタイムが D3DGDI2\_TYPE を送信する必要があることに注意してください。\_は、\_遅延\_AGP 通知をドライバーに送信します。 そのため、ドライバーは、 [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)関数への呼び出しを受け取ったときに、AGP メモリのすべてのユーザーモードマッピングを解放する必要があります。

 

 





