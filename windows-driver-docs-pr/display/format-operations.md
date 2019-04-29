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
ms.openlocfilehash: 7499aa4041c462ee53f9307a6b7abdca9cc120e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325338"
---
# <a name="format-operations"></a>形式の操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


サポートされている画面形式のレポート操作は、その形式の画面で実行できるを DirectX 8.0 ドライバーが示すも必要があります。 ピクセル形式のサポートされている操作がを通じて報告された、 **dwOperations**のフィールド、 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)構造体。 ドライバーは、このフィールドを論理的に組み合わせたその形式のサーフェスのすべてのサポートされている操作を設定する必要があります。

 

 





