---
title: MB id モーフィング ソリューションの詳細
description: 構成の要件と互換性のある Id モーフィング デバイス MB id について説明します
ms.assetid: E4E17B4F-665B-425C-B90B-F60561B71CAB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76696e4e057e298ccb8a9eddf763fcb287df92b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536671"
---
# <a name="mb-identity-morphing-solution-details"></a>MB Id モーフィング ソリューションの詳細


## <a name="configuration-requirements"></a>構成要件


Windows 8 の遷移の間で関数の順序を維持する必要があります。 たとえば、MBIM が Windows 8 構成では、3 番目の関数の場合もことが、IHV NCM-2.0 の構成では、3 番目の関数。

Windows 7 の構成

Windows 7 構成モーフィングのデバイスの最初の構成があります。 この構成によっては、関数の 1 つとして、大容量記憶装置の関数が必要です。 Windows 8 では、この構成は選択しません。 Windows 7 と Windows の以前のバージョンでは、Windows 7 構成は、既定の構成を選択します。 この構成は、Ihv が IHV のドライバーをインストールすることができるドライバー パッケージを配置 USB 大容量記憶装置の関数を公開に使用されます。

Windows 8 の構成

Windows 7 構成では、MBCD が読み込まれる関数の 1 つとして、MBIM 関数を公開します。 Windows 8 では、この構成の値が返された USBCCGP subCompatibleID 値で使用されます。 USBCCGP は、読み込まれるときに、この構成を選択します。 Windows 8 構成は、2、3、または 4 のいずれかの構成にあります。 Windows 8 構成としては、その他の構成はサポートされていません。 この構成では、大容量記憶装置の関数が、IHV のドライバー パッケージをインストールするようにする場合は、最初の関数としても公開します。

IHV NCM 2.0 構成

IHV-NCM-2.0 の構成では、MBIM と共に IHV 固有の関数と大容量記憶装置の機能を公開します。 この構成を設定しないまたは Windows で使用されるは。 ユーザーがインストールした後、IHV ソフトウェアがこの構成に変形ことができます。 この構成では、関数の順序が Windows 8 構成のように同じであることに注意してください。 追加の関数は、Windows 8 構成に追加できる、同じ順序で既存の関数を保持する必要があります。

IHV NCM 1.0 構成

IHV-NCM-1.0 の構成では、NCM 1.0 と共に IHV 固有の関数と大容量記憶装置の機能を公開します。 この構成を設定しないまたは Windows 8 で使用されるは。 この構成は、ユーザーが、IHV ソフトウェアをインストールした後、Windows 7 および Windows の以前のバージョンでのみ使用されます。 IHV ソフトウェア モーフィング モーフィング デバイスを Windows 7 構成からこの構成を行います。

## <a name="compatible-ids"></a>互換性 Id


互換性 Id は、ドライバーを Windows に基本設定の読み込みを示すために、デバイスによって使用される 8 文字以下の文字列です。 デバイスは、Microsoft OS ディスクリプターを使用して、互換性 Id を定義できます。 互換性のあるおよび subcompatible Id は、個々 の関数に適用されます。 各構成には、互換性のある Id では、その構成内の関数のセットを割り当てるの個別セットを持つことができます。 互換性のあるおよび subcompatible Id は、個々 の関数に適用されます、モーフィングのデバイスでは、構成が選択されていないときに、1 つの互換性のある ID を持つことができます。 この互換性があり、subcompatible ID は、論理的にモーフィング デバイス全体に適用されます。

**USBCCGP の読み込み**

Windows 8 で USBCCGP ドライバーが自動的に構成を選択する Windows-8 - モーフィングのデバイスで必要です。

USBCCGP ドライバーの読み込み、モーフィングのデバイスをモーフィング デバイスの構成が選択されていないときに、次の互換性があり、subcompatible Id を報告する必要があります。

-   モーフィング デバイスは、関数にグループ化のインターフェイスの Iad を使用している場合、互換性のある ID は"ALTRCFG"および Windows 8 構成の番号として subcompatible ID として報告する必要があります。
-   モーフィング デバイスは、関数にグループ化のインターフェイスの WCM Ufd を使用している場合、互換性のある ID は"WMCALTR"および Windows 8 構成の番号として subcompatible ID として報告する必要があります。

たとえば、Windows 8 構成が構成 3 の場合は、subcompatible ID でどちらの場合に、「3」をなります。

**互換性 Id をモーフィング**

USB デバイスの列挙中にモーフィング デバイスの構成が選択されていない場合、USBHUB は互換性のある ID にモーフィングのデバイスを照会します。 モーフィング デバイスは」の説明に従って、USBCCGP を読み込むために使用する互換性があり、subcompatible の ID を返します[MB Id モーフィング ソリューションの概要](mb-identity-morphing-solution-overview.md)します。

USBHUB USBCCGP を読み込んだ後、USBCCGP は以前に報告 subcompatible ID で示される構成を選択します。 USBCCGP は、もう一度 subcompatible との互換性 ID し照会します。 この時点では、変換時のデバイスでは、現在選択されている構成と互換性があり subcompatible Id を返す必要があります。 そのため、USBCCGP は読み込みし、特定の構成を選択、変換時のデバイスを報告される subcompatible との互換性 Id の変形を必要があります。 USBCCGP を読み込み、構成を選択した後に使用される subcompatible との互換性 Id を報告しないモーフィングのデバイスを使用してする必要があります。

![usbhub 列挙処理中に、デバイスから microsoft os ディスクリプターをクエリします。](images/mbim13.png)

USBHUB 列挙処理中に、デバイスから Microsoft OS ディスクリプターをクエリします。

![デバイスは、未構成の状態で compatid を返します。 ](images/mbim14.png)

デバイスは、未構成の状態で CompatId を返します。 この CompatId は USBCCGP の読み込みに使用されます。

![usbccgp subcompatible id で報告される構成を選択します。](images/mbim15.png)

USBCCGP subcompatible ID で報告される構成を選択します

![デバイスの新しい構成に基づき、microsoft os 記述子モーフィングを行います。 microsoft os ディスクリプターを usbccgp 照会します。](images/mbim16.png)

デバイスの新しい構成に基づき、Microsoft OS 記述子モーフィングを行います。 Microsoft OS ディスクリプターを USBCCGP 照会します。

![デバイスでは、任意の compatid は返されません。 クラスに基づく/サブクラス/プロトコル、usbccgp usbstor と mbcd を読み込みます。](images/mbim17.png)

デバイスでは、任意の CompatID は返されません。 クラスに基づく/サブクラス/USBSTOR と MBCD はプロトコル、USBCCGP を読み込みます。

 

 





