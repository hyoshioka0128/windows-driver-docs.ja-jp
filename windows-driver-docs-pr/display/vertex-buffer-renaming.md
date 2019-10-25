---
title: 頂点バッファーの名前変更
description: 頂点バッファーの名前変更
ms.assetid: b76552b4-77a9-43f4-984b-10de92dffa83
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 ディスプレイ、頂点バッファー、名前の変更
- 頂点バッファー WDK DirectX 8.0、名前の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad782d8ff749aab5febcda547aab918cb5e4d24b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825304"
---
# <a name="vertex-buffer-renaming"></a>頂点バッファーの名前変更


## <span id="ddk_vertex_buffer_renaming_gg"></span><span id="DDK_VERTEX_BUFFER_RENAMING_GG"></span>


ドライバーとランタイムの間の並列処理を向上させるために、Direct3D は頂点バッファーの "名前の変更" の概念をサポートしています。 基本的に、これは頂点バッファーのダブルバッファリング方式です。 特定の状況では、DDI 呼び出しを使用して頂点バッファーを渡したときに、頂点バッファーのビデオメモリポインターを変更することができます。 このようにして、ドライバーは頂点バッファーの内容の処理を継続できますが、同時に、アプリケーションは頂点バッファーをロックして塗りつぶすことができます。 アプリケーションに関しては、同じ頂点バッファーを使用します。 この頂点バッファーが指すメモリが変更されているという事実は、ランタイムとドライバーによって隠されています。

以前のバージョンの DirectX では頂点バッファーの名前変更がサポートされていましたが、DirectX 8.0 では特定の変更が行われています。 以前のバージョンの Direct3D では、名前の変更は主に[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI エントリポイントを介して行われていました。 [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)で指定されたフラグは、ドライバーが頂点またはコマンドバッファーを交換できるかどうかを指定します。その場合は、バッファーの必要なサイズを指定します。 ただし、DirectX 8.0 では、 *D3dDrawPrimitives2*を使用した頂点バッファーのスワップは実行されません (ただし、レガシインターフェイスを介した呼び出しでも、このメカニズムを利用します) が、 *lockexecutebuffer* ([*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))) を使用することはできません。DDI エントリポイント。

DirectX 8.0 では、D3DLOCK\_DISCARD という新しいロックフラグが定義されています。このフラグは、ドライバーに渡されると、呼び出し元はドライバーの既存の内容を必要としないことを示します。そのため、頂点バッファーデータへのポインターを返す前に破棄することができます。 このため、D3DLOCK\_DISCARD フラグが設定された頂点バッファーロック呼び出しをドライバーが受け取ると、 **Fpvidmem**を新しい値に設定することにより、頂点バッファーの名前を変更することができます。

Windows 2000 の初期製品版リリースでは、D3DLOCK\_DISCARD フラグがドライバーに渡されないことに注意してください。 フラグは、Windows 2000 Service Pack 1 (SP1) 以降のすべてのバージョンの Windows 2000 で渡されます。

DirectX 7.0 では、フラグ DDLOCK\_DISCARDCONTENTS を使用して、 *Lockexecutebuffer*経由で頂点バッファーの名前を変更することもできます。 ただし、DirectX 7.0 の最初のリリースでのランタイムとドライバーの同期により、このメカニズムが正しく動作しなくなります。 ただし、directx 8.0 でリリースされた DirectX 7.0 のバージョンはこの問題を修正し、ロック時の頂点バッファーの名前変更は DirectX 7.0 インターフェイスを介して機能します。

 

 





