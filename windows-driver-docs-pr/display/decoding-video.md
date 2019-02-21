---
title: ビデオのデコード
description: ビデオのデコード
ms.assetid: d434469f-1279-47c4-b824-61daeb25b214
keywords:
- ビデオのビデオをデコードについての詳細の WDK DirectX va なのでのデコード
- ビデオのデコードについての詳細の va なので、ビデオの WDK DirectX のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 932408a24eabffcf021e5a969f8db14393543050
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559691"
---
# <a name="decoding-video"></a>ビデオのデコード


マイクロソフトの Direct3D ランタイムが呼び出すユーザー モードのディスプレイ ドライバーの[ **DecodeBeginFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff551802)と[ **DecodeEndFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff551805)関数ユーザー モードのディスプレイ ドライバーがビデオをデコードできるこれらの関数呼び出しまでの時間を示します。 ユーザー モードのディスプレイ ドライバーが任意のビデオを実行する前に、デコード操作、マイクロソフトの Direct3D ランタイムは、ユーザー モードのディスプレイ ドライバーを呼び出す必要があります[ **SetDecodeRenderTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff569530)を設定する関数、レンダー ターゲットのサーフェスにとっては、操作をデコードします。 ただし、呼び出し**SetDecodeRenderTarget**期間開始フレーム、終了フレーム以外にのみ発生することができます。

保護されたモードとへの呼び出しで[ **DecodeBeginFrame**](https://msdn.microsoft.com/library/windows/hardware/ff551802)、Direct3D のランタイムを設定または変数に DirectX VA コンテンツ キーを変更する、 **pPVPSetKey**のメンバー、[ **D3DDDIARG\_DECODEBEGINFRAME** ](https://msdn.microsoft.com/library/windows/hardware/ff542987)へのポインターを構造体します。 デコード デバイスは、この保護された転送の圧縮された DirectX VA バッファーのキーとそれ以降のフレームを使用します。

**注**   、Direct3D ランタイム セット、 **pPVPSetKey**ポインターのみを変更またはキーを設定します。 事前に設定して、キーを使用して、ランタイムにポインターを設定**NULL**同じキーの時間がかかる再読み込みを回避するためにします。 ドライバーでは、冗長な設定は削除しません。 デコーダーのアプリケーションでは、冗長な設定を避ける必要があります。

 

後のレンダー ターゲットのサーフェスをデコード操作の設定、ユーザー モードのディスプレイ ドライバーへの呼び出しを受信できる、 [ **DecodeExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551808)ビデオを実行する関数は、開始フレーム間での操作をデコードおよびフレームの終了時間帯。

呼び出しで[ **DecodeExecute**](https://msdn.microsoft.com/library/windows/hardware/ff551808)、バッファーの種類で指定されているかを満たさない、 **CompressedBufferType**のメンバー、 [ **DXVADDI\_DECODEBUFFERDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562896)の構造、 **pCompressedBuffers**の配列、 [ **D3DDDIARG\_DECODEEXECUTE** ](https://msdn.microsoft.com/library/windows/hardware/ff543001)構造が使用される GUID のデコードを**hDecode** D3DDDIARG のメンバー\_DECODEEXECUTE を指定します。 たとえば、スライスのコントロール (D3DDDIFMT\_SLICECONTROLDATA)、逆量子化 (D3DDDIFMT\_INVERSEQUANTIZATIONDATA)、およびビット ストリーム (D3DDDIFMT\_BITSTREAMDATA) バッファーにのみ必要可変長のデコード (VLD) の処理、および非ブロック化制御バッファー (D3DDDIFMT\_DEBLOCKINGDATA) はまったく使用 mpeg-2 していません。

保護モードでは、コンテンツ キーで保護された転送の暗号化されたバッファーは、初期のカウンター値のバッファー記述子にへのポインターを含めることが (つまりで変数を**pCipherCounter** のメンバー[**DXVADDI\_DECODEBUFFERDESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562896)構造体を指す) です。 呼び出しごとに、ユーザー モードのディスプレイ ドライバーの[ **DecodeExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff551808)関数は、このようなバッファーの前に、ローカルのビデオ メモリへの保護された転送を実行する必要があります**DecodeExecute**デコード操作では、バッファーのデータを使用します。 ただし、プランが存在しない残余違い以外の型の圧縮 DirectX VA バッファーを暗号化する (D3DDDIFMT\_RESIDUALDIFFERENCEDATA) とビット ストリーム (D3DDDIFMT\_BITSTREAMDATA) の種類。

 

 





