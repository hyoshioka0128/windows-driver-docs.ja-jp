---
title: COPP と複数モニターのサポート
description: COPP と複数モニターのサポート
ms.assetid: 96bd24f6-4aba-4605-8fd4-465c86061044
keywords:
- コピー防止 WDK COPP、複数をモニターします。
- コピー防止 WDK COPP ビデオ、複数をモニターします。
- COPP WDK DirectX VA、複数をモニターします。
- ビデオの WDK COPP、複数のモニターに保護されています。
- 複数のモニター WDK COPP
- WDK COPP を監視します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aab7bad643d839cfc720262a25e40b4fc467dcb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346936"
---
# <a name="copp-and-multiple-monitor-support"></a>COPP と複数モニターのサポート


## <span id="ddk_copp_and_multiple_monitor_support_gg"></span><span id="DDK_COPP_AND_MULTIPLE_MONITOR_SUPPORT_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

COPP でサポートされている、マルチ モニターのみモードは、デュアル ビューです。 さまざまな複製とシアター モードがサポートされていません。 このルールの唯一の例外では、グラフィックス アダプターが複合および s-ビデオ コネクタを使用して、両方のコネクタを通じて同じ表示信号を同時にフィードの場合です。 ここでは、ビデオのミニポート ドライバーでは、s-ビデオ コネクタことを報告する必要があり、アプリケーションによって開始される COPP 呼び出しによって要求されたときに両方の表示出力に適切な保護が適用されていることを確認する必要があります。

 

 





