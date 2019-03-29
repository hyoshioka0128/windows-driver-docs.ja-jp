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
ms.openlocfilehash: cab5d2eec86f70402741518a4c81bd7b072fe85a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574078"
---
# <a name="present-and-getbltstatus"></a>現状と GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


ランタイム DX8 を呼び出して不要になった[ *DdGetBltStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549385) blt システム メモリのサーフェスに関連するのです。 これは、Windows 2000 の動作では常にです。 結果は、システム メモリのサーフェスとの間の非同期の DMA はことはできません。 DX8 ドライバー自体には、ロックのシステム メモリのサーフェスをページングする必要がありますしないと、システム メモリのビデオ メモリの転送には、同期する必要があります。

 

 





