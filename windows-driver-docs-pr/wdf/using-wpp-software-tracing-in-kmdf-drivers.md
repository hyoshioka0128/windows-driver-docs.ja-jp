---
title: KMDF ドライバーでの WPP ソフトウェア トレースの使用
description: KMDF ドライバーでの WPP ソフトウェア トレースの使用
ms.assetid: dad7aa8d-4ced-47b3-80d2-ec9cfb355783
keywords:
- トレースの WDK、framework ベースのドライバー ソフトウェア
- WDK の KMDF ドライバーのデバッグ ソフトウェア トレース
- WDK、framework ベースのドライバーのトレース
- WDK、framework ベースのドライバーをトレース WPP ソフトウェア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75c7715187396c2e4f8ad34cf5acda990a49485
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372154"
---
# <a name="using-wpp-software-tracing-in-kmdf-drivers"></a>KMDF ドライバーでの WPP ソフトウェア トレースの使用


[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)ドライバーをデバッグする際に役立つトレース メッセージを追加することができます。 さらに、フレームワークの[イベント ロガー](using-the-framework-s-event-logger.md)数百のトレース メッセージを表示することができますを提供します。

使用してトレース メッセージを表示する[traceview で](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)または[Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)します。 できます[カーネル デバッガーにトレース メッセージを送信](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)します。

### <a name="adding-tracing-messages-to-your-driver"></a>ドライバーへのメッセージのトレースの追加

フレームワークに基づくドライバーには、トレース メッセージを追加するには、次の必要があります。

- 追加、 **\#含める**WPP マクロのいずれかを含む、ドライバーのソース ファイルの各ディレクティブ。 このディレクティブを識別する必要があります、[トレース メッセージのヘッダー (TMH) ファイル](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)します。 ファイル名の形式である必要があります&lt;*ドライバー ソース ファイル名*&gt; **.tmh**します。

  たとえば、ドライバーが 2 つのソース ファイルで構成される場合が呼び出されます*MyDriver1.c*と*MyDriver2.c*、し*MyDriver1.c*含める必要があります。

  **\#include "MyDriver1.tmh"**

  *MyDriver2.c*含める必要があります。

  **\#include "MyDriver2.tmh"**

  Microsoft Visual Studio で、ドライバーをビルドすると、WPP プリプロセッサを生成します。*tmh*ファイル。

- 定義、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))ヘッダー ファイルでマクロ。 このマクロは定義 GUID と[トレース フラグ](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)ドライバーのトレース メッセージ。

- 含める、 [WPP\_INIT\_トレース](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))、ドライバーのマクロ[ **DriverEntry ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)します。 このマクロには、ソフトウェア トレースは、ドライバーがアクティブにします。

- 含める、 [WPP\_クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))、ドライバーのマクロ[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)コールバック関数。 このマクロは、ソフトウェア トレースは、ドライバーを無効になります。

- 使用して、 [ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロ、または[カスタマイズされたバージョン](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)トレース メッセージを作成するのには、ドライバー、マクロの。

- ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。 ドライバーのプロパティ ページで次のようにクリックします。**構成プロパティ**、し**Wpp**します。 下、**全般**] メニューの [設定**WPP トレースの実行**[はい] にします。 下、**ファイル オプション**メニューで、たとえば、フレームワークの WPP テンプレート ファイルを指定することも必要があります。

  ```cpp
  {km-WdfDefault.tpl}*.tmh
  ```
    
- を Visual Studio で、ドライバー プロジェクトの追加の WPP トレース設定を指定するには、ドライバーのプロジェクトをソリューション エクスプ ローラーで右クリックします。 プロパティに次のリンク -> 構成し、プロパティは、WPP トレース]-> [です。 

- トレースの構成ファイルを指定するには、構成データのスキャン設定を使用します。 コマンド ラインの下に追加構成ファイルのトレースの 1 つ以上の -> [追加オプション] には、次のように
  ```cpp
  -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\wdftraceenums.h"
  ```
  トレース メッセージをドライバーを追加する方法の詳細については、次を参照してください。[ドライバーに WPP マクロを追加する](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)します。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>WPP ソフトウェア トレースを使用しているサンプル ドライバー

AMCC5933、非 PNP、KMDF\_FX2、PCIDRV、PLX9x5x、およびシリアル[サンプル ドライバー](sample-kmdf-drivers.md) WPP ソフトウェア トレースを使用します。

 

 





