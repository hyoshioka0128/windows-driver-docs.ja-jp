---
title: ビデオ キャプチャおよびその他の子デバイスのサポート
description: ビデオ キャプチャおよびその他の子デバイスのサポート
ms.assetid: 15575700-7525-459e-a099-158f0c13899c
keywords:
- ビデオキャプチャの WDK ディスプレイ
- キャプチャビデオの WDK ディスプレイ
- インターフェイス WDK 表示
- 子ビデオキャプチャドライバーの WDK ディスプレイ
- MDLs WDK 表示
- メモリ記述子の一覧 WDK 表示
- キャプチャバッファーの WDK 表示
- ディスプレイドライバーモデル WDK Windows Vista、子ビデオキャプチャドライバー
- Windows Vista display driver model WDK、子ビデオキャプチャドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1eefa7fffe1692cdbb2a731e79dd85205a498ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825558"
---
# <a name="supporting-video-capture-and-other-child-devices"></a>ビデオ キャプチャおよびその他の子デバイスのサポート


ビデオキャプチャデバイスまたは別の子デバイスの表示ミニポートドライバーとドライバーでは、子ドライバーが親ミニポートドライバーを介してそのデバイスと通信するために使用できるプライベートインターフェイスを相互に定義できます。 子ビデオキャプチャドライバーは、親ディスプレイミニポートドライバーに密に結合されている必要があります。 実際、ビデオキャプチャは、ディスプレイミニポートドライバーの一部として実装される可能性があります。 ビデオキャプチャドライバーは、ディスプレイミニポートドライバーと共にプライベートインターフェイスを使用して、 *I2C*バスにアクセスしたり、その他の目的に使用したりできます。

プライベートインターフェイスを初期化するために、ビデオキャプチャドライバーは、ディスプレイミニポートドライバーのディスプレイポートドライバー ( *Dxgkrnl*の一部) に[ **\_インターフェイス要求\_の IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)を送信します。 表示ポートドライバーは、このような要求を受信すると、ミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出し、プライベートインターフェイスを初期化するための情報を含む[**クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)構造体にポインターを渡します。

ビデオキャプチャがディスプレイミニポートドライバーの一部として実装されている場合、ビデオキャプチャは*DxgkDdiQueryInterface*を直接**呼び出すことが**あります。  

 

子デバイス (ビデオキャプチャデバイスを含む) の各ドライバーは、デバイスが関連付けられているハードウェアを示すアダプターの GUID を返す必要があります。 アダプター GUID は、アダプターの初期化時に送信される[**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数の*DxgkStartInfo*パラメーターによってポイントされる、 [**DXGK\_START\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_start_info)構造体の**adapterguid**メンバーのディスプレイミニポートドライバーに提供されます。 ユーザーモードのキャプチャコンポーネントは、後でこのアダプターの GUID をディスプレイアダプターにマップできます。

Microsoft Windows 2000 Display Driver モデル構造では、MDLs がビデオキャプチャドライバーに送信されます。 Windows Vista display driver model は、システムメモリへのキャプチャをサポートするだけでなく、ビデオメモリへのキャプチャをサポートしています。 Direct3D ランタイムは、DirectX Video 加速度 2.0-type 関数を呼び出して、キャプチャデータに対して後処理を実行するように GPU に指示します。 ビデオメモリバッファーを記述するために MDLs を送信する代わりに、ユーザーモードの表示ドライバーは、バッファー割り当てをキャプチャするハンドルである D3DKMT\_ハンドル型の値を送信します。 このため、ビデオキャプチャドライバーとディスプレイミニポートドライバーの組み合わせでは、 [**DxgkCbGetHandleData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata)などの既存のコールバック関数を使用して、キャプチャバッファーを記述するプライベートデータを参照できます。 ドライバーの組み合わせでは、 [**DxgkCbGetCaptureAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_getcaptureaddress) callback 関数を使用してキャプチャバッファーの物理アドレスを返すこともできます。

ビデオキャプチャアプリケーションは、Direct3D ランタイムを呼び出してキャプチャバッファーを作成します。その後、ランタイムはユーザーモードの表示ドライバーを呼び出します。 ランタイムは、 [**D3DDDIARG\_createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Flags**メンバーに設定された**CaptureBuffer**ビットフィールドフラグを使用して、ユーザーモードの display ドライバーの[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を呼び出し、キャプチャバッファーを作成します。 また、メモリマネージャーがディスプレイミニポートドライバーの[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)関数を呼び出してキャプチャバッファーの割り当てを作成するときに、ビデオメモリマネージャーの**キャプチャ**ビットフィールドフラグも指定する必要があります。 キャプチャバッファーが作成されると、それらはすぐにメモリに固定され、解放されるまで固定解除されません。 キャプチャスタックはキャプチャバッファーのカーネルモード割り当てハンドルをキャプチャドライバーに送信する必要があるため、ランタイムはユーザーモードの表示ドライバーの[**GetCaptureAllocationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaptureallocationhandle)関数を呼び出して、各リソースハンドルをそのリソースのカーネルモード割り当てハンドルにマップします。

キャプチャドライバーは、システムメモリへのキャプチャを直接サポートしているかどうかを報告できます。 キャプチャドライバーがシステムメモリへの直接キャプチャをサポートしている場合は、この目的のために MDLs がキャプチャドライバーに送信されます。 キャプチャドライバーがシステムメモリへの直接キャプチャをサポートしていない場合、ランタイムはビデオメモリキャプチャバッファーを作成し、キャプチャドライバーはそれらを格納する必要があります。 ユーザーモードの表示ドライバーの[**CaptureToSysMem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_capturetosysmem)関数を呼び出して、キャプチャバッファーの内容をシステムのメモリ領域にコピーします。 ランタイムは、 [**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)関数ではなく*CaptureToSysMem*を使用して、ビットブロック転送 (bitblt) 用の特殊なハードウェアを利用できます。これにより、ユーザーモードの Display ドライバーが[**pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)関数を呼び出す必要がありません。

AVStream はビデオキャプチャを制御するので、ビデオキャプチャが発生するタイミングを DirectX グラフィックスカーネルサブシステムが認識していません。 ただし、グラフィックスカーネルサブシステムは、キャプチャバッファーとして使用される割り当てを認識しています。 キャプチャバッファーを破棄しようとすると、グラフィックスカーネルサブシステムは、ディスプレイミニポートドライバーの[**DxgkDdiStopCapture**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_stopcapture)関数を呼び出して、キャプチャ操作がキャプチャバッファーとしての割り当ての使用をすぐに停止する必要があることを示します。 キャプチャ操作がキャプチャスタックを介して既に停止している場合、ドライバーはその呼び出しを無視しても安全です。

 

 





