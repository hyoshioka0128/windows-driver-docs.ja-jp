---
title: GPU 上で XPS ラスタライズ
description: XML Paper Specification (XPS) ラスタライズ GPU 上では、独立系ハードウェア ベンダー (IHV) コードやドライバーの動作の変更は必要ありません。
ms.assetid: 3C43552A-7D2B-4C10-9AD3-66755171D997
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95436d3e791d758404b9e29672e215c7eca4620c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551147"
---
# <a name="xps-rasterization-on-the-gpu"></a>GPU 上で XPS ラスタライズ


XML Paper Specification (XPS) ラスタライズ GPU 上では、独立系ハードウェア ベンダー (IHV) コードやドライバーの動作の変更は必要ありません。 ただし、XPS ラスタライズ、バグまたはドライバーのコードで不適切な想定を公開することができます可能性のある使用状況パターンです。 Windows 表示 Driver Model (WDDM) 1.2 およびそれ以降のドライバーが XPS ラスタライズ ディスプレイへの準拠テストを高品質な Windows 印刷を確保するために渡すことがあります。

|                                                                                   |                                                   |
|-----------------------------------------------------------------------------------|---------------------------------------------------|
| WDDM の最小バージョン                                                              | 1.2                                               |
| Windows の最小バージョン                                                           | 8                                                 |
| ドライバーの実装: 完全なグラフィックスおよび表示のみ                              | 必須                                         |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要件とテスト | **Device.Graphics¦XPSRasterizationConformance** |

 

## <a name="span-idxpsspanspan-idxpsspanxps-rasterization-conformance"></a><span id="xps"></span><span id="XPS"></span>XPS ラスタライズへの準拠


XPS ラスタライズ表示への準拠要件は、WDDM GPU ドライバーでは、Direct2D で XPS ラスタライザーのコンテキストで使用した場合に、適切なラスタライズ結果が得られますかどうかを判断します。

XPS ラスタライザーは、ラスタライズする XPS 印刷記述子言語 (PDL) 印刷ドライバーを Windows でよく使われるシステム コンポーネントです。 XPS ラスタライザー WDDM GPU ドライバーの件名の付いたシステムで実行されたときから取得される結果と XPS ラスタライザーの基準の使用から得られた結果の間、比較が実行をラスタライズ結果の正確性を判断するには.

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... XPSRasterizationConformance**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





