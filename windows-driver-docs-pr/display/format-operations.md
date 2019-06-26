---
title: 形式の操作
description: 形式の操作
ms.assetid: 242e5b5a-4184-487a-aeda-19149caa941b
keywords:
- テクスチャ形式の一覧が DirectX 8.0 リリース ノート WDK Windows 2000 の表示
- テクスチャ形式には、WDK の DirectX 8.0 が一覧表示されます。
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ae4f4e261ccc5f7b2ed6e730051ec2970649d0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356371"
---
# <a name="format-operations"></a>形式の操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


サポートされている画面形式のレポート操作は、その形式の画面で実行できるを DirectX 8.0 ドライバーが示すも必要があります。 ピクセル形式のサポートされている操作がを通じて報告された、 **dwOperations**のフィールド、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)構造体。 ドライバーは、このフィールドを論理的に組み合わせたその形式のサーフェスのすべてのサポートされている操作を設定する必要があります。

 

 





