---
title: ユーザー モード ドライバーのログ記録
description: ビデオメモリの実用的な内訳を取得するには、Windows Display Driver Model (WDDM) ドライバーが Microsoft Direct3D リソースとビデオメモリ割り当ての関係を公開する必要があります。
ms.assetid: E850E148-821D-4544-A778-00B1B9D13964
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf4b5995ad14eaf7b0e45af85ceda7130a2898bc
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967898"
---
# <a name="span-iddisplayuser-mode_driver_loggingspanuser-mode-driver-logging"></a><span id="display.user-mode_driver_logging"></span>ユーザー モード ドライバーのログ記録


ビデオメモリの実用的な内訳を取得するには、Windows Display Driver Model (WDDM) ドライバーが Microsoft Direct3D リソースとビデオメモリ割り当ての関係を公開する必要があります。 これは、Windows 8 以降では、追加のユーザーモードドライバー (UMD) ログインターフェイスの導入によって可能になりました。 この情報を Windows イベントトレーシング (ETW) トレースに追加すると、API の観点からビデオメモリの割り当てを確認することができます。

**最小 WDDM バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックスとレンダーのみ**: 必須

** [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)必要条件とテスト**:**デバイス. グラフィックヲ umdlogging**


 

開発者にとって、UMD ログを使用すると、内部的な断片化、またはサーフェイスを迅速に破棄した場合の影響など、現在見にくいメモリのコストを明確にすることができます。 これにより、Microsoft は、パフォーマンスの問題を分析するためのトレースを提供しているお客様やパートナーとの連携を向上させることができます。 特に、この機能は、メモリ関連のパフォーマンスの問題を調査する際に、一般的なブロックポイントを克服するのに役立ちます。アプリケーションではワーキングセットが大きすぎますが、この問題の原因となっている API リソースや呼び出しを特定することはできません。

このドライバーは、UMD ETW インターフェイスを実装することによって、Direct3D リソースとビデオメモリ割り当ての間の関係を公開する必要があります。 ドライバーは、ログ記録イベントに加えて、リソースと割り当ての間の既存のすべてのマッピングを任意の時点で報告できる必要があります。

## <a name="span-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanspan-idumd_driver_allocation_logging_ddispanumd-driver-allocation-logging-ddi"></a><span id="UMD_driver_allocation_logging_DDI"></span><span id="umd_driver_allocation_logging_ddi"></span><span id="UMD_DRIVER_ALLOCATION_LOGGING_DDI"></span>UMD ドライバー割り当てログ DDI


ユーザーモードドライバー割り当てログデバイスドライバーインターフェイス (DDI) では、Windows イベントトレーシング (ETW) カーネルレベルのトレース機能の下にイベントが提供されます。この機能は、Microsoft DirectX graphics カーネルサブシステム (Dxgkrnl.sys) のどの API リソースがどのカーネル割り当てに関連付けられているかを示します。

この DDI を使用すると、内部メモリの断片化を検出したり、データが急激に破棄された場合の影響を検出したりできます。また、パフォーマンスの問題を特定し、アプリのリソースまたは API の呼び出しによって、メモリのワーキングセットが大きすぎて使用されているかどうかを判断するのに役立ちます。

次の関数、列挙、および Umdprovider .h ヘッダーの構造を使用して、ユーザーモードの表示ドライバーでイベントをログに記録します。

-   [**Umdetwlogmapallocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogmapallocation)関数
-   [**Umdetwlogunmapallocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwlogunmapallocation)関数
-   [**Umdetwregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwregister)関数
-   [**Umdetwunregister 解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/nf-umdprovider-umdetwunregister)関数
-   [**UMDETW \_割り当て \_ セマンティック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/ne-umdprovider-_umdetw_allocation_semantic)列挙型
-   [**UMDETW \_割り当ての \_ 使用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/umdprovider/ns-umdprovider-_umdetw_allocation_usage)構造

Umdetw ヘッダーも参照してください。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、デバイス上の関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください **。**

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





