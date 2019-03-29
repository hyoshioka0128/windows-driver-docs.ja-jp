---
title: ネイティブ 802.11 IHV UI 拡張 COM インターフェイス
description: ネイティブ 802.11 IHV UI 拡張 COM インターフェイス
ms.assetid: 95487686-17a0-43e2-93bb-99b3adb9dadd
keywords:
- IHV UI 拡張 DLL WDK ネイティブ 802.11、COM インターフェイス
- COM インターフェイスの WDK ネイティブ 802.11 IHV UI 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a44c0b76244ba7d05efbcbdcbe1912549096686b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580545"
---
# <a name="native-80211-ihv-ui-extensions-com-interfaces"></a>ネイティブ 802.11 IHV UI 拡張 COM インターフェイス




 

802.11 IHV UI 拡張機能のネイティブ DLL では、1 つ以上の次の COM インターフェイスを実装します。

<a href="" id="idot11extui"></a>**IDot11ExtUI**  
を通じて、 **IDot11ExtUI** COM インターフェイスでは、オペレーティング システムのネイティブ 802.11 ネットワークの構成 UI は、802.11 IHV UI 拡張機能のネイティブ DLL と対話できます。 この COM インターフェイスがネイティブの 802.11 ネットワークの構成 UI での DLL をクエリする方法を提供するなど、 **IDot11ExtUIProperty**オペレーティング システムの 802.11 接続の拡張に使用される COM インターフェイスとセキュリティのプロパティ。

802.11 IHV UI 拡張機能のネイティブ DLL での実装を提供する必要があります、 **IDot11ExtUI** COM インターフェイスです。

この COM インターフェイスの詳細については、次を参照してください。 [IDot11ExtUI COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553769)します。

<a href="" id="idot11extuiproperty"></a>**IDot11ExtUIProperty**  
を通じて、 **IDot11ExtUIProperty** COM インターフェイス、802.11 IHV UI 拡張機能のネイティブ DLL がネイティブの 802.11 ネットワークの構成 UI で表示される接続とセキュリティのプロパティを拡張できます。

**IDot11ExtUIProperty** COM インターフェイスは省略可能とは、802.11 IHV UI 拡張機能のネイティブの DLL が、オペレーティング システムの 802.11 の接続とセキュリティのプロパティの拡張機能をサポートしているかが必要です。

802.11 IHV UI 拡張機能のネイティブ DLL がの 1 つまたは複数の実装を提供できる、 **IDot11ExtUIProperty**ネイティブ 802.11 プロパティへの IHV で定義された拡張機能を表す各実装での COM インターフェイスです。 DLL は、セキュリティ設定の 1 つまたは複数のプロパティの拡張機能を提供できます。 Windows Vista では、DLL は、接続の設定は複数のプロパティの拡張機能を追加できます。

この COM インターフェイスの詳細については、次を参照してください。 [IDot11ExtUIProperty COM インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff553746)します。

<a href="" id="iwizardextension"></a>**IWizardExtension**  
802.11 IHV UI 拡張機能のネイティブ DLL がの 1 つまたは複数の実装を提供できる、 **IWizardExtension** COM インターフェイスです。 各実装は、1 つまたは複数のカスタム UI ページの表示をサポートします。 次のいずれかでは、これらの UI ページが表示されます。

-   ネイティブの 802.11 IHV 拡張機能の DLL によって行われた外部要求。 このプロセスの詳細については、次を参照してください。[カスタム UI の表示を要求する](requesting-the-display-of-a-custom-ui.md)します。

-   802.11 IHV 拡張機能のネイティブ DLL に表示するカスタム UI があるかどうかを決定する、オペレーティング システムによって行われたクエリです。 このプロセスの詳細については、次を参照してください。[カスタム UI を表示するためのクエリ](querying-for-the-display-of-a-custom-ui.md)します。

-   802.11 IHV UI 拡張機能のネイティブ DLL のコンポーネントによる内部要求。

詳細については、 **IWizardExtension** COM インターフェイスを参照してください[IWizardExtension COM インターフェイス](https://go.microsoft.com/fwlink/p/?linkid=56607)します。

ネイティブの 802.11 ネットワークの構成 UI コンポーネントの詳細については、次を参照してください。[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)します。

 

 





