---
title: VF ミニポート ドライバーの INF 要件
description: VF ミニポート ドライバーの INF 要件
ms.assetid: D15B337F-EC63-4E9A-94DA-E7F0487D5D48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8689e6415e710b2d6a7ae6fce9022283dbe493c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327709"
---
# <a name="inf-requirements-for-vf-miniport-drivers"></a>VF ミニポート ドライバーの INF 要件


PCI Express (PCIe) 仮想機能 (VF) ミニポート ドライバーの INF ファイルでは、シングル ルート I/O 仮想化 (SR-IOV) の標準化された INF キーワードが指定されていません。 INF ファイルのみ PCIe 物理機能 (PF) のでは、標準化された SR-IOV キーワードを指定します。 これらのキーワードの詳細については、次を参照してください。 [PF ミニポート ドライバーの INF 要件](inf-requirements-for-pf-miniport-drivers.md)します。

VF のミニポート ドライバーの INF では、ネットワーク アダプターの場合は、その他の INF ファイルと同じ要件が (で唯一の例外) に従います。 詳細については、次を参照してください。[ネットワーク デバイスの標準化された INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

唯一の例外は、VF ミニポート ドライバーの INF ファイルが SR-IOV 対応のデータ パスを管理するサービスにバインドのリレーションシップを定義する必要があります。 失敗するようにネットワーク アクセスできる経由で合成データ パスに、VF データ パスが何らかの理由で破棄する場合に必要です。 これらのデータ パスの詳細については、次を参照してください。 [SR-IOV データ パス](sr-iov-data-paths.md)します。

これらのデータ パスを管理するサービスにバインドする、VF ミニポート ドライバーの INF ファイルがの次の設定を指定する必要があります、 **UpperRange**と**LowerRange**エントリ。

``` syntax
HKR, Ndi\Interfaces, UpperRange, 0, "ndisvf"
HKR, Ndi\Interfaces, LowerRange, 0, "iovvf"
```

 

 





