---
title: MPEG-4
description: MPEG-4
ms.assetid: 7879acd5-39fe-46b4-a427-43e4ea52315e
keywords:
- Mpeg-4 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f42c5e9c70bf3aefa754df3e43e31ee34421c9ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558740"
---
# <a name="mpeg-4"></a>MPEG-4


## <span id="ddk_mpeg_4_gg"></span><span id="DDK_MPEG_4_GG"></span>


Mpeg-4 が大きく H.263 プログレッシブ スキャンのコーディング、およびインター レースと 4 以外の色のサンプリングの形式をサポートするためには、mpeg-2 に基づいて: 2:0。 H.263 と mpeg-2 をサポートする機能は、mpeg-4 のサポートを使用できます。

Mpeg-4 は 8 ビットよりも多くのサンプルの精度をサポートできます。 DirectX VA にはピクセルを使用してあたり 8 ビット以上をサポートするためのメカニズムが含まれています、 **bBPPminus1**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体。

**注**   DirectX 問い合わせくださいで図形のコーディング、オブジェクト指向、顔のモデリング、メッシュ オブジェクト、およびのスプライトなど、mpeg-4 に最も固有の機能はサポートされていません。

 

 

 





