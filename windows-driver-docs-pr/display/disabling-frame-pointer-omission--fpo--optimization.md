---
title: フレーム ポインターの省略 (FPO) の最適化の無効化
description: Windows 7、Windows Display Driver Model (WDDM) 1.1 のカーネル モード ドライバーがパフォーマンスの問題を診断する機能を向上させるためにフレーム ポインターの省略 (FPO) の最適化を無効にする必要があります。
ms.assetid: ABA1A097-D9AA-41F4-90D4-B2FBB9B08534
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a7ac0ce1a713890191b74b55cdecd7734a2a9cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358918"
---
# <a name="disabling-frame-pointer-omission-fpo-optimization"></a>フレーム ポインターの省略 (FPO) の最適化の無効化


Windows 7、Windows Display Driver Model (WDDM) 1.1 のカーネル モード ドライバーがパフォーマンスの問題を診断する機能を向上させるためにフレーム ポインターの省略 (FPO) の最適化を無効にする必要があります。 Windows 8 以降、同じ要件がすべての WDDM 1.2 とそれ以降のドライバー (ユーザー モードおよびカーネル モード) の該当するため FPO フィールドに関連するパフォーマンスの問題をデバッグしやすきます。

|                                                                                   |                                                                                    |
|-----------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| WDDM の最小バージョン                                                              | 1.2                                                                                |
| Windows の最小バージョン                                                           | 8                                                                                  |
| ドライバーの実装など、完全なグラフィックをのみを表示したりのみを表示                | 必須                                                                          |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | [WHQL FPO 最適化は、カーネルのビデオ ドライバーを確認します。](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2) |

 

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で[カーネルのビデオ ドライバーの WHQL FPO 最適化チェック](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2ad364ea-73db-47b6-a627-dea13e7c17d2)します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





