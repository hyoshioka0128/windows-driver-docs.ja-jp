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
ms.openlocfilehash: 3369f94dd3d9d852c144e4a2832ad8ac23dabac5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365742"
---
# <a name="displayconfigsetdeviceinfo-summary-and-scenarios"></a>DisplayConfigSetDeviceInfo の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法をまとめると、 [ **DisplayConfigSetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo) CCD 関数を使用するためのシナリオを提供**DisplayConfigSetDeviceInfo**します。

### <a name="span-iddisplayconfigsetdeviceinfosummaryspanspan-iddisplayconfigsetdeviceinfosummaryspandisplayconfigsetdeviceinfo-summary"></a><span id="displayconfigsetdeviceinfo_summary"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SUMMARY"></span>DisplayConfigSetDeviceInfo の概要

呼び出し元が使用できる[ **DisplayConfigSetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)ターゲットのプロパティを設定します。 **DisplayConfigSetDeviceInfo**を開始することが現在使用のみと停止のブートがアナログのターゲットで force プロジェクションを永続化します。

### <a name="span-iddisplayconfigsetdeviceinfoscenariosspanspan-iddisplayconfigsetdeviceinfoscenariosspandisplayconfigsetdeviceinfo-scenarios"></a><span id="displayconfigsetdeviceinfo_scenarios"></span><span id="DISPLAYCONFIGSETDEVICEINFO_SCENARIOS"></span>DisplayConfigSetDeviceInfo シナリオ

[**DisplayConfigSetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)は、次のシナリオで呼び出されます。

-   ユーザーが、テレビの接続に s-ビデオまたは複合のコネクタを使用して、オペレーティング システムが、テレビを検出できないことがあるとします。 表示のコントロール パネル アプレットを呼び出すことができます[ **DisplayConfigSetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)コネクタの出力を強制的にします。

-   オペレーティング システムが、EDID を読み取ったり、モニターにできないことと、ユーザーは、スイッチ ボックスを使用または KVM スイッチのことがあるとします。 表示のコントロール パネル アプレットを呼び出すことができます[ **DisplayConfigSetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfigsetdeviceinfo)をコネクタの出力を強制し、解像度を設定します。

 

 





