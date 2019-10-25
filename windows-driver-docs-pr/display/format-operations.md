---
title: 書式設定操作
description: 書式設定操作
ms.assetid: 242e5b5a-4184-487a-aeda-19149caa941b
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、テクスチャ形式の一覧
- テクスチャ形式は、WDK DirectX 8.0 を一覧表示します
- Dピクセル形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7226a7fc4b32e961a6f0e60114ef65d7c05880c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839691"
---
# <a name="format-operations"></a>書式設定操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


サポートされている表面形式を報告する場合、DirectX 8.0 ドライバーは、その形式のサーフェイスで実行できる操作を示す必要もあります。 ピクセル形式に対してサポートされる操作は、 [**Dd画素形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の構造体の**dwoperations**フィールドを通じて報告されます。 ドライバーは、このフィールドを、その形式のサーフェイスでサポートされているすべての操作の論理的な組み合わせに設定する必要があります。

 

 





