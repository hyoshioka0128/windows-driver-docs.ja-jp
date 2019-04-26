---
title: モード情報とパス情報との関係
description: モード情報とパス情報との関係
ms.assetid: 214717dd-1c01-4daf-9296-586299668d3a
keywords:
- 接続には、WDK の Windows 7 の表示、CCD 概念、モード、およびパスの情報が表示されます。
- 接続には、WDK の Windows Server 2008 R2 の表示、CCD 概念、モード、およびパスの情報が表示されます。
- 構成するには、WDK の Windows 7 の表示、CCD 概念、モード、およびパスの情報が表示されます。
- 構成するには、WDK の Windows Server 2008 R2 の表示、CCD 概念、モード、およびパスの情報が表示されます。
- CCD WDK Windows 7 の概念の表示、モードとパスの情報
- CCD 概念 WDK Windows Server 2008 R2 の表示、モードとパスの情報
- モードとパス情報 WDK Windows 7 の表示
- モードとパス情報 WDK Windows Server 2008 R2 の表示
- パスとモード情報 WDK Windows 7 の表示
- パスとモード情報 WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53658021a130763c19ac750fa3a2c73acecafa1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351470"
---
# <a name="relationship-of-mode-information-to-path-information"></a>モード情報とパス情報との関係


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) CCD 関数は、パス情報は、特定の表示構成のソースとターゲットのモードの情報に常に返します。 次の図は、パス情報をソースとターゲットのモードの情報を関連付ける方法の例を示します。 この例では、QDC\_すべて\_パス フラグに渡されました、*フラグ*への呼び出しでパラメーター **QueryDisplayConfig**します。

![パス情報をモードの情報の関係を示す図](images/displayconfigpathandmode.png)

 

 





