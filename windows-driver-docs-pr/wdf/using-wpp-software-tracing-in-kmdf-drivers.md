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
ms.openlocfilehash: a8a6fb0f7cc6c2e3933396a270eca24d87b1ea6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570451"
---
# <a name="using-wpp-software-tracing-in-kmdf-drivers"></a>KMDF ドライバーでの WPP ソフトウェア トレースの使用


[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)ドライバーをデバッグする際に役立つトレース メッセージを追加することができます。 さらに、フレームワークの[イベント ロガー](using-the-framework-s-event-logger.md)数百のトレース メッセージを表示することができますを提供します。

使用してトレース メッセージを表示する[traceview で](https://msdn.microsoft.com/library/windows/hardware/ff553872)または[Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994)します。 できます[カーネル デバッガーにトレース メッセージを送信](https://msdn.microsoft.com/library/windows/hardware/ff546837)します。

### <a name="adding-tracing-messages-to-your-driver"></a>ドライバーへのメッセージのトレースの追加

フレームワークに基づくドライバーには、トレース メッセージを追加するには、次の必要があります。

- 追加、 **\#含める**WPP マクロのいずれかを含む、ドライバーのソース ファイルの各ディレクティブ。 このディレクティブを識別する必要があります、[トレース メッセージのヘッダー (TMH) ファイル](https://msdn.microsoft.com/library/windows/hardware/ff553926)します。 ファイル名の形式である必要があります&lt;*ドライバー ソース ファイル名*&gt;**.tmh**します。

  たとえば、ドライバーが 2 つのソース ファイルで構成される場合が呼び出されます*MyDriver1.c*と*MyDriver2.c*、し*MyDriver1.c*含める必要があります。

  **\#include "MyDriver1.tmh"**

  *MyDriver2.c*含める必要があります。

  **\#include "MyDriver2.tmh"**

  Microsoft Visual Studio で、ドライバーをビルドすると、WPP プリプロセッサを生成します。*tmh*ファイル。

- 定義、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)ヘッダー ファイルでマクロ。 このマクロは定義 GUID と[トレース フラグ](https://msdn.microsoft.com/library/windows/hardware/ff553904)ドライバーのトレース メッセージ。

- 含める、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)、ドライバーのマクロ[ **DriverEntry ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff540807)します。 このマクロには、ソフトウェア トレースは、ドライバーがアクティブにします。

- 含める、 [WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)、ドライバーのマクロ[ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)コールバック関数。 このマクロは、ソフトウェア トレースは、ドライバーを無効になります。

- 使用して、 [ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)マクロ、または[カスタマイズされたバージョン](https://msdn.microsoft.com/library/windows/hardware/ff542492)トレース メッセージを作成するのには、ドライバー、マクロの。

- ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。 ドライバーのプロパティ ページで次のようにクリックします。**構成プロパティ**、し**Wpp**します。 下、**全般**] メニューの [設定**WPP トレースの実行**[はい] にします。 下、**ファイル オプション**メニューで、たとえば、フレームワークの WPP テンプレート ファイルを指定することも必要があります。

  ```cpp
  {km-WdfDefault.tpl}*.tmh
  ```
    
- を Visual Studio で、ドライバー プロジェクトの追加の WPP トレース設定を指定するには、ドライバーのプロジェクトをソリューション エクスプ ローラーで右クリックします。 プロパティに次のリンク -> 構成し、プロパティは、WPP トレース]-> [です。 

- トレースの構成ファイルを指定するには、構成データのスキャン設定を使用します。 コマンド ラインの下に追加構成ファイルのトレースの 1 つ以上の -> [追加オプション] には、次のように
  ```cpp
  -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\wdftraceenums.h"
  ```
  トレース メッセージをドライバーを追加する方法の詳細については、次を参照してください。[ドライバーに WPP マクロを追加する](https://msdn.microsoft.com/library/windows/hardware/ff541243)します。

### <a name="sample-drivers-that-use-wpp-software-tracing"></a>WPP ソフトウェア トレースを使用しているサンプル ドライバー

AMCC5933、非 PNP、KMDF\_FX2、PCIDRV、PLX9x5x、およびシリアル[サンプル ドライバー](sample-kmdf-drivers.md) WPP ソフトウェア トレースを使用します。

 

 





