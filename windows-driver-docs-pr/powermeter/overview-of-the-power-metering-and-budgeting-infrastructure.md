---
title: 電力使用状況測定と予算のインフラストラクチャの概要
description: 電力使用状況測定と予算のインフラストラクチャの概要
ms.assetid: eda1c829-eb5e-404b-bf6b-1b0807ee02c7
keywords:
- 使用状況の測定と予算の WDK の電源の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaeef30d377b47a548a5bb159c00173e995bc017
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538623"
---
# <a name="overview-of-the-power-metering-and-budgeting-infrastructure"></a>電力使用状況測定と予算のインフラストラクチャの概要


Windows 7 および Windows Server 2008 R2 以降、Windows は、電力使用状況測定と予算 (PMB) インフラストラクチャをサポートします。 このインフラストラクチャは、電力消費量と管理機能を提供することで、コンピューター システム上のエネルギー効率を昇格させます。 さらに、追加のオプションを構成する使用状況測定と予算の電源を PMB を提供します。 システムの製造元、IT プロフェッショナル、およびエンドユーザーは、ニーズに応えるには、能力とパフォーマンスのバランスを取るために、システムを調整するのに、PMB インフラストラクチャを使用することができます。

PMB インフラストラクチャは、ユーザー モード アプリケーションとサービスを次の情報を提供します。

<span id="Power_Metering_Information"></span><span id="power_metering_information"></span><span id="POWER_METERING_INFORMATION"></span>電力使用状況測定情報  
この情報は、コンピューター システムまたはサブコンポーネントの電源を使用する方法の決定に使用されます。 電力消費量を監視すると、または*従量制課金*システムの電力メーターによって。 電力使用状況測定では、使用状況測定機能と電力消費量のしきい値などの電力メーターの現在の構成も提供します。

<span id="Power_Budgeting_Information"></span><span id="power_budgeting_information"></span><span id="POWER_BUDGETING_INFORMATION"></span>電源の予算情報  
この情報を使用して、電源の制限を確認または*予算*、つまりコンピューター システムでサポートされています。 ハードウェア プラットフォームによってこの情報がすることもできます、システムの電力の割り当てを構成します。

電源メーターは、単位はワットの電力消費に関する情報をレポートするシステムのハードウェア コンポーネントです。 この情報は、通常、ベースボード管理コント ローラー (BMC) を使用して電源装置の一部として提供されます。 電源メーターは、システム全体の電力消費量や、コンピューターのサブシステムを監視し、イベントを生成する (そのためには構成されている) 場合、次の条件のいずれかに発生します。

-   電力消費量は、電源装置の構成済みの電源のしきい値を超えています。

-   システムによって消費される電力では、構成済みの電力の割り当てに到達します。

複数の電力メーターは、独自のコンポーネントのセットを監視する各電力メーターで、コンピューター システムにインストールできます。

次の図は、PMB インフラストラクチャの概要を示します。

![電力使用状況測定とインフラストラクチャの予算 (pmb) の図の概要 ](images/powermeter-1.png)

PMB は、次のコンポーネントで構成されます。

<span id="User-Mode_Power_Service__UMPS_"></span><span id="user-mode_power_service__umps_"></span><span id="USER-MODE_POWER_SERVICE__UMPS_"></span>ユーザー モード Power サービス (UMPS)  
WMI クラスのセットを使用することによって、UMPS がシステムの電力使用状況測定を公開するユーザー モード サービスと予算情報。 この情報は、電源管理とレポートの Windows パフォーマンス モニター (PerfMon) などのアプリケーションによって使用されます。

PMB WMI クラスは、UMPS の電源の WMI プロバイダーのコンポーネントによって提供されます。 これらの WMI クラスは、バージョンに準拠*Distributed Management Task Force (DMTF) の電源プロファイルの 1.1.0*します。 詳細についてを参照してください、 [DMTF の電源を提供するプロファイル](https://go.microsoft.com/fwlink/p/?linkid=145048)します。

UMPS の詳細については、[ユーザー モードの Power サービス](user-mode-power-service.md)を参照してください。

<span id="Power_Meter_Interface__PMI__"></span><span id="power_meter_interface__pmi__"></span><span id="POWER_METER_INTERFACE__PMI__"></span>電力メーター インターフェイス (PMI)   
PMI は、ドライバーによって提供される WDM インターフェイスです。 このインターフェイスを使用すると、ドライバー サービスの PMI I/O 要求パケット (Irp) から、[電源マネージャー](https://msdn.microsoft.com/library/windows/hardware/ff559829)と、UMPS の電源の WMI プロバイダーのコンポーネント。 これらの Irp は、クエリを実行し、現在の電力使用状況測定と電力メーターから予算情報の設定に使用されます。

Windows 7 および Windows Server 2008 R2 以降のオペレーティング システムでドライバーを提供 (*ACPIPMI します。SYS*) PMI ACPI 4.0 Power メータリング オブジェクトをサポートするシステムを実装します。 このドライバーにより、相手先ブランド供給 (Oem) PMB インフラストラクチャ内でサードパーティ製のドライバーをインストールすることがなく参加できるシステムを構築します。

PMI の詳細については、[電力メーター インターフェイス](power-meter-interface.md)を参照してください。

<span id="ACPI_PMI"></span><span id="acpi_pmi"></span>ACPI PMI  
ACPI PMI では、使用状況測定、予算 WDM PMI インターフェイスを提供するドライバーへのハードウェア プラットフォームの機能と能力を公開します。

ACPI PMI は ACPI 4.0 Power メータリング オブジェクトを使用して提供されます。 これらの ACPI オブジェクトなど、Intelligent Platform Management Interface (IPMI)、電力使用状況測定と予算のハードウェア プラットフォームで使用される、基になるテクノロジに抽象化レイヤーを提供します。

ACPI 4.0 Power メータリング オブジェクトは、ACPI コントロール メソッド バッテリ パラダイムの後にモデル化されます。 システム ファームウェアには、ACPI 4.0 Power メータリング オブジェクトを実装する必要があります。 システム ファームウェアには、ACPI 4.0 Power メータリング オブジェクトも実装する必要があります。 実装の詳細は、独自の各システムに固有です。

詳細については、[ACPI 電力メーター インターフェイス](acpi-power-meter-interface.md)を参照してください。

 

 




