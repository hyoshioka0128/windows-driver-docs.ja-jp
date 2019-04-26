---
title: DXVA-HD DDI のプログラミングに関する考慮事項
description: DXVA-HD DDI のプログラミングに関する考慮事項
ms.assetid: 84576a8d-67e1-480a-9323-ef34b0900d22
keywords:
- DXVA HD DDI WDK Windows 7 の表示、プログラミングの考慮事項
- DXVA HD DDI WDK Server 2008 R2 の表示、プログラミングの考慮事項
- 高解像度ビデオ WDK Windows 7 の表示、DXVA HD DDI、プログラミングに関する考慮事項
- 高解像度ビデオ WDK Server 2008 R2 の表示、DXVA HD DDI、プログラミングに関する考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac77b4ef218b43c6902b698e3d7c952b79c62e8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359426"
---
# <a name="dxva-hd-ddi-programming-considerations"></a>DXVA-HD DDI のプログラミングに関する考慮事項


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

実装する場合、 [DXVA HD DDI](dxva-hd-ddi.md)ユーザー モードのディスプレイ ドライバーでは、次のプログラミングのヒントを検討してください。

-   ドライバーは、D3DCAPS3 を設定する必要があります\_DXVAHD (0x00000400L) ビット、 **Caps3**のメンバー [D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)を DXVA HD DDI をサポートし、それ以外の場合、Direct3D のランタイムが失敗したことを示すために構造体呼び出す、 [ **CreateVideoProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff540732) DXVA HD デバイスを作成する関数。 D3DCAPS9 構造体は、DirectX 9.0 SDK ドキュメントで説明します。 ドライバーの設定、D3DCAPS3\_DXVAHD ビットへの呼び出しに応答でその[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)関数を D3DDDICAPS\_GETD3D9CAPS 値で設定されます、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体、 *pData*パラメーターを指します。

-   DXVAHD\_画面\_型\_ビデオ\_入力\_アプリケーション レベル DXVAHD のプライベート値\_画面\_DDI の対応する値を持たない型の列挙体。 アプリケーション設定、DXVAHD\_画面\_型\_ビデオ\_入力\_CPU またはシェーダー ベースのビデオのさまざまな形式の種類に割り当てられるオフスクリーン プレーンなサーフェイスでの秘密の値プロセッサのプラグインです。

-   DXVAHD\_画面\_型\_ビデオ\_アプリケーション レベル DXVAHD の出力値\_画面\_種類の列挙型に対応する、 **VideoProcessRenderTarget**のフラグをビット フィールド、 [ **D3DDDI\_RESOURCEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544644)構造体。 Direct3D のランタイム セット**VideoProcessRenderTarget**で、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)ランタイムが呼び出す、ドライバーのときに[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)レンダー ターゲットのビデオの処理を作成する関数。

-   Direct3D のランタイムは、両方のビット ブロック転送 (bitblt) とストリームの状態を維持します。 ランタイムは、ランタイムが照会されたときに、アプリケーションに返します。

-   アプリケーション レベル**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**メソッドに対応する DDI 関数がありません。 ただし、アプリケーションを呼び出すと**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**ビデオ プロセッサの状態データをプライベート bitblt 関数を取得する Direct3D のランタイムは、ドライバーを呼び出して[ **GetVideoProcessBltStatePrivate** ](https://msdn.microsoft.com/library/windows/hardware/ff566812)関数。

-   アプリケーション レベル**IDXVAHD\_VideoProcessor::GetVideoProcessStreamState**メソッドに対応する DDI 関数がありません。 ただし、アプリケーションを呼び出すと**IDXVAHD\_VideoProcessor::GetVideoProcessBltState**ビデオ プロセッサの状態データをプライベートのストリームを取得する Direct3D のランタイムは、ドライバーを呼び出して[ **GetVideoProcessStreamStatePrivate** ](https://msdn.microsoft.com/library/windows/hardware/ff566815)関数。

-   DXVAHD\_ストリーム\_状態\_のアプリケーション レベル DXVAHD D3DFORMAT 値\_ストリーム\_の状態の列挙対応する DDI 値がない、 [ **DXVAHDDDI\_ストリーム\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff563068)列挙体。 プラグインのビデオのプロセッサの使用、DXVAHD\_ストリーム\_状態\_、DXVAHD 使用が割り当てられたサーフェスの D3DFORMAT 値\_画面\_型\_ビデオ\_入力\_秘密の値のアプリケーション レベル DXVAHD\_画面\_種類の列挙型。

-   DXVAHD\_デバイス\_種類の列挙型が対応する DDI 列挙型を持たない (ありません DXVAHDDDI など\_デバイス\_型)。 最初のメンバー、 [ **DXVAHDDDI\_VPDEVCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff563113)構造は予約されていますが、アプリケーション レベル DXVAHD の最初のメンバー\_VPDEVCAPS 構造体が、DXVAHD に設定されています。\_デバイス\_型の値で、 **DeviceType**メンバー。 **DeviceType**メンバーは、ランタイムまたは DXVAHD としてドライバーを常に報告するビデオ プロセッサ、プラグインによって設定されます\_デバイス\_型\_ハードウェア。

-   **乗数**のメンバー、 [ **DXVAHDDDI\_フィルター\_範囲\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff563055)構造体は浮動小数点値。 ドライバーには、基本の 2 つの分数として正確に表すことができる値を使用する必要があります。 たとえば、0.25 は基本の 2 つの分数として正確に表すことができますが、0.1 ことはできません。

-   すべて[DXVA HD DDI](dxva-hd-ddi.md)関数が返す必要があります S\_OK、E\_INVALIDARG または E\_OUTOFMEMORY します。

 

 





