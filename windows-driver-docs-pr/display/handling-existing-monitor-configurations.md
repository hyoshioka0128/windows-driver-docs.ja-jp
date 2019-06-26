---
title: 既存のモニター構成の処理
description: 既存のモニター構成の処理
ms.assetid: b2da12ea-cbcd-4754-a65f-e54ed305f5d7
keywords:
- モニターの構成の WDK の表示、復元前
- モニター構成の WDK 表示、既存のモニタ
- TMM WDK の表示、既存のモニターの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322bd3a7737266c46224238be5b48ca34f8869d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382318"
---
# <a name="handling-existing-monitor-configurations"></a>既存のモニター構成の処理


新しいモニターを検出するほか、2 つのモニターの構成で TMM ダイアログを起動するには、TMM もする必要があります復元前の構成を表示します。 TMM はを通じてユーザー モードのディスプレイ ドライバーにデータの表示を渡すことによって表示の構成を復元することができます、 [ **IViewHelper::SetConfiguration** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568176(v=vs.85))メソッド。 TMM はメモリを割り当てるし、メモリ内の表示モードとトポロジの情報を格納します。 TMM 渡すのでは、このメモリを**IStream**インターフェイス、 *pIStream*パラメーターの**された SetConfiguration**を指します。 ユーザー モードのディスプレイ ドライバーを変更したりその他の表示データ (たとえば、ガンマまたはテレビの設定) にもできます。 データの表示では、ドライバーが完了したら、ドライバーを呼び出す、 **IStream::Release**メモリを解放するメソッド。

次の図は、TMM 既存のモニター構成を復元するときに発生する操作の流れを示しています。

![既存のモニター構成を復元するかを示す図](images/tmm-existconfig.png)

 

 





