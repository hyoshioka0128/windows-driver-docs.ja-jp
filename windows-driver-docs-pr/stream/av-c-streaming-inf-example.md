---
title: AV/C ストリーミングの INF の例
description: AV/C ストリーミングの INF の例
ms.assetid: c8a2c9cd-c71b-4fd1-80f5-34d13837865e
keywords:
- AV/C WDK、Stream フィルター ドライバー
- フィルター ドライバー WDK AV/C を Stream
- Avcstrm.sys ストリーミング フィルター ドライバー WDK、INF の例
- INF ファイル ストリーミング WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6717b21fb421315c1418bc8383392e78c8c6f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386763"
---
# <a name="avc-streaming-inf-example"></a>AV/C ストリーミングの INF の例





(サブユニット デバイス ドライバーのインストール) の中に、関数のドライバーの INF ファイルをインストール*Avcstrm.sys*ドライバー スタックの低いフィルター ドライバーとして。 INF ファイルが含まれて、"。*hw*"セクションのデバイスのインストールを実行します。 次のコード例は、追加する方法を示します*Avcstrm.sys* Windows 2000 またはそれ以降のオペレーティング システムまたは Windows Millennium Edition、Windows 98、または Windows 95 またはを使用して、以降のオペレーティング システム上の低いフィルター ドライバーとして"サブユニット"としてインストール セクション名:

```INF
[Subunit.HW]
AddReg=Subunit_AddFilter_W9x

[Subunit.NT.HW]
AddReg=Subunit_AddFilter_NT

[SubUnit_AddFilter_W9x]
HKR,,"LowerFilters",0x00010000,"avcstrm.sys"; Win9X use "avcstrm.sys" as driver name

[Subunit_AddFilter_NT]
HKR,,"LowerFilters",0x00010000,"AVCSTRM"; NT use this "AVCSTRM" as Service name
```

Windows 2000 以降、function ドライバーも行う必要があります、必要なドライバーの依存関係サービスで、適切なドライバーの読み込み順序を保持するためにセクションをインストールします。 次の例では、サブユニット ドライバーの前に、AVCSTRM サービスのセクションが読み込まれます。

```INF
ServiceBinary = %12%\subunit.sys
Dependencies  = AVCSTRM   ; loaded before subunit.sys
```

デバイスのインストール ファイルの詳細については、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

 

 




