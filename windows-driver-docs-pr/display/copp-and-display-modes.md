---
title: COPP と表示モード
description: COPP と表示モード
ms.assetid: e7da753d-0ccd-428e-b51f-3fd0a19674e8
keywords:
- コピー防止 WDK COPP、表示モード
- ビデオのコピー防止 WDK COPP、表示モード
- COPP WDK DirectX va なので、表示モード
- 保護されたビデオの WDK COPP、表示モード
- WDK COPP の表示モード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b438aa71b0ff24f5eb07683650114aa6337f5fcb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370276"
---
# <a name="copp-and-display-modes"></a>COPP と表示モード


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

ビデオのミニポート ドライバーは、物理的なコネクタでサポートされているすべての保護の種類が現在使用されている表示モードに関係なく、DirectX VA COPP デバイスに関連付けられているレポートする必要があります。 呼び出しを受信すると、ビデオのミニポート ドライバーがサポートされている保護の種類を報告、 [ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus) 、DXVA で関数を\_COPPQueryProtectionType 設定、 **guidStatusRequestID**のメンバー、 [ **DXVA\_COPPStatusInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)構造体。 詳細については、次を参照してください。 [COPP 状態](copp-status.md)します。

特定の保護の種類では、現在の解像度が大きすぎる場合は、その後、ビデオのミニポート ドライバーの[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数が呼び出され、その保護の種類の保護レベルを設定、ドライバーはエラーを返す必要があります。 場合の例を次のシナリオに与えるドライバーの*COPPCommand*関数は、成功またはエラーを返す必要があります。

-   DirectX VA COPP デバイスがコネクタでは、s-ビデオ出力、ビデオのミニポート ドライバーへの呼び出しに関連付けられている場合は[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus) DXVA で関数を\_COPPQueryProtectionType 設定アナログ コンテンツ保護 (ACP) 型のサポートを指定する必要があります (COPP\_ProtectionType\_ACP)。 その後場合、ドライバーの[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数が呼び出され、このコネクタで ACP の種類のレベルを設定、ドライバーは、s-ビデオの出力解像度は固定であるためも成功した場合に返す必要がありますただしデスクトップ解像度 (表示モード) より高い場合があります。

-   DirectX VA COPP デバイスは、ビデオのミニポート ドライバーへの呼び出しのコンポーネント出力コネクタに関連付けられて[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus) DXVA で関数を\_COPPQueryProtectionType 設定ACP 型のサポートを示す必要があります。 ただし場合、ドライバーの[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)ディスプレイの解像度が 720 p または 1080 i の場合は、この出力では、ACP 型のレベルを設定する関数は、ドライバーは、DDERR を返す必要があります\_TOOBIGSIZE エラー コードのコンポーネント出力のコネクタで ACP の種類の保護レベルを設定するには、解像度が大きすぎるためです。

 

 





