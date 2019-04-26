---
title: DDI コンプライアンス規則
description: DDI コンプライアンス規則
ms.assetid: f020fff9-f880-4aa8-b422-5452728d2fdd
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d1261b3e37bef67b11d9b3844abed2b3c2e1cdef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345756"
---
# <a name="ddi-compliance-rules"></a>DDI コンプライアンス規則


このセクションでは、一覧表示し、Windows Driver Model (WDM)、カーネル モード ドライバー フレームワーク (KMDF)、オーディオ (PortCls) AVStream (KS)、NDIS、および Storport ドライバーの検証に使用できる Windows デバイス ドライバー インターフェイス (DDI) コンプライアンス規則について説明します。 DDI 準拠規則は、ドライバーとオペレーティング システムのカーネル インターフェイスの適切な相互作用するための要件を定義します。

[オーディオ ドライバーの規則](rules-for-audio-drivers.md)  
[AVStream ドライバーの規則](rules-for-avstream-drivers.md)  
[WDM ドライバーの規則](sdv-rules-for-wdm-drivers.md)  
[KMDF ドライバーの規則](sdv-rules-for-kmdf-drivers.md)  
[NDIS ドライバーの規則](sdv-rules-for-ndis-drivers.md)  
[Storport ドライバーの規則](sdv-rules-for-storport-drivers.md)  

### <a name="driver-verification-tools"></a>ドライバー検証ツール

コード分析ツールを使用する[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)と[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448) DDI の使用に関する規則に準拠する目的のドライバーをテストします。 Static Driver Verifier (SDV) は、SDV は、開発サイクルの早い段階で使用できるように、ドライバーのソース コードのスタティック分析を実行します。 Driver Verifier は、実行時にドライバーをテストするには、後にビルド、展開、およびインストールされているため、オペレーティング システムと統合されます。

ドライバーのソース コードを使用して[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)ドライバーとオペレーティング システムのモデルを作成します。 SDV はこのモデルで悪意のある環境でドライバーを配置し、体系的に、ドライバーを経由するパスの形式化された一連のドライバーのコンプライアンス規則の違反を探すことによってコード テスト ([Static Driver Verifier ルール](https://msdn.microsoft.com/library/windows/hardware/ff552839))。

Windows 8 以降を構成できます[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)コンプライアンスが有効にするとに、インストールされているドライバーでの確認に同じの一部を実行する[DDI 準拠の検査](https://msdn.microsoft.com/library/windows/hardware/hh454208)します。

## <a name="related-topics"></a>関連トピック


[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)
[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)
 

 





