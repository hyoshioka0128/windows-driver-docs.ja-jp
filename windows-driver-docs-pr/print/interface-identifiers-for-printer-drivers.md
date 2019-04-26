---
title: プリンター ドライバーのインターフェイス ID
description: プリンター ドライバーのインターフェイス ID
ms.assetid: 8182cba5-4461-4ca0-8b01-342519609b1f
keywords:
- COM インターフェイスの WDK の印刷、インターフェイスの識別子
- インターフェイス識別子 WDK を印刷します。
- プラグインを WDK の印刷、インターフェイスの識別子
- 識別子の WDK プリンター
- Guid の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51226fb598705b363f86d120c5a8ba807e98e4b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345289"
---
# <a name="interface-identifiers-for-printer-drivers"></a>プリンター ドライバーのインターフェイス ID





Guid のセットは、prcomoem.h で定義されます。 これらの Guid のそれぞれは、プリンター ドライバー (Unidrv および Pscript5) とプラグイン間の通信に使用する COM インターフェイスのいずれかのインターフェイス識別子です。

Windows 2000 と Windows XP では、次の Guid が定義されています。

**IID\_IPrintOemUI**
**IID\_IPrintOemUI2** (Pscript5 UI のプラグインを Windows XP および Windows オペレーティング システムの以降のバージョン) **IID\_IPrintOemDriverUI**
**IID\_IPrintCoreUI2** (Pscript5 UI のプラグインを Windows XP および Windows オペレーティング システムの以降のバージョン) **IID\_IPrintOemUni**
**IID\_IPrintOemUni2** (Unidrv は、Windows XP と Windows オペレーティング システムの以降のバージョンでは、プラグインをレンダリング) **IID\_IPrintOemUni3** (Unidrv は、Windows Vista および Windows オペレーティング システムの以降のバージョンのプラグインをレンダリング) **IID\_IPrintOemDriverUni**
**IID\_IPrintOemPS**
**IID\_IPrintOemPS2** (Pscript5 は、Windows XP と Windows オペレーティング システムの以降のバージョンでは、プラグインをレンダリング) **IID\_IPrintOemDriverPS**
**IID\_IPrintCorePS2** (Pscript5 レンダリングのプラグインを Windows XP および Windows オペレーティング システムの以降のバージョン) の各 GUID1 つのインターフェイスの 1 つのバージョンを識別します。 インターフェイスの新しいバージョンが定義されている場合は、新しい GUID が一覧に追加されます。

ユーザー インターフェイスのプラグインとプラグインのレンダリングには、サポートされるインターフェイスのバージョンを識別する必要があります。 プリンター ドライバー (Unidrv または Pscript5) の呼び出し、プラグインの**iunknown::queryinterface**メソッド (Windows SDK のドキュメントで説明)、入力としてインターフェイス識別子を指定します。 メソッドが、インターフェイスは、S の状態の戻り値へのポインターを返す必要があります、プラグインは、指定したバージョンをサポートする場合\_ok をクリックします。 返す必要がありますそれ以外の場合、E\_NOINTERFACE します。 ドライバーが最新バージョンのインターフェイスの識別子で開始され、呼び出しを続行**QueryInterface**メソッドを返します秒までの以前のバージョン識別子を持つ\_[ok] またはドライバーの一覧に達した。バージョン識別子。

同様に、Unidrv と Pscript5 指定**iunknown::queryinterface**のメソッド、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md) COM インターフェイスです。 プラグインは、適切なインターフェイスを呼び出す必要があります**QueryInterface**ドライバーがサポートするインターフェイスのバージョンを確認して、インターフェイス ポインターを受け取るメソッド。

 

 




