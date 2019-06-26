---
title: アダプター グループの識別と機能の提供
description: アダプター グループの識別と機能の提供
ms.assetid: 44a2ac71-8852-472f-82a2-7bd4d7dffa1a
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0、構成します。
- 複数ヘッド ハードウェア WDK DirectX 9.0、アダプター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85003a30008b8221b6fde880dd2eb44b8a13ccec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380179"
---
# <a name="identifying-adapter-group-and-providing-capabilities"></a>アダプター グループの識別と機能の提供


## <span id="ddk_identifying_adapter_group_and_providing_capabilities_gg"></span><span id="DDK_IDENTIFYING_ADAPTER_GROUP_AND_PROVIDING_CAPABILITIES_GG"></span>


DirectX 9.0 ランタイムの送信、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETADAPTERGROUP 値を構成するアダプターのグループの識別子を要求する DirectX 9.0 バージョンのドライバーをドライバーの複数ヘッドのビデオ カード。 ドライバーでの識別子を取得する、 **ulUniqueAdapterGroupId**のメンバー、 [ **DD\_GETADAPTERGROUPDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getadaptergroupdata)構造体。 ドライバーは、マスターとグループ内のすべての下位アダプターの一意識別子を提供する必要があります。 ランタイムでは、以降の操作でこの識別子を使用して、特定のアダプターがグループの一部であるかどうかを確認します。 この識別子は、その他のハードウェア ベンダーからドライバーを含む、ドライバーの間で一意である必要があります。 そのため、この識別子を他の複数ヘッドのビデオ カードに共通することはできませんを一意な 0 以外のカーネル モード アドレスとして報告することをお勧めします。

DirectX 9.0 バージョンのドライバーでは、D3DCAPS9 構造体の次のメンバーを設定して、複数ヘッド ハードウェアを構成する方法を示します。

-   **NumberOfAdaptersInGroup**

    (場合にのみマスター) は、アダプターの数、アダプター グループに指定します。 これは、1 つ head カード (従来のアダプター) の場合は 1 です。 値は、複数ヘッド カードのマスターのアダプターに 1 を超えています。 値は、複数ヘッド カードの下位のアダプターの場合は 0 です。 各カードは最大で 1 つのマスターがあることができますが、多くの部下を持つことができます。

-   **MasterAdapterOrdinal**

    グループでは、マスターのアダプターの数を指定します。 この数は、関連するは、システムには、1 つ以上のヘッドが複数のカードが含まれている場合です。 たとえば、ヘッドが 1 つのカード、二重ヘッド カード、および triple ヘッド カードが、システムが含まれる場合、システムとしてヘッドを参照します。1 つの場合は 0、1 と、double 型の 2 と 3、4、および三重の 5。 この場合、マスターのアダプターは次のとおりです。0、1 つを 1 は、double および三重の 3。

-   **AdapterOrdinalInGroup**

    グループ内のヘッドがドライバーによって参照されている順序を示す数を指定します。 この値は、マスターのアダプターの場合は 0 では常に、各下位アダプターの連続した番号 (1、2、およびなど)。

ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

 

 





