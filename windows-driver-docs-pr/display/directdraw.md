---
title: DirectDraw
description: DirectDraw
ms.assetid: b7f1194e-0f5e-444e-a71c-6a4a836547d9
keywords:
- DirectDraw WDK Windows 2000 ディスプレイ
- Windows 2000 display driver model WDK、DirectDraw
- ディスプレイドライバーモデル WDK Windows 2000、DirectDraw
- ヘッダーファイルの WDK DirectDraw
- DirectDraw WDK Windows 2000 表示、ヘッダーファイル
- WDK DirectDraw の描画
- WDK DirectDraw、ヘッダーファイルの描画
- グラフィックス WDK Windows 2000 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4264ba68e863c72f99df4da5f97451a8d0e0e639
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839736"
---
# <a name="directdraw"></a>DirectDraw


## <span id="ddk_directdraw_gg"></span><span id="DDK_DIRECTDRAW_GG"></span>


このセクションでは、Microsoft DirectDraw のインターフェイスとアーキテクチャについて説明し、DirectDraw ドライバーライターの実装ガイドラインを示します。 このガイドラインは、Microsoft Windows 2000 以降用に記述されています。 このリーダーは、DirectDraw Api に精通しており、Windows 2000 display driver model をしっかりと把握している必要があります。

Microsoft Windows 2000 以降用の Microsoft DirectDraw ドライバーを作成するドライバーライターでは、次のヘッダーファイルを使用する必要があります。

-   ddrawint には、DirectDraw ドライバーの基本型、定数、および構造体が含まれてい*ます。*

-   *ddraw*には、アプリケーションとドライバーの両方で使用される基本的な型、定数、および構造体が含まれています。

-   *dvp*は、ドライバーが DirectDraw ビデオポート拡張 (VPE) をサポートしている場合に使用されます。

-   *dxmini .h*は、ビデオミニポートドライバーが、カーネルモードのビデオトランスポート、dxmini インターフェイス (dxmini によって指定された関数[ **\_インターフェイス**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)構造) をサポートしている場合に使用されます。

-   *ddkmapi .h*は、 [**dxapi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)関数にアクセスするためにビデオキャプチャドライバーによって使用されます。 さらに、DirectDraw は、DxApi インターフェイスを呼び出します。

-   dmemmgr は、DirectDraw ランタイムに依存するのではなく、ドライバーが独自のメモリ管理を実行する場合に使用し*ます。*

-   *ddkernel. h*は、ドライバーにカーネルモードのサポートが含まれている場合に使用されます。

-   *dx95type*を使用すると、ドライバーの作成者は、既存の windows 98/Me ドライバーを windows 2000 以降に簡単に移植できます。 このヘッダーファイルは、2つのプラットフォームで異なる名前をマップします。

Ddraw ヘッダーファイルには Windows SDK が付属してい*ます*。その他のすべてのヘッダーファイルは、Windows Driver Kit (WDK) に含まれています。 Windows Driver Development Kit (DDK) には、 *p3samp*ビデオ表示ディレクトリにある DirectDraw ドライバー用のサンプルコードも含まれています。

DirectDraw ドライバーの関数、コールバック、および構造体のリファレンスページについては、「 [Directdraw Driver functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) 」と「 [directdraw driver 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)体」を参照してください。

DirectDraw の詳細については、Windows SDK を参照してください。 DirectDraw ドライバーの作成者は、 <em>directx@microsoft.com</em>に質問やコメントを電子メールで送信できます。

 

 





