---
title: IRP 優先度ヒントの使用
description: IRP 優先度ヒントの使用
ms.assetid: c34afff2-32f2-451b-ab16-ff048d5c3204
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f26eb5e1e9e65365a2d1ec74b5e8e271e186412a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838349"
---
# <a name="using-irp-priority-hints"></a>IRP 優先度ヒントの使用


*Irp 優先度ヒント*は、irp に関連付けられている[**IO\_priority\_hint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_priority_hint)値です。 IRP の優先順位ヒントは、Irp の相対的な重要度を示す単純なヒント機構を提供します。 ドライバーは、irp が処理される順序を選択するときに、IRP の priority ヒントを使用できます。 IRP 優先順位ヒントは、Windows Vista 以降のオペレーティングシステムで使用できます。

IRP 優先度ヒントの詳細については、 [Windows Vista ホワイトペーパーの「i/o の優先順位](https://go.microsoft.com/fwlink/p/?linkid=67877)設定」を参照してください。

 

 




