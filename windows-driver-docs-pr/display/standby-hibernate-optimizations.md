---
title: スタンバイ休止状態の最適化
description: Windows 8 では、ドライバーがスリープと再開のシステムパフォーマンスを向上させるために、必要に応じてを活用できるグラフィックススタックの最適化を提供しています。
ms.assetid: 1E71BFDF-3C67-41F6-968A-8AE54B54CCCB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bda009ca528a5e774775ce6af5c1883521b8bfd
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968589"
---
# <a name="standby-hibernate-optimizations"></a>スタンバイ休止状態の最適化


Windows 8 では、ドライバーがスリープと再開のシステムパフォーマンスを向上させるために、必要に応じてを活用できるグラフィックススタックの最適化を提供しています。

**Windows Display Driver Model (WDDM) の最小バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックスとレンダーのみ**: 省略可能

** [Whck](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)の要件とテスト**:**デバイスグラフィックのヲ**


 

## <a name="span-idstandby_hibernate_device_driver_interface__ddi_spanspan-idstandby_hibernate_device_driver_interface__ddi_spanspan-idstandby_hibernate_device_driver_interface__ddi_spanstandby-hibernate-device-driver-interface-ddi"></a><span id="Standby_hibernate_device_driver_interface__DDI_"></span><span id="standby_hibernate_device_driver_interface__ddi_"></span><span id="STANDBY_HIBERNATE_DEVICE_DRIVER_INTERFACE__DDI_"></span>スタンバイ休止状態デバイスドライバーインターフェイス (DDI)


これらの構造は、スタンバイ休止状態をサポートするために、Windows 8 以降で新しく追加または更新されました。

-   [**DXGK \_ QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)
-   [**DXGK \_ SEGMENTDESCRIPTOR3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentdescriptor3)
-   [**DXGK \_ SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)

この機能をサポートできるすべてのデバイスは、これらの休止状態の最適化を利用する必要があります。 WDDM 1.2 以降のドライバーがセグメントの機能を列挙する場合、 **PreservedDuringStandby**、 **PreservedDuringHibernate**、および**PartiallyPreservedDuringHibernate**の1つ以上のスタンバイ休止状態フラグも設定する必要があります。 詳細については、 [**DXGK \_ SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)トピックの「解説」を参照してください。

## <a name="span-idstandbyoptspanspan-idstandbyoptspanusing-standby-hibernate-optimizations"></a><span id="standbyopt"></span><span id="STANDBYOPT"></span>スタンバイ休止状態の最適化の使用


PC がスリープ状態に移行したり、スリープ状態から再開されたりすると、ビデオメモリの内容が適切に保存および復元されるように、いくつかの操作が発生します。 これらの操作のいくつかは不要であり、回避することができます。

-   統合されたグラフィックスアダプターは、ビデオメモリとしてシステムメモリを使用します。 コンピューターをスリープ状態にすると、常にシステムメモリが更新されるため、削除は必要ありません。 したがって、グラフィックススタックによって発生する遅延は、0遅延または数ミリ秒の順序になることがあります。
-   個々のアダプターのメモリを消去するのにかかる合計時間は、削除されたメモリの量と、消去の比率で割った値になります。 このため、消去するメモリの量を減らすことで時間を短縮できます。

これらの操作の目的は、破棄されるデータだけが再作成できるデータであることを確認することです。

WDDM 1.2 ドライバーは、電源状態遷移中に保持する割り当てを指定することで、これらの最適化を利用できます。

予備のグラフィックスアダプターの新しい世代は、スタンバイ時 (自己更新 VRAM) にメモリを更新するように設計できます。 これらのアダプターは、これらの最適化の恩恵を受けます。

削除は、自己更新の VRAM 機能を持たない個別のグラフィックスアダプターにも当てはまります。 このような場合、パフォーマンスの最適化は、保持されるデータの量を最小限に抑えることになります。 たとえば、提供された割り当て、破棄された割り当て、未使用のダイレクトメモリアクセス (DMA) バッファーなど、ビデオメモリ内の未使用のデータは破棄できます。

この機能では、次の利点が得られる可能性があります。

-   作業を行わない: 統合グラフィックスアダプターと独立したグラフィックスアダプター (自己更新の VRAM 機能を使用) では、グラフィックススタックによって発生する遅延は、ゼロ遅延または数ミリ秒の順序になることがあります。
-   作業量の削減: 個別のグラフィックスアダプターでは、パフォーマンスの向上は、ほとんどの場合、ビデオメモリ内の未使用データの量によって異なります。
-   メモリ trashing の削減: 解放されるメモリの量が多いほど、メモリ trashing の効果が大きくなります。 このため、個別のグラフィックスアダプターは、大量のシステムメモリを削除する必要があるため、大きな影響を与えます。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、**デバイス**の関連する[whck のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





