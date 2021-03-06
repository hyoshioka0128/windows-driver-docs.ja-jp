---
title: ビデオ ポートベースのキャプチャ
description: ビデオ ポートベースのキャプチャ
ms.assetid: 84cc1ee3-142c-4dae-9f5c-0dde66cc3df9
keywords:
- グラフ構成 WDK ビデオ キャプチャには、ポート ベースのビデオのキャプチャをフィルター処理します。
- ビデオ ポートに基づくキャプチャ WDK ビデオ キャプチャ
- ビデオ ポート ピン WDK のビデオのキャプチャ
- VPEs WDK ビデオ キャプチャ
- 拡張機能のビデオ ポート WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 839f5f95264526de19bdf4e593d417a066af3dea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385376"
---
# <a name="video-port-based-capture"></a>ビデオ ポートベースのキャプチャ


ビデオ ポートに基づいてキャプチャ デバイスには、ビデオ ポート マネージャーに接続するビデオ ポート pin を提供する必要があります。 ビデオ ポートの暗証番号 (pin) は、CPU や周辺機器のコンポーネントの相互接続 (PCI) バスのオーバーヘッドなし、プレビュー ストリームを表示する、ハードウェア ベースのトランスポートを使用できます。 別々 の pin がキャプチャ機能を提供します (たとえば、ときにキャプチャされたビデオ書き込む必要があるディスクに)。 キャプチャ中に、キャプチャ バッファーは、ディスプレイ ドライバー、バス マスターによってバッファーに設定するに提供されます。 このセクションで後で、さらに詳細にキャプチャ ミニドライバーとディスプレイ ドライバー間のやり取りが説明されている[カーネル モードのビデオ トランスポート](https://docs.microsoft.com/windows-hardware/drivers/display/kernel-mode-video-transport)します。

Microsoft Windows 98 SE または Windows 2000 を実行するシステムで、オーバーレイ Mixer フィルター (以降のオペレーティング システムでのビデオ ポート マネージャー フィルターの一部) は、セカンダリのモニターでビデオ ポートの接続をサポートしません。 この場合、暗証番号 (pin) の接続は失敗します。 セカンダリのモニターでビデオ ポート接続は、Windows Millennium Edition (Windows Me) および Windows XP を実行するシステムでサポートされます。

デバイスは、VBI キャプチャをサポートする場合は通常 2 つの追加の pin を公開します。VPVBI VBI. ビデオ ポート manager フィルターでは、VPVBI 暗証番号 (pin) を使用して、VBI キャプチャ ビデオ ポート画面を割り当てます。 自体 VBI の暗証番号 (pin) は、生の VBI サンプルを提供します。

次の図は、VPVBI と VBI キャプチャの別々 のパスを示します。

![vpvbi と vbi キャプチャの別々 のパスを示す図](images/video-port-capture.gif)

この種類のフィルターのグラフに固有のプロパティ セットは[KSPROPSETID\_VPConfig と KSPROPSETID\_VPVBIConfig](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig)と[PROPSETID\_アロケーター\_コントロール](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-allocator-control)します。

### <a name="using-the-video-port-extensions-vpes"></a>ビデオ ポート拡張 (VPEs) を使用します。

**注:** 次の段落の前に次のバージョンの Windows Vista オペレーティング システムにのみ適用されます。 ディスプレイ ドライバーが、新しい Windows Vista ドライバー表示 Model (LDDM) を使用している場合、Windows Vista で VPE が無効です。

ビデオ キャプチャ ミニドライバーが使用できる、 [ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)キャプチャをキャプチャ間のビデオ ポート バス間で転送するビデオのストリーミング ビデオのミニポート ドライバーとの通信に関数ハードウェアとディスプレイ ハードウェア。 ストリームは、NTSC、PAL、SECAM、ビデオの連続したフィールドで構成され、帰線消去 (VBI) とタイムコード (水平方向の同期と垂直方向の同期) のデータを含めることができます。 ビデオ ストリーム特性を含むディメンション、色の書式、頻度、スケーリング、および、トリミングが VPE DirectDraw インターフェイスからユーザー モードで構成されます。 ストリーミングが開始した後**DxApi**が個々 のフレームをキャプチャするカーネル モードで呼び出されます。 解像度または全画面表示のコマンド プロンプトとの間の切り替えの変更など、表示の変更をサポートするためには、ビデオのキャプチャがこのような表示に対応するため、ミニドライバーはビデオのミニポート ドライバーを使用した登録もする必要がありますは、イベントを変更します。

VPEs と**DxApi** DirectDraw DDI DirectX 5.0 に導入された関数。 **DxApi** Windows 2000 以降のオペレーティング システムでビデオのミニポート ドライバーでサポートされています。 仮想表示ミニポート ドライバー (miniVDD) サポート**DxApi** Windows 98 と Windows Me オペレーティング システム。 使用して有効にするカーネル モードのビデオ トランスポート**DxApi**、WDM ビデオ キャプチャのミニドライバーを含める必要があります、 *ddkmapi.h* (DirectDraw カーネル モードの API) のヘッダー ファイルとリンク、 *dxapi.lib*ライブラリ。 **DxApi**ライブラリによってエクスポートされた機能を使用して*dxapi.sys*します。 *DxApi.sys*のみ DirectDraw が読み込まれるときにためには**DxApi** DirectDraw DDI に VPEs の一部です。

**DxApi**によって公開される 1 つのカーネル モード API は、 *DxApi.sys*します。 ビデオ ポート拡張機能は、ユーザー モード API によって公開される*DDraw.dll*します。 ビデオ キャプチャ ミニドライバーをいくつかの別の呼び出しを行う必要があります**DxApi**セットアップを正しくストリームするビデオ ポート ハードウェアを構成します。

**DxApi**は 1 つの関数を複数の関数の識別子をカプセル化します。 ミニドライバーは、最初の引数に必要な関数の識別子を渡す**DxApi**します。 残りの引数**DxApi**は、関数識別子およびバッファーの長さに対応する構造体のミニドライバーに割り当てられたバッファー。 関数は、入力と出力バッファーの形式とサイズの動作は、指定された関数の識別子に依存します。 この動作が記載されて[DxApi 関数と識別子](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

WDK を実装する方法を示す 2 つのサンプル ドライバーを提供する、 **DxApi**機能します。 ATIWDM サンプルには、動作に存在する特定のハードウェアが必要です。 TestCap サンプルは、ハードウェアとすべてのプラットフォームの動作には必要ありません。 GraphEdt ツールを使用して、いずれかのサンプルと対話することができます。

ビデオ キャプチャ ミニドライバーを呼び出す必要のある共通の関数**DxApi**実行を次に示します。

-   カーネル モード DirectDraw を識別するハンドルを開く (**DxApi** DD に設定する識別子を関数\_DXAPI\_OPENDIRECTDRAW)。 IRQL でこの操作を実行する必要があります = パッシブ\_レベル。

-   ハードウェアのビデオ ポートのカーネル モードの機能を取得 (**DxApi** DD に設定する識別子を関数\_DXAPI\_GETKERNELCAPS)。

-   全画面表示のコマンド プロンプトにモードの切り替えなど、DirectDraw イベントを処理するコールバックを登録 (**DxApi** DD に設定する識別子を関数\_DXAPI\_登録\_コールバック)。

-   ターゲット DirectDraw サーフェスを識別するハンドルを開く (**DxApi** DD に設定する識別子を関数\_DXAPI\_OPENSURFACE)。

-   コールバックの登録を解除 (**DxApi** DD に設定する識別子を関数\_DXAPI\_登録解除\_コールバック)。

-   カーネル モード DirectDraw に関してもサーフェスへのハンドルを閉じる (**DxApi** DD に設定する識別子を関数\_DXAPI\_CLOSEHANDLE)

### <a name="video-port-child-devices-and-power-management"></a>ビデオ ポート子デバイスと電源管理

TV チューナーとの組み合わせのディスプレイ アダプターなどのビデオ ポート子デバイスは、使用されて、ミニドライバーと電源の状態遷移をブロックできます。 ミニドライバーの使用をアクティブにしたときに発生する電源状態の遷移ブロック (ピンまたはフィルターが開きます)。 ミニドライバーが読み込まれるがない場合の pin またはフィルター使用中、低電力の状態 (たとえば、S1、S2、S3 の場合、および S4) を (完全に利用) S0 から電源の状態遷移が発生します。 電源状態の遷移ブロック ビデオ ポート子デバイスのクライアントである Stream クラス ミニドライバーでのみ発生します。

WHQL 放棄はベンダーがロゴを引き続き取得できるように、この条件に合うデバイスを使用できます。

 

 




