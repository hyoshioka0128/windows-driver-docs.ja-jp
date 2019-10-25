---
title: COPP と表示モード
description: COPP と表示モード
ms.assetid: e7da753d-0ccd-428e-b51f-3fd0a19674e8
keywords:
- コピー防止 WDK COPP、表示モード
- ビデオコピー防止 WDK COPP、表示モード
- COPP WDK DirectX VA、表示モード
- 保護されたビデオ WDK COPP、表示モード
- 表示モード WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ded167c890e83ac087cfddcdc2d5b3daa3365f2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839786"
---
# <a name="copp-and-display-modes"></a>COPP と表示モード


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

ビデオミニポートドライバーは、現在使用されている表示モードに関係なく、DirectX VA COPP デバイスに関連付けられている物理コネクタでサポートされているすべての保護の種類を報告する必要があります。 ビデオミニポートドライバーは、DXVA の**Guidstatusrequestid**メンバーで DXVA\_COPPQueryProtectionType が設定された[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数への呼び出しを受信すると、サポートされている保護の種類を報告します[ **\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体。 詳細については、「 [Copp Status](copp-status.md)」を参照してください。

現在の解像度が特定の保護の種類に対して大きすぎる場合は、その保護の種類の保護レベルを設定するためにビデオミニポートドライバーの[*Coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数が呼び出されると、ドライバーからエラーが返されます。 次のシナリオは、ドライバーの*Coppcommand*関数が成功またはエラーを返す場合の例を示しています。

-   DirectX VA COPP デバイスが S-Video 出力コネクタに関連付けられている場合、DXVA\_COPPQueryProtectionType セットでビデオミニポートドライバーの[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数を呼び出すと、アナログコンテンツ保護 (ACP) のサポートが示される必要があります。「(COPP\_ProtectionType\_ACP)」と入力します。 その後、ドライバーの[*Coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数を呼び出して、このコネクタで ACP 型のレベルを設定すると、ドライバーは成功を返します。これは、デスクトップの解像度 (表示モード) が高い場合でも、s-Video の出力解像度が固定されているためです。

-   DirectX VA COPP デバイスがコンポーネント出力コネクタに関連付けられている場合、DXVA\_COPPQueryProtectionType set でビデオミニポートドライバーの[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数を呼び出すと、ACP 型のサポートも示される必要があります。 ただし、ディスプレイの解像度が720p または1080i の場合、ドライバーの[*Coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数を呼び出して、この出力で ACP 型のレベルを設定すると、ドライバーは DDERR\_TOOBIGSIZE エラーコードを返す必要があります。これは、解像度が大きすぎてコンポーネント出力コネクタの ACP 型の保護レベル。

 

 





