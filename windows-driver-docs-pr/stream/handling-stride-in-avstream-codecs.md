---
title: AVStream コーデックのストライド処理
description: AVStream コーデックのストライド処理
ms.assetid: 816a0ddc-8ab8-4259-9842-76f5e4dadee0
keywords:
- AVStream ハードウェア コーデックは、WDK、stride の処理をサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d2e57ae0a23a8649dfb954374dd08f5f0ceafe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384017"
---
# <a name="handling-stride-in-avstream-codecs"></a>AVStream コーデックのストライド処理


デコーダーが強化されたビデオ レンダラー (EVR) または Direct3D をサポートするコンポーネントなどのレンダラーに接続されている場合、ミニドライバーは、システム メモリのバッファーではなく D3D バッファーを受け取ります。

レンダリングの前に D3D のサーフェスにコピーする必要があります、システム メモリのバッファーとは異なり、レンダリング エンジンによって直接 D3D バッファーを表示できます。 そのため、D3D バッファーを使用して、システム メモリのバッファーではなくで、ミニドライバー各バッファーのコピー操作が保存されます。

解明できるミニドライバーは、D3D バッファーを受け取り、D3D 画面がロックされているし、へのポインターにある[ **KSSTREAM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header).**データ**します。 指定されている surface stride 情報、 [ **KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info) KSSTREAM 拡張\_ヘッダー、次のコード例に示すように。

```cpp
typedef struct KS_FRAME_INFO {
    ULONG                   ExtendedHeaderSize; // Size of this extended header
    DWORD                   dwFrameFlags;       // Field1, Field2, or Frame
    LONGLONG                PictureNumber;
    LONGLONG                DropCount;

    // The following are only set when you use OverlayMixer
    HANDLE                  hDirectDraw;        // user mode DDraw handle
    HANDLE                  hSurfaceHandle;     // user mode surface handle
    RECT                    DirectDrawRect;     // portion of surface locked
    union {
  LONG               lSurfacePitch;  // Contains surface pitch a.k.a stride
         DWORD              Reserved1;
    };
    // Reserved fields, never reference these
    DWORD                   Reserved2;
    DWORD                   Reserved3;
    DWORD                   Reserved4;
} KS_FRAME_INFO, *PKS_FRAME_INFO;
```

ミニドライバーを使用する必要があります、 **biWidth**のメンバー、 [ **KS\_BITMAPINFOHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)表面幅として構造体。

([**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_videoinfoheader).**bmiHeader**型 KS\_BITMAPINFOHEADER します。 [**KS\_DATARANGE\_ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video).**VideoInfoHeader**型 KS\_VIDEOINFOHEADER)。

場合 KS\_フレーム\_情報 **。lSurfacePitch** 0 以外の値を持つ、ミニドライバーを使用する必要があります**lSurfacePitch**関連 KSSTREAM で指定されているバッファーの幅/stride として\_ヘッダー。 それ以外の場合、出力の画像は、文字が正しく表示されます。

 

 




