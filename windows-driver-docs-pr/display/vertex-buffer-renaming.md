---
title: 頂点バッファーの名前を変更
description: 頂点バッファーの名前を変更
ms.assetid: b76552b4-77a9-43f4-984b-10de92dffa83
keywords:
- DirectX 8.0 WDK Windows 2000 のリリース ノートを表示する頂点バッファー、名前を変更します。
- 頂点バッファー WDK DirectX 8.0 では、名前を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91f6fb5d31b605cc10978b245934858df9e61ed3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539664"
---
# <a name="vertex-buffer-renaming"></a>頂点バッファーの名前を変更


## <span id="ddk_vertex_buffer_renaming_gg"></span><span id="DDK_VERTEX_BUFFER_RENAMING_GG"></span>


ドライバーと、ランタイムの並列処理を向上させるのには、Direct3D には、頂点バッファー「の名前を変更」の概念がサポートしています。 基本的には、これは、頂点バッファーのダブル バッファリング スキームです。 ドライバーは、頂点バッファー DDI 呼び出しを通じて渡されるときに特定の状況では、頂点バッファーのビデオ メモリのポインターを変更します。 この方法で、ドライバーは、アプリケーションをロックし、頂点バッファーを入力すると同時に、中に、頂点バッファーの内容を処理する続行できます。 アプリケーションがに関する限り、同じ頂点バッファーを使用しています。 その頂点バッファーを指すメモリが変更されているという事実は、ランタイムとドライバーによって隠されています。

DirectX の以前のバージョンがサポートされています、頂点バッファーがある名前変更と、DirectX 8.0 と特定の変更がされています。 Direct3D の以前のバージョンでを主に使用して実現された名前の変更、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI エントリ ポイント。 指定されたフラグ[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)そうである場合と、ドライバーは、頂点またはコマンド バッファーをスワップだったかどうか指定は、必要なサイズのバッファー。 ただし、DirectX の 8.0 で頂点バッファーをスワップできませんによって実現されます*D3dDrawPrimitives2* (ただし、レガシー インターフェイス経由の呼び出しは、このメカニズムをまだ exploit) からのものではなく、 *LockExecuteBuffer* ([*LockD3DBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff568216)) DDI エントリ ポイント。

DirectX 8.0 は、新しいロック フラグ、D3DLOCK を定義します。\_、破棄するには、ドライバーに渡される、呼び出し元では、ドライバーの既存の内容は必要ありませんし、破棄する頂点バッファーのデータへのポインターを返す前にそのことを示します。 そのため、ドライバーが、D3DLOCK、頂点バッファーのロックの呼び出しを受信すると\_破棄フラグ設定、頂点バッファーを設定して名前を変更する選択できます、 **fpVidMem**に新しい値。

なお、D3DLOCK\_によって Windows 2000 の初期の製品版リリースに、破棄フラグがドライバーに渡されません。 Windows 2000 Service Pack 1 (SP1) および Windows 2000 のすべての後続バージョンにフラグが渡されます。

DirectX 7.0 では、頂点バッファーの名前を変更することもできますを使用して*LockExecuteBuffer* DDLOCK フラグを使用して\_DISCARDCONTENTS します。 ただし、ランタイムと DirectX 7.0 の元のリリースでのドライバーの間の同期は、このメカニズムが正しく動作を防止します。 ただし、この問題と頂点バッファーの修正リリース DirectX 8.0 で DirectX 7.0 のバージョン 7.0 の DirectX インターフェイスを通じて機能はロック時に名前を変更します。

 

 





