---
title: IRP 優先度ヒントの使用
description: IRP 優先度ヒントの使用
ms.assetid: c34afff2-32f2-451b-ab16-ff048d5c3204
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b95d6bc15b496e46042d3211c37ae43b001de5d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383287"
---
# <a name="using-irp-priority-hints"></a>IRP 優先度ヒントの使用


*IRP の優先度ヒント*は、 [ **IO\_優先度\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_io_priority_hint) IRP に関連付けられている値。 IRP の優先順位のヒントは Irp の相対的な重要度を示す簡単なヒント表示メカニズムを提供します。 IRP が処理される順序を選択するときに、ドライバーは IRP の優先度のヒントを使用できます。 IRP の優先順位のヒントは、Windows Vista 以降のオペレーティング システムで利用できます。

IRP の優先順位のヒントの詳細については、次を参照してください。、 [Windows Vista での I/O 優先順位付け](https://go.microsoft.com/fwlink/p/?linkid=67877)ホワイト ペーパー。

 

 




