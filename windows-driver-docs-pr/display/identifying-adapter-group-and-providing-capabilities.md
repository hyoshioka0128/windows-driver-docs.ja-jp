---
title: アダプターグループの識別と機能の提供
description: アダプターグループの識別と機能の提供
ms.assetid: 44a2ac71-8852-472f-82a2-7bd4d7dffa1a
keywords:
- 複数ヘッドハードウェア WDK DirectX 9.0、構成
- 複数ヘッドハードウェア WDK DirectX 9.0、アダプター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394bf0aebd46ed8dbc71cbec36ee80516b64d219
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839650"
---
# <a name="identifying-adapter-group-and-providing-capabilities"></a>アダプターグループの識別と機能の提供


## <span id="ddk_identifying_adapter_group_and_providing_capabilities_gg"></span><span id="DDK_IDENTIFYING_ADAPTER_GROUP_AND_PROVIDING_CAPABILITIES_GG"></span>


DirectX 9.0 ランタイムは、D3DGDI2\_TYPE\_GETADAPTERGROUP 値を使用して DirectX 9.0 バージョンのドライバーに**GetDriverInfo2**要求を送信し、ドライバーのマルチヘッドビデオカードを構成するアダプターのグループの識別子を要求します. このドライバーは、 [**DD\_GETADAPTERGROUPDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getadaptergroupdata)構造体の**ulUniqueAdapterGroupId**メンバーの識別子を返します。 ドライバーは、グループ内のマスターおよびすべての下位アダプターの一意の識別子を提供する必要があります。 ランタイムは、後続の操作でこの識別子を使用して、指定されたアダプターがグループに属しているかどうかを判断します。 この識別子は、他のハードウェアベンダーのドライバーを含む、ドライバー間で一意である必要があります。 そのため、この識別子は、他の複数のヘッドビデオカードと共通ではない一意のゼロ以外のカーネルモードアドレスとして報告することをお勧めします。

DirectX 9.0 バージョンドライバーは、D3DCAPS9 構造体の次のメンバーを設定することによって、その複数ヘッドハードウェアがどのように構成されているかを示します。

-   **NumberOfAdaptersInGroup**

    アダプターグループ内のアダプターの数を指定します (マスターの場合のみ)。 これは、シングルヘッドカード (従来のアダプター) では1です。 複数のヘッドカードのマスターアダプターの値が1を超えています。 複数ヘッドカードの下位アダプターの値は0です。 各カードには最大1つのマスターを含めることができますが、多くの下位図形を持つことができます。

-   **MasterAdapterOrdinal**

    グループ内のマスターアダプターの番号を指定します。 この数値は、システムに複数のヘッドカードが1つ以上含まれている場合に関連します。 たとえば、システムにシングルヘッドカード、ダブルヘッドカード、およびトリプルヘッドカードが含まれている場合、システムは、1の場合は0、double の場合は1と2、トリプルの場合は3、4、および5になります。 この場合、マスターアダプターは、single の場合は0、double の場合は1、トリプルの場合は3になります。

-   **AdapterOrdinalInGroup**

    グループ内のヘッドがドライバーによって参照される順序を示す数値を指定します。 マスターアダプターの場合、この値は常に0になり、下位のアダプターごとに連続して番号が付けられます (つまり、1、2など)。

このドライバーは、 **GetDriverInfo2**クエリに対する応答として、D3DCAPS9 構造体を返します。「 [DirectX 8.0 スタイルの Direct3D 機能の報告](reporting-directx-8-0-style-direct3d-capabilities.md)」で説明されているように、D3DCAPS8 構造体を返す方法と似ています。 このクエリのサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。

 

 





