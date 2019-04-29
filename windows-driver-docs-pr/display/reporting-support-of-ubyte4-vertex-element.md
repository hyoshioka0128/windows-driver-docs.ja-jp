---
title: UBYTE4 頂点要素に対するサポートのレポート
description: UBYTE4 頂点要素に対するサポートのレポート
ms.assetid: d5091ceb-71de-4310-95d9-c52361772ebc
keywords:
- UBYTE4 頂点要素 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 637f36ad7a45e1b427d3a10b2c3c06ead731ff79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383235"
---
# <a name="reporting-support-of-ubyte4-vertex-element"></a>UBYTE4 頂点要素に対するサポートのレポート


## <span id="ddk_reporting_support_of_ubyte4_vertex_element_gg"></span><span id="DDK_REPORTING_SUPPORT_OF_UBYTE4_VERTEX_ELEMENT_GG"></span>


DirectX 9.0 バージョンのドライバーが、D3DDTCAPS を設定して UBYTE4 頂点要素型のサポートを報告する必要があります\_UBYTE4 ビット、 **DeclTypes** D3DCAPS9 構造体のメンバー。 Nonsupport UBYTE4 頂点要素型を示すために、ドライバーが設定されていない、D3DDTCAPS\_UBYTE4 ビット。 これに対し、A DirectX 8.1 と以前のドライバーの設定、D3DVTXPCAPS\_いいえ\_VSDT\_UBYTE4 が nonsupport UBYTE4 頂点要素型を示すビットします。

 

 





