---
title: KMDF ドライバーでの WPP ソフトウェア トレースの使用
description: KMDF ドライバーでの WPP ソフトウェア トレースの使用
ms.assetid: dad7aa8d-4ced-47b3-80d2-ec9cfb355783
keywords:
- ソフトウェアトレース WDK、フレームワークベースのドライバー
- ドライバーのデバッグ WDK KMDF、ソフトウェアのトレース
- WDK のトレース、フレームワークベースのドライバー
- WPP ソフトウェアトレース WDK、フレームワークベースのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 851abe9f4548d18641b9d69f0f9f2406606edca2
ms.sourcegitcommit: 6914901515545eda08b2c35bef816e6e2711a5b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86944618"
---
# <a name="using-wpp-software-tracing-in-kmdf-drivers"></a>KMDF ドライバーでの WPP ソフトウェア トレースの使用


[WPP ソフトウェアトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)を使用すると、ドライバーのデバッグに役立つトレースメッセージを追加できます。 さらに、フレームワークの[イベントロガー](using-the-framework-s-event-logger.md)には、表示できる数百のトレースメッセージが用意されています。

トレースメッセージは、 [traceview](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)または[traceview](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)を使用して表示できます。 [トレースメッセージをカーネルデバッガーに送信](https://docs.microsoft.com/windows-hardware/drivers/devtest/how-do-i-send-trace-messages-to-a-kernel-debugger-)することもできます。

### <a name="adding-tracing-messages-to-your-driver"></a>ドライバーへのトレースメッセージの追加

フレームワークベースのドライバーにトレースメッセージを追加するには、次のことを行う必要があります。

- すべての WPP マクロを含む各ドライバーのソースファイルに、 ** \# include**ディレクティブを追加します。 このディレクティブは、[トレースメッセージヘッダー (TMH) ファイル](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-message-header-file)を識別する必要があります。 ファイル名の形式は、ドライバーの &lt; *ソースファイル名* &gt; **. tmh**である必要があります。

  たとえば、ドライバーが*MyDriver1*と*MyDriver2*という2つのソースファイルで構成されている場合、 *MyDriver1*には次のものが含まれている必要があります。

  **\#"MyDriver1" を含めます。**

  および*MyDriver2*には次のものが含まれている必要があります。

  **\#"MyDriver2" を含めます。**

  Microsoft Visual Studio でドライバーをビルドすると、WPP プリプロセッサによってが生成されます。*tmh*ファイル。

- ヘッダーファイルで、 [WPP \_ 制御 \_ guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロを定義します。 このマクロは、ドライバーのトレースメッセージの GUID と[トレースフラグ](https://docs.microsoft.com/windows-hardware/drivers/devtest/trace-flags)を定義します。

- 使用するドライバーの[**Driverentry ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)に、 [WPP \_ INIT \_ TRACING](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))マクロを含めます。 このマクロは、ドライバーのソフトウェアトレースをアクティブにします。

- 使用するドライバーの[*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)コールバック関数に、 [WPP \_ クリーンアップ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))マクロを含めます。 このマクロは、ドライバーのソフトウェアトレースを非アクティブにします。

- トレースメッセージを作成するには、ドライバーで[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロまたはマクロのカスタマイズされた[バージョン](https://docs.microsoft.com/windows-hardware/drivers/devtest/can-i-customize-dotracemessage-)を使用します。

- ドライバープロジェクトのプロパティページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。 ドライバーのプロパティページで、[**構成プロパティ**]、[ **Wpp トレース**] の順にクリックします。 [**全般**] メニューの [ **WPP トレースの実行**] を [はい] に設定します。 [**ファイルオプション**] メニューで、フレームワークの WPP テンプレートファイルも指定する必要があります。次に例を示します。

  ```cpp
  {km-WdfDefault.tpl}*.tmh
  ```
    
- Visual Studio でドライバープロジェクトの追加の WPP トレース設定を指定するには、ソリューションエクスプローラーでドライバープロジェクトを右クリックします。 次に、[プロパティ->構成プロパティ->WPP トレース] へのリンクをクリックします。 

- トレース構成ファイルを指定するには、[構成データのスキャン] 設定を使用します。 複数のトレース構成ファイルの場合は、次のように ' コマンドライン '-> ' 追加オプション ' の下に追加します。
  ```cpp
  -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\wdftraceenums.h"
  ```
  ドライバーにトレースメッセージを追加する方法の詳細については、「[ドライバーへの WPP マクロの追加](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-wpp-macros-to-a-trace-provider)」を参照してください。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>WPP ソフトウェアトレースを使用するサンプルドライバー

AMCC5933、NONPNP、KMDF \_ FX2、PCIDRV、PLX9x5x、およびシリアル[サンプルドライバー](sample-kmdf-drivers.md)は、WPP ソフトウェアトレースを使用します。

 

 





