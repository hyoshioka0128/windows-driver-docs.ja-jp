---
title: シングル ルート I/O 仮想化 (SR-IOV) の概要
description: シングル ルート I/O 仮想化 (SR-IOV) の概要
ms.assetid: B241F468-F568-4500-9356-E576CEBA8F3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba74bd92a204a7828e85239ff1e142a1d405b9a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548855"
---
# <a name="overview-of-single-root-io-virtualization-sr-iov"></a>シングル ルート I/O 仮想化 (SR-IOV) の概要


シングル ルート I/O 仮想化 (SR-IOV) のインターフェイスでは、PCI Express (PCIe) 仕様の拡張機能です。 SR-IOV は、さまざまな PCIe ハードウェア関数間でリソースへのアクセスを分離する、ネットワーク アダプターなどのデバイスにできます。 これらの関数は、次の種類で構成されます。

-   PCIe 物理機能 (PF)。 この関数は、デバイスの主な機能であり、デバイスの SR-IOV 機能をアドバタイズします。 PF は、仮想化環境で、HYPER-V 親パーティションに関連付けられます。

-   1 つまたは複数 PCIe 仮想機能 (Vf)。 各 VF は PF. のデバイスの関連付け VF では、PF でデバイス上の他の VFs、メモリ、ネットワーク ポートなど、デバイスの 1 つまたは複数の物理リソースを共有します。 各 VF は、仮想化環境での HYPER-V 子パーティションに関連付けられます。

各 PF と VF には、一意 PCI Express 要求者 ID (RID) I/O メモリ管理ユニット (IOMMU) を異なるトラフィック ストリームを区別し、メモリを適用し、PF と VFs 間の変換を中断できるが割り当てられます。 これにより、適切な HYPER-V の親または子パーティションに直接配信されるトラフィック ストリームができます。 その結果、特権を持たないデータ トラフィック、PF から VF に他の VFs の影響を与えずにされます。

SR-IOV は、HYPER-V 仮想化スタックのソフトウェア スイッチ レイヤーをバイパスするネットワーク トラフィックを使用できます。 VF は、子パーティションに割り当てられている、ため、ネットワーク トラフィックは VF と子パーティション間で直接フローします。 結果として、ソフトウェア エミュレーション レイヤー入出力のオーバーヘッドは減少しは nonvirtualized 環境と同様にほぼ同等のパフォーマンスは、ネットワーク パフォーマンスを発揮します。

詳しくは、次のトピックをご覧ください。

[SR-IOV のアーキテクチャ](sr-iov-architecture.md)

[SR-IOV 対応のデータ パス](sr-iov-data-paths.md)

 

 





