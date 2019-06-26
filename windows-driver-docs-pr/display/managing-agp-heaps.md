---
title: AGP ヒープの管理
description: AGP ヒープの管理
ms.assetid: edeed3bc-c107-4286-9d5a-7fdef89cc4e1
keywords:
- ヒープ WDK DirectDraw
- ヒープ メモリ WDK の DirectDraw を表示します。
- WDK DirectDraw、ヒープの非ローカルの表示メモリ
- AGP WDK DirectDraw、ヒープ
- ヒープ AGP サポート WDK DirectDraw を描画するには、
- DirectDraw AGP サポート WDK Windows 2000 の表示、ヒープ
- WDK DirectDraw AGP、ヒープ メモリ
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 237a030332369aed342e70f139cb8398a569a054
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379017"
---
# <a name="managing-agp-heaps"></a>AGP ヒープの管理


## <span id="ddk_managing_agp_heaps_gg"></span><span id="DDK_MANAGING_AGP_HEAPS_GG"></span>


**このトピックでは、Windows NT ベースのオペレーティング システムにのみ適用されます。**

ドライバーは AGP を管理できる、DirectX のランタイムから受信した通知を使用するヒープ。 ドライバーとしてランタイムからに通知を受信する**GetDriverInfo2**次の値を使用する要求。

-   D3DGDI2\_型\_延期\_AGP\_AWARE

-   D3DGDI2\_型\_FREE\_延期\_AGP

-   D3DGDI2\_型\_DEFER\_AGP\_FREES

詳細については、 **GetDriverInfo2**要求を参照してください[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

ディスプレイ デバイスが作成されると、ディスプレイ ドライバーが受信、 **GetDriverInfo2** 、D3DGDI2 要求\_型\_延期\_AGP\_対応の通知をドライバー使用して決定をヒープ AGP を処理し、代わりに、D3DGDI2 を使用するその他のメカニズムを無効にする必要があるかどうか\_型\_FREE\_延期\_AGP と D3DGDI2\_型\_DEFER\_AGP\_FREES 通知後に、ランタイムを送信します。 D3DGDI2 で\_型\_延期\_AGP\_対応の通知へのポインターを提供する DirectX のランタイム、 [ **DD\_延期\_AGP\_認識\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_deferred_agp_aware_data)構造体、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)データ構造体。

ドライバーが受け取る場合があります、 **GetDriverInfo2** 、D3DGDI2 要求\_型\_DEFER\_AGP\_FREES 通知の表示モードの変更が発生する前にします。 DirectX のランタイムは、ランタイムは、表示モードの変更を実行している場合にのみこの通知を送信します。 ドライバーは、画面を作成するプロセスに対して画面を破棄するプロセスのプロセス id (PID) を確認する必要があります。 Pid が異なる場合、ドライバーを破棄しないように AGP メモリのユーザー モード マッピングのため、アプリケーションがメモリを使用しても可能性があります。

ドライバーが受信、 **GetDriverInfo2** 、D3DGDI2 で要求を\_型\_FREE\_延期\_AGP 通知とサーフェスを使用してプロセスの停止内のデバイスをすべて表示、テクスチャ、頂点バッファー、および表示モードの変更時にロックされたインデックス バッファー。 通知を安全に破壊されることがすべてのユーザー モード マッピング AGP メモリのドライバーに通知します。

D3DGDI2 で\_型\_DEFER\_AGP\_FREES と D3DGDI2\_型\_FREE\_延期\_AGP の通知へのポインターを提供する、ランタイム、[ **DD\_FREE\_延期\_AGP\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_free_deferred_agp_data)構造体、 **lpvData** DD のメンバー\_GETDRIVERINFODATA データ構造体。 **DwProcessId** DD のメンバー\_FREE\_延期\_AGP\_データ AGP メモリを破壊するプロセスの PID を指定します。

アプリケーションが、ランタイム、D3DGDI2 を送信することがなく終了できますに注意してください。\_型\_FREE\_延期\_ドライバーに AGP 通知。 そのため、ドライバーを解放すべてのユーザー モード マッピング AGP メモリへの呼び出しを受け取ったときにその[ **D3dDestroyDDLocal** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)関数。

 

 





