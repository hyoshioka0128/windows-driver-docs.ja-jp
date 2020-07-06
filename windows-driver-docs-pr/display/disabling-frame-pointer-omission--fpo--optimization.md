---
title: フレーム ポインターの省略 (FPO) の最適化の無効化
description: Windows 7 では、フレームポインターの省略 (FPO) の最適化を無効にしてパフォーマンスの問題を診断する機能を向上させるために、Windows Display Driver Model (WDDM) 1.1 カーネルモードドライバーが必要です。
ms.assetid: ABA1A097-D9AA-41F4-90D4-B2FBB9B08534
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 443d813cbd232a8c0475b3395ab83d5d4a3cb2d8
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967967"
---
# <a name="disabling-frame-pointer-omission-fpo-optimization"></a>フレーム ポインターの省略 (FPO) の最適化の無効化


Windows 7 では、フレームポインターの省略 (FPO) の最適化を無効にしてパフォーマンスの問題を診断する機能を向上させるために、Windows Display Driver Model (WDDM) 1.1 カーネルモードドライバーが必要です。 Windows 8 以降では、すべての WDDM 1.2 以降のドライバー (ユーザーモードとカーネルモード) に同じ要件が適用されるため、フィールドの FPO に関連するパフォーマンスの問題を簡単にデバッグできます。

**最小 WDDM バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックス、描画のみ、表示のみ**: 必須

** [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト**: [WHQL FPO の最適化チェック (カーネルビデオドライバー](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2) )


 

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、「[カーネルビデオドライバーの WHQL FPO の最適化チェック](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2)」の関連する[whck ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





