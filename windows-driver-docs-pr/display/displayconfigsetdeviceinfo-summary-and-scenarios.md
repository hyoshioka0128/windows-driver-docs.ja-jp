---
title: DisplayConfigSetDeviceInfo の概要とシナリオ
description: DisplayConfigSetDeviceInfo の概要とシナリオ
ms.assetid: b00c1586-26f0-4fe1-8cc8-3db552ebba86
keywords:
- Windows 7 の WDK の表示、CCD Api、DisplayConfigSetDeviceInfo 接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD Api、DisplayConfigSetDeviceInfo 接続が表示されます。
- Windows 7 の WDK の表示、CCD Api、DisplayConfigSetDeviceInfo 構成が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示、CCD Api、DisplayConfigSetDeviceInfo が表示されます。
- CCD WDK Windows 7 の概念の表示、DisplayConfigSetDeviceInfo
- CCD 概念 WDK Windows Server 2008 R2 の表示、DisplayConfigSetDeviceInfo
- DisplayConfigSetDeviceInfo WDK Windows 7 の表示
- DisplayConfigSetDeviceInfo WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d4d4cc1986671e724bd9554fef8ac91b6fc0b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354832"
---
# <a name="displayconfigsetdeviceinfo-summary-and-scenarios"></a>DisplayConfigSetDeviceInfo の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法をまとめると、 [ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909) CCD 関数を使用するためのシナリオを提供**DisplayConfigSetDeviceInfo**します。

### <a name="span-iddisplayconfigsetdeviceinfosummaryspanspan-iddisplayconfigsetdeviceinfosummaryspandisplayconfigsetdeviceinfo-summary"></a><span id="displayconfigsetdeviceinfo_summary"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SUMMARY"></span>DisplayConfigSetDeviceInfo の概要

呼び出し元が使用できる[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)ターゲットのプロパティを設定します。 **DisplayConfigSetDeviceInfo**を開始することが現在使用のみと停止のブートがアナログのターゲットで force プロジェクションを永続化します。

### <a name="span-iddisplayconfigsetdeviceinfoscenariosspanspan-iddisplayconfigsetdeviceinfoscenariosspandisplayconfigsetdeviceinfo-scenarios"></a><span id="displayconfigsetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SCENARIOS"></span>DisplayConfigSetDeviceInfo シナリオ

[**DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)は、次のシナリオで呼び出されます。

-   ユーザーが、テレビの接続に s-ビデオまたは複合のコネクタを使用して、オペレーティング システムが、テレビを検出できないことがあるとします。 表示のコントロール パネル アプレットを呼び出すことができます[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)コネクタの出力を強制的にします。

-   オペレーティング システムが、EDID を読み取ったり、モニターにできないことと、ユーザーは、スイッチ ボックスを使用または KVM スイッチのことがあるとします。 表示のコントロール パネル アプレットを呼び出すことができます[ **DisplayConfigSetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553909)をコネクタの出力を強制し、解像度を設定します。

 

 





