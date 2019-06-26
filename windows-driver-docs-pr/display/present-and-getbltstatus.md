---
title: 現状と GetBltStatus
description: 現状と GetBltStatus
ms.assetid: 76fd88df-18a9-4f00-834d-6683788fc2f6
keywords:
- Windows 2000 の WDK の表示、プレゼンテーションの DirectX 8.0 リリース ノートします。
- WDK DirectX 8.0 のプレゼンテーション
- レンダリング結果表示の WDK DirectX 8.0
- 表示される結果 WDK DirectX 8.0
- DdGetBltStatus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14aa4edffd07f8a48f0da46e08aaf603c4eeeb12
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371367"
---
# <a name="present-and-getbltstatus"></a>現状と GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


ランタイム DX8 を呼び出して不要になった[ *DdGetBltStatus* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus) blt システム メモリのサーフェスに関連するのです。 これは、Windows 2000 の動作では常にです。 結果は、システム メモリのサーフェスとの間の非同期の DMA はことはできません。 DX8 ドライバー自体には、ロックのシステム メモリのサーフェスをページングする必要がありますしないと、システム メモリのビデオ メモリの転送には、同期する必要があります。

 

 





