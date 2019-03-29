---
title: ディスプレイ ドライバーの同期に関する問題
description: ディスプレイ ドライバーの同期に関する問題
ms.assetid: 7d87e963-02c3-4da2-9dbd-ca14bde2867b
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、同期
- 同期の WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f6585c9318b199a947e240d8d8b585b1d0ff78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580011"
---
# <a name="synchronization-issues-for-display-drivers"></a>ディスプレイ ドライバーの同期に関する問題


Microsoft では、ロックを保持しているときに、すべての GDI 関数を呼び出さないことをディスプレイ ドライバーでお勧めします。 ディスプレイ ドライバーを呼び出さないこと、次の関数のいずれか、ミュー テックスを保持しているときに特に重要です。 これは、デッドロックにつながります。

-   BRUSHOBJ\_hGetColorTransform

-   BRUSHOBJ\_pvAllocRbrush

-   BRUSHOBJ\_pvGetRbrush

-   BRUSHOBJ\_ulGetBrushColor

-   CLIPOBJ\_bEnum

-   CLIPOBJ\_cEnumStart

-   CLIPOBJ\_ppoGetPath

-   EngAcquireSemaphore

-   EngAllocMem

-   EngAllocPrivateUserMem

-   EngAllocUserMem

-   EngAlphaBlend

-   EngAssociateSurface

-   EngBitBlt

-   EngCheckAbort

-   EngComputeGlyphSet

-   EngControlSprites

-   EngCopyBits

-   EngCreateBitmap

-   EngCreateClip

-   EngCreateDeviceBitmap

-   EngCreateDeviceSurface

-   EngCreateDriverObj

-   EngCreateEvent

-   EngCreatePalette

-   EngCreatePath

-   EngCreateSemaphore

-   EngCreateWnd

-   EngDeleteClip

-   EngDeleteDriverObj

-   EngDeleteEvent

-   EngDeletePalette

-   EngDeletePath

-   EngDeleteSafeSemaphore

-   EngDeleteSemaphore

-   EngDeleteSurface

-   EngDeleteWnd

-   EngDxIoctl

-   EngEraseSurface

-   EngFillPath

-   EngFntCacheAlloc

-   EngFntCacheFault

-   EngFntCacheLookUp

-   EngFreeMem

-   EngFreeModule

-   EngFreePrivateUserMem

-   EngFreeUserMem

-   EngGetType1FontList

-   EngGradientFill

-   EngHangNotification

-   EngInitializeSafeSemaphore

-   EngLineTo

-   EngLoadImage

-   EngLoadModule

-   EngLoadModuleForWrite

-   EngLockDirectDrawSurface

-   EngLockDriverObj

-   EngLockSurface

-   EngMapEvent

-   EngMapFile

-   EngMapFontFileFD

-   EngMarkBandingSurface

-   EngModifySurface

-   EngMovePointer

-   EngNineGrid

-   EngPaint

-   EngPlgBlt

-   EngQueryPalette

-   EngReleaseSemaphore

-   EngSetPointerShape

-   EngStretchBlt

-   EngStretchBltROP

-   EngStrokeAndFillPath

-   EngStrokePath

-   EngTextOut

-   EngTransparentBlt

-   EngUnloadImage

-   EngUnlockDirectDrawSurface

-   EngUnlockDriverObj

-   EngUnlockSurface

-   EngUnmapEvent

-   EngUnmapFile

-   EngUnmapFontFile

-   EngUnmapFontFileFD

-   EngWaitForSingleObject

-   FONTOBJ\_cGetAllGlyphHandles

-   FONTOBJ\_cGetGlyphs

-   FONTOBJ\_pifi

-   FONTOBJ\_pjOpenTypeTablePointer

-   FONTOBJ\_pQueryGlyphAttrs

-   FONTOBJ\_pvTrueTypeFontFile

-   FONTOBJ\_pxoGetXform

-   FONTOBJ\_vGetInfo

-   HeapVidMemAllocAligned

-   PALOBJ\_cGetColors

-   PATHOBJ\_bEnumClipLines

-   PATHOBJ\_bMoveTo

-   PATHOBJ\_bPolyBezierTo

-   PATHOBJ\_vEnumStartClipLines

-   PATHOBJ\_vGetBounds

-   STROBJ\_bEnum

-   VidMemFree

-   WNDOBJ\_bEnum

-   WNDOBJ\_cEnumStart

-   WNDOBJ\_vSetConsumer

-   XFORMOBJ\_bApplyXform

-   XFORMOBJ\_iGetFloatObjXform

-   XFORMOBJ\_iGetXform

-   XLATEOBJ\_cGetPalette

-   XLATEOBJ\_hGetColorTransform

-   XLATEOBJ\_iXlate

-   XLATEOBJ\_piVector

 

 





