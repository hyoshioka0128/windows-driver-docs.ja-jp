---
title: AVStream コーデックのストライド処理
description: AVStream コーデックのストライド処理
ms.assetid: 816a0ddc-8ab8-4259-9842-76f5e4dadee0
keywords:
- AVStream ハードウェアコーデックサポート WDK、stride の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b483577a30e0d6cacb9e73af6fb6e74f508d194f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838777"
---
# <a name="handling-stride-in-avstream-codecs"></a>AVStream コーデックのストライド処理


デコーダーが拡張ビデオレンダラー (EVR) などのレンダラーや、Direct3D をサポートするコンポーネントに接続されている場合、ミニドライバーはシステムメモリバッファーではなく D3D バッファーを受信します。

レンダリングの前に D3D サーフェイスにコピーする必要があるシステムメモリバッファーとは異なり、D3D バッファーはレンダーエンジンによって直接表示できます。 そのため、システムメモリバッファーではなく D3D バッファーを使用することにより、ミニドライバーは各バッファーのコピー操作を保存します。

ミニドライバー対応のが D3D バッファーを受け取ると、D3D サーフェイスがロックされ、それを指すポインターが[**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)に配置されます。**データ**。 次のコード例に示すように、画面の stride 情報は、 [**KS\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) EXTENSION から ksk ストリーム\_ヘッダーに指定されています。

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

ミニドライバーは、 [**BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)構造体\_の**biwidth**メンバーをサーフェイスの幅として使用する必要があります。

([**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)。**Bmiheader**の型は、\_bitmapinfoheader です。 [**KS\_datarange ビデオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)を再生します。**Videoinfoheader**は、型 KS\_videoinfoheader) です。

KS\_FRAME\_INFO の場合。**lSurfacePitch**の値が0以外の場合、ミニドライバーは、関連する ksk ストリーム\_ヘッダーで指定されているバッファーの幅/ストライドとして**lSurfacePitch**を使用する必要があります。 それ以外の場合、出力イメージはゆがんで表示されます。

 

 




