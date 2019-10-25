---
title: ハイブリッド システム構成の検証
ms.assetid: 9DB53DAB-0A3D-48A4-84C0-8D60F56B64E8
description: ハイブリッドシステムを検証する手順については、decription をご確認ください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59dc295f82b7d31fdceb874f4521ec36996bd97e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825357"
---
# <a name="validating-a-hybrid-system-configuration"></a>ハイブリッド システム構成の検証


この手順は、ディスプレイアダプターの[ハイブリッドシステム](using-cross-adapter-resources-in-a-hybrid-system.md)の構成を検証するために Windows 8.1 から開始されます。

1.  システムが起動すると、ディスプレイアダプターの1つが現在の POST アダプターとしてマークされます。 この POST アダプターが Windows Display Driver Model (WDDM) 1.3 をサポートし、統合された表示パネルを備えている場合は、統合された*ハイブリッド*アダプターと見なされます。
2.  ハイブリッドシステムの別個のアダプターは、ハイブリッドの*独立*したアダプターと見なされます。 次のものが必要です。
    -   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)を設定します。**HybridDiscrete**メンバー。
    -   WDDM 1.3 をサポートします。
    -   アダプター間のリソースをサポートします。
    -   表示出力がありません。

3.  システムで使用できる WDDM ハイブリッド離散アダプターは1つだけです。
4.  統合されたハイブリッドアダプターが検出されると、次のようになります。
    -   新しい WDDM 1.3 ディスプレイアダプター ((2) または (3) に一致するアダプターを除く)、または基本的な表示ドライバーまたは基本レンダリングドライバーは、すべて読み込まれません。
    -   読み込まれた WDDM 1.3 ディスプレイアダプター (または、(2) または (3) に一致するアダプターを除く)、またはハイブリッド不連続アダプターではない、基本ディスプレイまたは基本レンダリングドライバー) は停止されます。

5.  1\.3 より前の WDDM バージョンをサポートするドライバーは、統合されたハイブリッドアダプターが存在する場合でも読み込むことができます。

 

 





