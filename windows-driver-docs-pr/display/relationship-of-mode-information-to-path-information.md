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
ms.openlocfilehash: 3618bfce50b5fc39191566b05ba9ea00cdf7527f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386450"
---
# <a name="relationship-of-mode-information-to-path-information"></a>モード情報とパス情報との関係


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) CCD 関数は、パス情報は、特定の表示構成のソースとターゲットのモードの情報に常に返します。 次の図は、パス情報をソースとターゲットのモードの情報を関連付ける方法の例を示します。 この例では、QDC\_すべて\_パス フラグに渡されました、*フラグ*への呼び出しでパラメーター **QueryDisplayConfig**します。

![パス情報をモードの情報の関係を示す図](images/displayconfigpathandmode.png)

 

 





