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
ms.openlocfilehash: 9d3d751bb13851f9c0c18fbbf4062b1e6b8b9231
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578598"
---
# <a name="handling-existing-monitor-configurations"></a>既存のモニター構成の処理


新しいモニターを検出するほか、2 つのモニターの構成で TMM ダイアログを起動するには、TMM もする必要があります復元前の構成を表示します。 TMM はを通じてユーザー モードのディスプレイ ドライバーにデータの表示を渡すことによって表示の構成を復元することができます、 [ **IViewHelper::SetConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff568176)メソッド。 TMM はメモリを割り当てるし、メモリ内の表示モードとトポロジの情報を格納します。 TMM 渡すのでは、このメモリを**IStream**インターフェイス、 *pIStream*パラメーターの**された SetConfiguration**を指します。 ユーザー モードのディスプレイ ドライバーを変更したりその他の表示データ (たとえば、ガンマまたはテレビの設定) にもできます。 データの表示では、ドライバーが完了したら、ドライバーを呼び出す、 **IStream::Release**メモリを解放するメソッド。

次の図は、TMM 既存のモニター構成を復元するときに発生する操作の流れを示しています。

![既存のモニター構成を復元するかを示す図](images/tmm-existconfig.png)

 

 





