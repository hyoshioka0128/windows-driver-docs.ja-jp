---
title: SKU の差別化ディレクティブ
description: Windows Server 2008 および Windows Vista SP1 でボックス表示ドライバーの Inf を変更すると、クライアントでのみ意味をドライバーは、サーバー Sku の Windows ではインストールしないと、ドライバーを表す新しい値が含まれます。
ms.assetid: 9E31BD57-41B6-40DF-AF27-8EAC66BDFE09
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81557e368bf9e6cca606d82250b7d7809dacc07b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360330"
---
# <a name="sku-differentiation-directive"></a>SKU の差別化ディレクティブ


Windows Server 2008 と Windows Vista SP1 では、インボックスのディスプレイ ドライバーの Inf としてドライバーを表す新しい値を含める変更された*クライアントのみ*ドライバーはサーバー Sku の Windows でインストールすることを意味します。 このディレクティブは、Windows 8 でのすべてのディスプレイ ドライバーに必要です。

Windows Vista SP1 より前に、で、次の値を使用しました。

``` syntax
X86:
[Manufacturer]
%ATI% = ATI.Mfg

[ATI.Mfg]

In Vista SP1\Server 2008 the following values were used; 
X86:
[Manufacturer]
%ATI% = ATI.Mfg,NTx86...1

[ATI.Mfg.NTx86...1]

X64:
[Manufacturer]
%ATI% = ATI.Mfg,NTamd64...1

[ATI.Mfg.NTamd64...1]
```

Windows 8、Windows Vista SP1 および Windows Server 2008 用に使用されたのと同じ値が使用されます。

## <a name="span-idskudifferentiationfordevicedriversspanspan-idskudifferentiationfordevicedriversspanspan-idskudifferentiationfordevicedriversspansku-differentiation-for-device-drivers"></a><span id="SKU_differentiation_for_device_drivers__"></span><span id="sku_differentiation_for_device_drivers__"></span><span id="SKU_DIFFERENTIATION_FOR_DEVICE_DRIVERS__"></span>デバイス ドライバーの SKU の差別化


独立系ハードウェア ベンダー (Ihv) は、指定した INF がサーバーまたはクライアントのプラットフォームのみに対して有効であることを示す ProductType INF の値を使用できます。 これは Windows XP およびそれ以降のオペレーティング システムで動作し、変更が比較的簡単に実装します。

そのため、クライアント専用のドライバー パッケージがサーバー システムのドライバー ストアに存在する場合でもそのドライバーはインストールできません。

[ **INF 製造元セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)を追加する方法について説明*TargetOSVersion*さまざまな条件に基づいてフィルター デバイスのインストールにします。 これらの条件の 1 つは*ProductType*、これは、パッケージのインストール先の Sku のカテゴリを指定に使用できます。 次の値が定義されている*ProductType*:

``` syntax
0x0000001 (VER_NT_WORKSTATION)
0x0000002 (VER_NT_DOMAIN_CONTROLLER)
0x0000003 (VER_NT_SERVER) 
```

任意の指定されたアーキテクチャでは、一般的な INF は、次のように、任意の SKU をインストールする修飾されています。

``` syntax
[Manufacturer]
%MSFT%=Models,amd64

[Models.NTamd64]
<models entries>
```

クライアントにインストールするには、この INF を制限するためにのみ、に装飾、ProductType「1」を追加する必要があります。 数は、10 進数または 16 進数として表される可能性があります。 ドキュメントが 16 進数を示していますが、わかりやすくするための 10 進数の例で使用します。

``` syntax
[Manufacturer]
%MSFT%=Models,amd64...1

; models section for workstation
[Models.NTamd64...1]
<models entries>
```

サーバーの場合、構文に分解して、クライアントとプレーンなサーバーにインストールします。 これらの各は、独自の製品の種類があります。 残念ながら、INF 構文には、両方の場合を対象に両方を指定する必要があります。 そのためにサーバー SKU を実際に対応するモデル セクション全体を複製する必要があります。

``` syntax
[Manufacturer]
%MSFT%=Models,amd64...1amd64...3

; models section for client
[Models.NTamd64...1]
IHV_DeviceName.XXX = "Foo Generic Device Name (Microsoft Corporation - WDDM v1.2)"
IHV_DeviceName.YYY = "Foo Enthusiast Device Name (Microsoft Corporation - WDDM v1.2)"
<models entries>

; models section for Server
[Models.NTamd64...3]
IHV_DeviceName.XXX = "Foo Generic Name (Microsoft Corporation - WDDM v1.2)"
IHV_DeviceName.ZZZ = "Foo Datacenter Name (Microsoft Corporation - WDDM v1.2)"
<models entries>
```

 

 





