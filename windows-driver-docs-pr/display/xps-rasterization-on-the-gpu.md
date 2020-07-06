---
title: GPU での XPS ラスター化
description: GPU での XML Paper Specification (XPS) のラスタライズでは、独立系ハードウェアベンダー (IHV) コードやドライバーの動作の変更は必要ありません。
ms.assetid: 3C43552A-7D2B-4C10-9AD3-66755171D997
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87b5701fb9e56bdaa3430e03011e116ebf09a33b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968487"
---
# <a name="xps-rasterization-on-the-gpu"></a>GPU での XPS ラスター化


GPU での XML Paper Specification (XPS) のラスタライズでは、独立系ハードウェアベンダー (IHV) コードやドライバーの動作の変更は必要ありません。 ただし、XPS ラスタライズは、ドライバーコードでバグまたは不適切な想定を公開する可能性がある使用パターンです。 Windows Display Driver Model (WDDM) 1.2 以降のドライバーは、高品質の Windows 印刷を確実に行うために、XPS ラスタライズの表示に準拠したテストを渡すことができる必要があります。

**最小 WDDM バージョン**: 1.2

**Windows の最小バージョン**: 8

**ドライバーの実装—完全なグラフィックスと表示のみ**: 必須

** [Whck](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)の要件とテスト**:**デバイスグラフィックのヲ**


 

## <a name="span-idxpsspanspan-idxpsspanxps-rasterization-conformance"></a><span id="xps"></span><span id="XPS"></span>XPS ラスタライズの適合性


XPS ラスタライズの表示に関する要件は、WDDM GPU ドライバーが XPS ラスタライザーのコンテキストで Direct2D によって使用される場合に、正しいラスタライズ結果を生成するかどうかを決定します。

XPS ラスタライザーは、XPS 印刷記述子言語 (PDL) をラスタライズするために Windows 印刷ドライバーによって頻繁に使用されるシステムコンポーネントです。 ラスタライズの結果が正しいかどうかを判断するために、サブジェクト WDDM GPU ドライバーを使用するシステムで XPS ラスタライザーから取得された結果と、XPS ラスタライザーのベースライン使用から取得した結果の間で比較が実行されます。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、**デバイス**の関連する[whck のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





