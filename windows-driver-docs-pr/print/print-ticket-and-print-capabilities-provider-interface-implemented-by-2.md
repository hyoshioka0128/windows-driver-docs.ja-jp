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
ms.openlocfilehash: a4ae80ca8503431540f6a3aae4f723b71e8703a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364002"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-printer-drivers"></a>プリンター ドライバーによって実装される印刷チケットと印刷機能のプロバイダー インターフェイス


Windows Vista オペレーティング システムでは、すべてのドライバーの基本的な印刷チケットのサポートを提供します。 ただし、サポートは Microsoft Win32 アプリケーション プログラミングを使用して、ドライバーによってパブリックに公開される情報にのみ基づいてインターフェイス (Api) など、 **DeviceCapabilities**と**を調べるため**およびの公開部分の設定によって、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体。 ドライバーでは、ドライバーの印刷チケットを実装してより豊富なエクスペリエンスを提供できは、次のトピックで説明されている機能プロバイダー インターフェイスを印刷することができます。

印刷チケットと印刷機能のプロバイダー インターフェイスの実装は、プロバイダーを呼び出すは、アプリケーションによって決まります、同時に行われる可能性がありますので、マルチ スレッドのセーフにすることがあります。

 

 




