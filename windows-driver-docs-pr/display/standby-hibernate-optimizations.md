---
title: スタンバイの最適化を休止状態します。
description: Windows 8 には、最適化をドライバー オプションで利用できるのスリープ状態にシステム パフォーマンスが向上し、再開するグラフィックス スタックが用意されています。
ms.assetid: 1E71BFDF-3C67-41F6-968A-8AE54B54CCCB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e12306d7874d99cb0900c94353baeb1c3a2877
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527553"
---
# <a name="standby-hibernate-optimizations"></a>スタンバイの最適化を休止状態します。


Windows 8 には、最適化をドライバー オプションで利用できるのスリープ状態にシステム パフォーマンスが向上し、再開するグラフィックス スタックが用意されています。

|                                                                                   |                                             |
|-----------------------------------------------------------------------------------|---------------------------------------------|
| Windows Display Driver Model (WDDM) の最小バージョン                               | 1.2                                         |
| Windows の最小バージョン                                                           | 8                                           |
| ドライバーの実装: 完全なグラフィックスとレンダリングのみ                               | 省略可能                                    |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | **Device.Graphics¦StandbyHibernateFlags** |

 

## <a name="span-idstandbyhibernatedevicedriverinterfaceddispanspan-idstandbyhibernatedevicedriverinterfaceddispanspan-idstandbyhibernatedevicedriverinterfaceddispanstandby-hibernate-device-driver-interface-ddi"></a><span id="Standby_hibernate_device_driver_interface__DDI_"></span><span id="standby_hibernate_device_driver_interface__ddi_"></span><span id="STANDBY_HIBERNATE_DEVICE_DRIVER_INTERFACE__DDI_"></span>スタンバイ休止状態にデバイス ドライバー インターフェイス (DDI)


これらの構造は、新規または更新済みの休止状態がスタンバイをサポートするために Windows 8 以降では。

-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff562010)
-   [**DXGK\_SEGMENTDESCRIPTOR3**](https://msdn.microsoft.com/library/windows/hardware/hh464086)
-   [**DXGK\_SEGMENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562039)

これらの利点を活かす休止状態にする必要があります最適化この機能をサポートできるすべてのデバイス。 WDDM 1.2 またはそれ以降のドライバーは、セグメントの機能を列挙するときに設定がありますも 1 つまたは複数のスタンバイ休止状態フラグの**PreservedDuringStandby**、 **PreservedDuringHibernate**、および**PartiallyPreservedDuringHibernate**します。 「解説」を参照してください、 [ **DXGK\_SEGMENTFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff562039)詳細についてはトピック。

## <a name="span-idstandbyoptspanspan-idstandbyoptspanusing-standby-hibernate-optimizations"></a><span id="standbyopt"></span><span id="STANDBYOPT"></span>スタンバイを使用して最適化を休止状態


PC がスリープ状態に遷移またはスリープ状態から再開は、そのビデオ メモリの内容を確認するいくつかの操作が発生する場合は正しく保持され、復元します。 これらの操作の一部が不要になりを回避できます。

-   統合型グラフィックス アダプターには、ビデオ メモリとしてのシステム メモリが使用されます。 コンピューターがスリープ状態になる場合に、システム メモリが更新されますが、ため、削除する必要はありません。 そのため、グラフィックス スタックによって導入される遅延できる電源を切るゼロ遅延または数ミリ秒順序。
-   個別のアダプターでのメモリを消去する時間の合計では、削除すると、消去のレートで割った値メモリの量と同じです。 したがってを消去するメモリの量を減らすことで時間を短縮できます。

これらの操作の目的は、破棄される唯一のデータが再作成できるようにデータであるかどうかを確認することです。

WDDM 1.2 ドライバーによっては、電源の状態遷移中にどの割り当てを保持する必要がありますを指定することによってこれらの最適化の利点がかかります。

スタンバイ (自己更新 VRAM) の場合、メモリを更新する、新しい世代の独立したグラフィックス アダプターを設計できます。 これらのアダプターは、これらの最適化を得られます。

削除は、自己更新 VRAM 機能がない独立したグラフィックス アダプターの関連するされます。 このような場合は、パフォーマンスの最適化は保存されているデータの量を最小限に抑えるには。 たとえばなどのビデオ メモリで使用されていないデータは割り当てを提供、破棄の割り当て、および未使用のダイレクト メモリ アクセス (DMA) バッファーを破棄することができます。

この機能はこれらのメリットが得られます。

-   作業を行いません。(自己更新 VRAM 機能) を統合、不連続のグラフィックス アダプター、グラフィックス スタックによって導入される遅延できます電源を切るゼロ遅延または数ミリ秒順序。
-   以下の作業を実行します。独立したグラフィックス アダプターの場合は、パフォーマンスの向上がでビデオ メモリで使用されていないデータの量は破棄されます依存ほとんどの場合です。
-   少ないメモリごみ箱に移動します。大きいほどメモリの量削除されると、メモリの破壊の影響も大きくします。 独立したグラフィックス アダプターより大きな影響は大量のシステム メモリを削除する必要があるため、これが。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... StandbyHibernateFlags**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





