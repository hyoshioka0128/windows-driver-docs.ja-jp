---
title: ビデオ キャプチャおよびその他の子デバイスのサポート
description: ビデオ キャプチャおよびその他の子デバイスのサポート
ms.assetid: 15575700-7525-459e-a099-158f0c13899c
keywords:
- ビデオ キャプチャ WDK の表示
- WDK のビデオ ディスプレイのキャプチャ
- インターフェイスの WDK の表示
- 子ビデオ キャプチャ ドライバー WDK を表示します。
- MDLs WDK の表示
- メモリの記述子には、WDK の表示が一覧表示されます。
- キャプチャ WDK 表示バッファー
- ドライバー モデル WDK Windows Vista では、子のビデオ キャプチャ ドライバーの表示します。
- Windows Vista のディスプレイ ドライバー モデル WDK、子のビデオ キャプチャ ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a43286d0ba1afe731a2abd58a4271ec60671450
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350064"
---
# <a name="supporting-video-capture-and-other-child-devices"></a>ビデオ キャプチャおよびその他の子デバイスのサポート


ディスプレイのミニポート ドライバーとのビデオ キャプチャ デバイスまたは別の子デバイス ドライバーでは、子ドライバーは、親のミニポート ドライバーを介してそのデバイスとの通信に使用できるプライベート インターフェイスを相互に定義できます。 子のビデオ キャプチャ ドライバーは、親の表示のミニポート ドライバーに密に結合する必要があります。 実際には、ビデオ キャプチャは、場合によって、ディスプレイのミニポート ドライバーの一部として実装できます。 ビデオ キャプチャ ドライバーにアクセスする、ディスプレイのミニポート ドライバーでプライベート インターフェイスを使用することができます、 *I2C*バスと他の目的です。

ビデオ キャプチャ ドライバーの送信、プライベート インターフェイスを初期化するために、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)ディスプレイ ポート ドライバー (の一部への要求*Dxgkrnl.sys*) 表示のミニポート ドライバーにします。 ミニポート ドライバーのポートのディスプレイ ドライバーは、このような要求を受信した後に呼び出す[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)関数し、へのポインターを渡す、 [**クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff569225)プライベート インターフェイスを初期化するために情報を含む構造体。

**注**  ビデオ キャプチャは、ディスプレイのミニポート ドライバーの一部として実装されている場合、ビデオのキャプチャが呼び出すことができます*DxgkDdiQueryInterface*直接します。

 

子デバイス (ビデオ キャプチャ デバイスを含む) の各ドライバーでは、アダプターのデバイスに関連付けられているハードウェアを示す GUID を返す必要があります。 ディスプレイのミニポート ドライバーに GUID が指定されたアダプター、 **AdapterGuid**のメンバー、 [ **DXGK\_開始\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562055)構造体指す、 *DxgkStartInfo*のパラメーター、 [ **DxgkDdiStartDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560775)アダプターが初期化されるときに送信される関数。 ユーザー モード キャプチャ コンポーネントは、ディスプレイ アダプターにこのアダプターの GUID を後でマップできます。

Microsoft Windows 2000 Display Driver Model の構造および送信のビデオに MDLs ドライバーをキャプチャします。 システム メモリへのキャプチャをサポートしているだけでなく、Windows Vista のディスプレイ ドライバー モデルは、ビデオ メモリをキャプチャをサポートします。 Direct3D ランタイムでは、キャプチャ データの後処理を実行する GPU に出力するための DirectX ビデオ アクセラレータ 2.0 型の関数を呼び出します。 ビデオ メモリ バッファーを記述する MDLs を送信する代わりに、ユーザー モードのディスプレイ ドライバーが D3DKMT を送信\_バッファーの割り当てをキャプチャするハンドルをハンドル型の値。 ビデオ キャプチャ ドライバーと表示のミニポート ドライバーの組み合わせがなどの既存のコールバック関数を使用するため、 [ **DxgkCbGetHandleData** ](https://msdn.microsoft.com/library/windows/hardware/ff559515)キャプチャを説明するプライベート データを参照するにはバッファー。 ドライバーの組み合わせを使用することも、 [ **DxgkCbGetCaptureAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff559510)キャプチャ バッファーの物理アドレスを返すコールバック関数。

ビデオ キャプチャ アプリケーション キャプチャ バッファーを作成する Direct3D の実行時に呼び出すランタイムは、その後、ユーザー モードのディスプレイ ドライバーを呼び出します。 共通言語ランタイムは、ユーザー モードのディスプレイ ドライバーの[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数と、 **CaptureBuffer**フラグのビット フィールドを設定、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)キャプチャ バッファーを作成する構造体。 ディスプレイのミニポート ドライバーを指定する必要がありますも、**キャプチャ**メモリ マネージャーは、ディスプレイ ミニポート ドライバーを呼び出すときに、ビデオ メモリ マネージャーのフラグをビット フィールド[ **DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)キャプチャ バッファーの割り当てを作成する関数。 キャプチャ バッファーを作成するがすぐにピン留めされているメモリ内と、リリースされるまではピンを外したはないです。 共通言語ランタイムは、ユーザー モードのディスプレイ ドライバーのキャプチャのスタックは、キャプチャ ドライバーに、キャプチャ バッファーのカーネル モードの割り当てのハンドルを送信する必要があります、ため[ **GetCaptureAllocationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff566771)各リソース ハンドルをそのリソースのカーネル モード割り当てハンドルにマップする関数。

キャプチャ ドライバーでは、システム メモリへの直接キャプチャをサポートするかどうかを報告できます。 キャプチャ ドライバーでは、システム メモリに直接キャプチャをサポートする場合、MDLs がこの目的のため、キャプチャ ドライバーに送信されます。 キャプチャ ドライバーがシステム メモリへの直接のキャプチャをサポートしていない場合は、ランタイムは、キャプチャ バッファー ビデオ メモリを作成し、キャプチャ ドライバーが入力する必要があります。 ユーザー モードのディスプレイ ドライバーの[ **CaptureToSysMem** ](https://msdn.microsoft.com/library/windows/hardware/ff539363)をシステム メモリの画面キャプチャ バッファーの内容をコピーする関数が呼び出されます。 ランタイムを使用できます*CaptureToSysMem*なく[ **Blt** ](https://msdn.microsoft.com/library/windows/hardware/ff538251)活用するために特殊なハードウェア ビット ブロック転送 (bitblt) を必要としない関数ユーザー モード ドライバーの呼び出しを表示する、 [ **pfnRenderCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568923)関数。

AVStream ビデオ キャプチャを制御するため、DirectX グラフィックスのカーネル サブシステムはビデオ キャプチャが発生したときの対応ではありません。 ただし、グラフィックス カーネル サブシステムは、キャプチャ バッファーとして使用される割り当てに注意してください。 グラフィックスのカーネルのサブシステムがディスプレイ ミニポート ドライバーを呼び出してキャプチャ バッファーは破棄されますが、 [ **DxgkDdiStopCapture** ](https://msdn.microsoft.com/library/windows/hardware/ff560776)キャプチャ操作が必要かを示す関数割り当てを使用して、キャプチャ バッファーとしてすぐに停止します。 キャプチャ操作は、キャプチャのスタックを既に停止されていますが場合、ドライバーでは、呼び出しを無視してかまいません。

 

 





