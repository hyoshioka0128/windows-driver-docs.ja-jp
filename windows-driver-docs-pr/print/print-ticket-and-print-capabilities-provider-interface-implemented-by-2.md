---
title: 印刷チケットと印刷機能のプロバイダー インターフェイス
description: プリンター ドライバーによって実装される印刷チケットと印刷機能のプロバイダー インターフェイス
ms.assetid: a14c1173-0419-44c7-bc8f-7197590083b3
keywords:
- プリンター インターフェイス DLL の WDK、印刷チケットのサポート
- プリンター インターフェイス DLL の WDK、印刷機能のサポート
- 印刷機能の WDK、プリンター インターフェイス DLL
- 印刷チケット WDK、プリンター インターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac6ea6df77763b73c467ea6e2013663f9cb1ba51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372080"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-printer-drivers"></a>プリンター ドライバーによって実装される印刷チケットと印刷機能のプロバイダー インターフェイス


Windows Vista オペレーティング システムでは、すべてのドライバーの基本的な印刷チケットのサポートを提供します。 ただし、サポートは Microsoft Win32 アプリケーション プログラミングを使用して、ドライバーによってパブリックに公開される情報にのみ基づいてインターフェイス (Api) など、 **DeviceCapabilities**と**を調べるため**およびの公開部分の設定によって、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体。 ドライバーでは、ドライバーの印刷チケットを実装してより豊富なエクスペリエンスを提供できは、次のトピックで説明されている機能プロバイダー インターフェイスを印刷することができます。

印刷チケットと印刷機能のプロバイダー インターフェイスの実装は、プロバイダーを呼び出すは、アプリケーションによって決まります、同時に行われる可能性がありますので、マルチ スレッドのセーフにすることがあります。

 

 




