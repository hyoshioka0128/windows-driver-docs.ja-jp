---
title: ビデオ ポートベースのキャプチャ
description: ビデオ ポートベースのキャプチャ
ms.assetid: 84cc1ee3-142c-4dae-9f5c-0dde66cc3df9
keywords:
- フィルターグラフの構成 WDK ビデオキャプチャ、ビデオポートベースのキャプチャ
- ビデオポートベースのキャプチャ WDK ビデオキャプチャ
- ビデオポート pin WDK ビデオキャプチャ
- VPEs WDK ビデオキャプチャ
- ビデオポート拡張機能の WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0238f12ca6ba2441f5fcd1ea93603cee406a7289
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843665"
---
# <a name="video-port-based-capture"></a>ビデオ ポートベースのキャプチャ


ビデオポートに基づくキャプチャデバイスは、ビデオポートマネージャーに接続するためのビデオポート pin を提供する必要があります。 ビデオポート pin を使用すると、ハードウェアベースのトランスポートで、CPU または周辺機器インターコネクト (PCI) バスのオーバーヘッドなしでプレビューストリームを表示できます。 別の pin を使用すると、キャプチャ機能が提供されます (キャプチャしたビデオをディスクに書き込む場合など)。 キャプチャ処理中に、キャプチャバッファーがディスプレイドライバーに提供されます。これにより、バスマスタリングによってバッファーがいっぱいになります。 Capture ミニドライバーとディスプレイドライバーの間の相互作用については、このセクションの後の方で詳細に説明し、[カーネルモードのビデオトランスポート](https://docs.microsoft.com/windows-hardware/drivers/display/kernel-mode-video-transport)で説明します。

Microsoft Windows 98 SE または Windows 2000 を実行するシステムでは、オーバーレイミキサーフィルター (以降のオペレーティングシステムでのビデオポートマネージャーフィルターの一部) では、セカンダリモニターでのビデオポート接続はサポートされません。 この場合、pin 接続は失敗します。 セカンダリモニターでのビデオポート接続は、Windows Millennium Edition (Windows Me) および Windows XP を実行しているシステムでサポートされています。

デバイスで VBI capture がサポートされている場合、通常、VPVBI と VBI の2つの追加の pin が公開されます。 ビデオポートマネージャーのフィルターでは、VPVBI pin を使用して VBI capture のビデオポートサーフェイスを割り当てます。 VBI pin 自体には、未加工の VBI サンプルが用意されています。

次の図は、VPVBI と VBI capture の個別のパスを示しています。

![vpvbi と vbi capture の個別のパスを示す図](images/video-port-capture.gif)

この種類のフィルターグラフに固有のプロパティセットは、 [kspropsetid\_VPConfig および kspropsetid\_VPVBIConfig](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig)と[PROPSETID\_アロケーター\_コントロール](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)です。

### <a name="using-the-video-port-extensions-vpes"></a>ビデオポート拡張機能 (VPEs) の使用

**注:** 次の段落は、Windows Vista の次のバージョンより前のオペレーティングシステムにのみ適用されます。 Windows vista では、ディスプレイドライバーで新しい Windows Vista ドライバー表示モデル (LDDM) が使用されている場合、VPE は無効になっています。

Video capture ミニドライバーは、 [**Dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数を使用してビデオミニポートドライバーと通信することができます。キャプチャのストリーミングビデオをキャプチャハードウェアとディスプレイハードウェアの間でビデオポートバス間で転送できます。 このストリームは、NTSC、PAL、または SECAM ビデオのシーケンシャルフィールドで構成されており、ブランキング (VBI) とタイムコード (水平同期および垂直同期) データを含めることができます。 ビデオストリームの特性 (ディメンション、色の形式、頻度、拡大縮小、トリミングなど) は、ユーザーモードで、VPE DirectDraw インターフェイスを介して構成されます。 ストリーミングが開始された後、 **Dxapi**は、個々のフレームをキャプチャするためにカーネルモードで呼び出されます。 解像度の変更や全画面表示のコマンドプロンプトからの切り替えなど、表示の変更をサポートするには、ビデオキャプチャミニドライバーもビデオミニポートドライバーに登録して、そのような表示変更イベントに応答できるようにする必要があります。

VPEs と**Dxapi**関数は、DirectX 5.0 で DirectDraw DDI に導入されました。 **Dxapi**は、Windows 2000 以降のオペレーティングシステムのビデオミニポートドライバーでサポートされています。 仮想表示ミニポートドライバー (miniVDD) では、Windows 98 および Windows Me オペレーティングシステムで**Dxapi**がサポートされています。 **Dxapi**を使用してカーネルモードのビデオトランスポートを有効にするには、WDM ビデオキャプチャミニドライバーに*ddkmapi. h* (DirectDraw カーネルモード API) ヘッダーファイルをインクルードし、 *dxapi .lib*ライブラリとリンクする必要があります。 **Dxapi**ライブラリでは、 *dxapi .sys*によってエクスポートされた機能を使用します。 Dxapi は DirectDraw が読み込まれている場合にのみ使用でき*ます。* これは、 **DXAPI**が Directdraw DDI に対する vpes の一部であるためです。

**Dxapi**は、 *dxapi .sys*によって公開される単一のカーネルモード API です。 ビデオポート拡張は、 *DDraw*によって公開されるユーザーモード API です。 ビデオキャプチャミニドライバーは、ビデオポートハードウェアを正しくストリームするように設定および構成するために、 **Dxapi**に対して複数の異なる呼び出しを行う必要があります。

**Dxapi**は、複数の関数識別子をカプセル化する単一の関数です。 ミニドライバーは、最初の引数に必要な関数識別子を**Dxapi**に渡します。 **Dxapi**の残りの引数は、関数の識別子とバッファーの長さに対応する構造体のミニドライバーに割り当てられたバッファー用です。 関数の動作と、入力バッファーと出力バッファーのサイズと形式は、指定された関数識別子によって異なります。 この動作は、「 [Dxapi 関数と識別子](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」に記載されています。

WDK には、 **Dxapi**機能を実装する方法を示す2つのサンプルドライバーが用意されています。 このサンプルでは、動作するために特定のハードウェアが必要です。 TestCap サンプルはハードウェアを必要とせず、すべてのプラットフォームで動作します。 GraphEdt ツールを使用して、いずれかのサンプルと対話できます。

ビデオキャプチャミニドライバーが**Dxapi**を呼び出して実行する一般的な関数は、次のとおりです。

-   カーネルモード DirectDraw (**dxapi**関数識別子が DD\_dxapi\_opendirectdraw) へのハンドルを開きます。 この操作は、IRQL = パッシブ\_レベルで実行する必要があります。

-   ハードウェアビデオポートのカーネルモード機能を取得します (**dxapi**関数識別子は、DD\_dxapi\_GETKERNEL cap に設定されています)。

-   全画面表示のコマンドプロンプトにモードスイッチなどの DirectDraw イベントを処理するためのコールバックを登録します (**dxapi**関数識別子は、DD\_dxapi\_登録\_コールバック)。

-   DirectDraw サーフェスをターゲットとするハンドルを開きます (**dxapi**関数識別子は、DD\_dxapi\_opensurface に設定されています)。

-   コールバックの登録を解除します (**dxapi**関数識別子が DD\_dxapi\_登録解除\_コールバック)。

-   画面へのハンドル、およびカーネルモード DirectDraw (**dxapi**関数識別子が DD\_dxapi\_CLOSEHANDLE) に設定されることを閉じる

### <a name="video-port-child-devices-and-power-management"></a>ビデオポートの子デバイスと電源管理

ビデオポートの子デバイス (TV チューナーやディスプレイの組み合わせアダプターなど) では、ミニドライバーを使用しているときに電源状態の移行がブロックされる可能性があります。 電源状態の移行のブロックは、ミニドライバーがアクティブに使用されている (ピンまたはフィルターが開いている) ときに発生します。 ミニドライバーが読み込まれているにもかかわらず、pin やフィルターが使用されていない場合は、S0 (完全電源) から低電力状態 (S1、S2、S3、S4 など) への電源状態の移行が発生します。 電源状態の移行のブロックは、ビデオポートの子デバイスのクライアントである Stream クラスミニドライバーでのみ発生します。

この条件を満たすデバイスに対しては、WHQL の権利が提供されます。そのため、ベンダは引き続きロゴを取得できます。

 

 




