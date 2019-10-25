---
title: 既定の NDIS ポート
description: 既定の NDIS ポート
ms.assetid: a9edf83f-9226-4c75-a04e-1879a05df24c
keywords:
- ポート WDK NDIS、既定値
- NDIS ポート WDK、既定の NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa9056de179be320963a3f57436bed4c72f7d741
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838171"
---
# <a name="default-ndis-port"></a>既定の NDIS ポート





ポート0は、ミニポートアダプターの既定のポートとして予約されています。 任意の構造体の任意の関数また**はポート番号のメンバーの**ポート番号パラメーターが0に設定さ*れている*場合、ミニポートドライバーがポートを割り当てなかったか、現在のアクティビティがポートに固有ではありません。

既定の NDIS ポートの例としては、負荷分散とフェールオーバー (LBFO) MUX 中間ドライバーを検討してください。 このようなドライバーの仮想ミニポートは、ポートゼロ (既定のポート) にすることができます。 中間のドライバーは、1からポートの数 (*N*) までのポート番号を使用して、基になるミニポートアダプターにポートを割り当てることができます。 前のドライバーがポート0にデータを送信して、LBFO ドライバーが基になるポートのいずれかを選択できるようにするか、または、後続のドライバーで 1 ~ *N*のポート番号を指定して、送信操作に特定のポートを選択することができます。

ミニポートドライバーは、ポートを割り当てたり、既定のポート以外のポート番号をサポートしたりする必要はありません。 ミニポートドライバーによってポートが割り当てられていない場合でも、NDIS は[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数を呼び出して NDIS\_ミニポートに登録属性を設定した後に、既定のポートを割り当ててアクティブにし[ **\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)の構造体です。 **NdisMSetMiniportAttributes**が正常にを返した場合、ミニポートドライバーは、既定のポートで操作を開始できます。 この場合、NDIS はミニポートドライバーが[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数から戻るときに既定のポートを解放します。

 

 





