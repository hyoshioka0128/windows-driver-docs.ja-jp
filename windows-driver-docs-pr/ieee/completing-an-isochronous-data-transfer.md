---
title: 等時性データ転送の完了
description: 等時性データ転送の完了
ms.assetid: 1fc98e1b-4dd5-4358-aa23-86fcbbf33967
keywords:
- アイソクロナス I/O WDK の IEEE 1394 バス、転送の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d067da9616af8750db5e27f30322c1c29cc81ef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376699"
---
# <a name="completing-an-isochronous-data-transfer"></a>等時性データ転送の完了





デバイスは、データを転送する必要がないと、ドライバーは、操作が完了して設定するときに、割り当てられたアイソクロナス リソースの割り当てを解除し、バスを伝える必要があります。

ドライバーは、クリーンアップする次の手順に従う必要があります。

1.  ドライバーでアイソクロナス操作が開始された場合、 [**要求\_アイソクロナス\_リッスン**](https://msdn.microsoft.com/library/windows/hardware/ff537655)または[**要求\_アイソクロナス\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537660) bus 要求を発行する必要がある必要があります、 [**要求\_アイソクロナス\_停止**](https://msdn.microsoft.com/library/windows/hardware/ff537659)バスの通知への要求ドライバーをアイソクロナスの操作を停止します。

2.  使用してリソース ハンドルにアタッチされているままにするバッファーをデタッチする必要があります、 [**要求\_アイソクロナス\_デタッチ\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff537651)要求。

3.  を通じて、解放する必要があります、ドライバーには、リソース ハンドルが割り当てられているが場合、 [**要求\_アイソクロナス\_FREE\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537654)要求。

4.  を通じて、解放する必要がありますドライバーに割り当てられたチャネルがある場合、 [**要求\_アイソクロナス\_FREE\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537653)要求。

5.  ドライバーを使用して割り当て済み、帯域幅の割り当てを解除する必要があります、 [**要求\_アイソクロナス\_FREE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537652)要求。

 

 




