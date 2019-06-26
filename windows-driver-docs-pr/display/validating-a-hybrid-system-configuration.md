---
title: ハイブリッド システム構成の検証
ms.assetid: 9DB53DAB-0A3D-48A4-84C0-8D60F56B64E8
description: ハイブリッド システムを検証する手順の説明。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89920a5759876e703358a0a271006c022a357e54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374368"
---
# <a name="validating-a-hybrid-system-configuration"></a>ハイブリッド システム構成の検証


このプロシージャは使用では、Windows 8.1 以降の構成を検証する、[ハイブリッド システム](using-cross-adapter-resources-in-a-hybrid-system.md)ディスプレイ アダプター。

1.  システムのブート ディスプレイ アダプターのいずれか、現在の POST アダプターとマークされます。 この投稿のアダプターでは、Windows 表示 Driver Model (WDDM) 1.3 をサポートし、統合表示パネルと見なされます、*統合ハイブリッド*アダプター。
2.  ハイブリッド システムで、個別のアダプターと見なされます、*ハイブリッド不連続*アダプター。 必要です。
    -   設定、 [ **DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps).**HybridDiscrete**メンバー。
    -   WDDM 1.3 をサポートします。
    -   クロス アダプターのリソースをサポートします。
    -   表示の出力しないことがあります。

3.  1 つだけの WDDM ハイブリッド個別のアダプターは、システム上で許可されています。
4.  ハイブリッド統合アダプターが検出された場合。
    -   任意の新しい WDDM 1.3 ディスプレイ アダプター (アダプター (2) に一致するか、(3) を除外または基本的な表示や basic レンダー ドライバー) は読み込まれません。
    -   すべて読み込む WDDM 1.3 ディスプレイ アダプター ((2) に一致するアダプターまたは (3) を除くまたは基本的な表示や basic レンダー ドライバー)、ハイブリッドの個別のアダプターが停止はありません。

5.  WDDM 以前のバージョン 1.3 をサポートするドライバーは、ハイブリッド統合アダプターが存在する場合にも読み込むことができます。

 

 





