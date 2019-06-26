---
title: 印刷ジョブのレンダリング
description: 印刷ジョブのレンダリング
ms.assetid: 78967839-b518-41c0-8825-b00f8b8560e6
keywords:
- 印刷ジョブをプリンター グラフィックス レンダリングの DLL の WDK
- グラフィックス DLL WDK プリンター、印刷ジョブの表示
- WDK の印刷ジョブの表示
- WDK のジョブを印刷するレンダリング
- WDK の印刷ジョブを表示
- WDK の縞模様の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909275ada9c8ccd101b8a503d140d9cb2bde850b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383531"
---
# <a name="rendering-a-print-job"></a>印刷ジョブのレンダリング





印刷ジョブは、作成、または EMF レコードとして、スプール ファイルに書き込まれたか、レンダリングされます。 場合は、EMF レコードのレンダリングは配置するときに、EMF*プリント プロセッサ*(localspl.dll) が再生するレコード。 以降ではユーザー モードの GDI 描画、関数への呼び出しの一連のレンダリングで構成されます**フォーマット**(Microsoft Windows SDK のドキュメントで説明)。 呼び出し**フォーマット**一連の一連のグラフィックスのレンダリング エンジン (GRE、カーネル モードの GDI とも呼ばれます)、およびプリンター グラフィックス DLL に関連するアクションにつながるアプリケーション呼び出しの最初します。

次の図は、カーネル モードの GDI やプリンター グラフィックス DLL 間の相互作用を示しています。 後**フォーマット**が呼び出されます。

![フォーマットが呼び出された後に、カーネル モードの gdi とプリンターのグラフィックス dll 間の相互作用を示す図](images/gdirendr2.png)

1.  アプリケーションを呼び出すと、**フォーマット**GDI プリンター デバイス コンテキストを作成する関数は、適切なプリンター グラフィックス DLL が読み込まれているを確認します。 DLL および呼び出し、GDI が読み込まれますがない場合、 [ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver) DLL 内の関数。 ドライバーの再読み込みがない限り、関数は再度呼び出されません。

2.  次に、GDI がプリンター グラフィックス DLL を呼び出す[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)機能、ドライバーはインスタンスと戻り値のデバイスの特性、物理デバイスを作成できます。 GDI では、返される情報を使用して、デバイスのインスタンスの内部の説明を作成します。

3.  GDI を呼び出してグラフィックス DLL の[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)デバイス インスタンスへの GDI ハンドルを指定する関数。 グラフィックス DLL は、いくつかの入力としてこのハンドルを使用する必要があります、**への Eng**、GDI 描画エンジンによって提供されるコールバックをプレフィックスとして (を参照してください[GDI サポート サービス](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-support-services))。

4.  デバイスのインスタンス ハンドルを受け取ると、GDI グラフィックス DLL の呼び出しを作成し[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数では、描画、画面を設定し、物理デバイスを関連付けますインスタンス。

5.  ドライバーは、呼び出すことによってデバイスのインスタンスの描画サーフェイスを作成できます[ **EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)します。 または、描画サーフェイスがデバイス管理されている場合は、ドライバーを呼び出せる[ **EngCreateDeviceSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)します。

6.  場合**EngCreateBitmap**物理ページ全体を格納するのに十分な大きさのビットマップを指定することはできません、ドライバーでは、ページが縞模様をサポートしている場合と[ **EngMarkBandingSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface)できますGDI 縞模様が採用することを通知するために呼び出されます。

7.  最後に、 [ **EngAssociateSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface) GDI に作成した画面を指定したデバイスのインスタンスに関連付けると、GDI がどのドライバーが指定したグラフィックス DDI 図面を把握できるようにするために呼び出す必要があります関数 (あれば) この特定のサーフェイスを描画するときを呼び出す必要がありますに。

この時点では、描画サーフェイスが作成されているし、レンダリングを開始できます。 GDI が呼び出す関数は、有効では縞模様かどうかによって異なります。

### <a name="banding-in-use"></a>バンドの使用

縞模様を使用する場合に表示されるドキュメントごとに、GDI プリンター グラフィックス DLL では、次の関数を呼び出し。

[**DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)物理ページごとに { [ **DrvStartPage**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)
[**DrvStartBanding** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)物理ページに各バンド パス { [ *DrvQueryPerBandInfo* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)レンダリング操作[ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)このバンドのラスター データを送信し、[次へ] の band と再利用する画面をオフ}} [ **DrvEndDoc**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)
### <a href="" id="banding-not-in-use"></a> 使用中でない縞模様

縞模様を使用しない場合に表示されるドキュメントごとに、GDI プリンター グラフィックス DLL では、次の関数を呼び出し。

[**DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)物理ページごとに[ **DrvStartPage** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)レンダリング操作[ *DrvSendPage* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)/ラスター データ ページの送信/} [ **DrvEndDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)は例外です[ *DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)、これらプリンター グラフィックスにプリンターのハードウェア制御シーケンスを送信する DLL を許可する関数が目的として (呼び出して[ **EngWritePrinter**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter))、および必要な内部操作を実行するには初期化するか、ドキュメント、ページ、またはバンドの処理を完了します。

プリンター グラフィックス DLL は、プリンターに適切なタイミングで描画された画像 (つまり、描画サーフェイスの内容) を送信する責任を負います (呼び出して**EngWritePrinter**)、次のように。

-   GDI が管理またはデバイス管理のビットマップ サーフェイス

    描画サーフェイスは、GDI が指定した、またはドライバーによって提供されるビットマップです。 プリンター グラフィックス DLL は、いくつかの描画の関数をフック可能性があります (を参照してください[画面ネゴシエーション](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation))。 ページの縞模様が、使用中の場合、 [ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)関数が画面の内容を描画を送信する必要があります。 使用して、縞模様でない場合、 [ *DrvSendPage* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)関数は描画サーフェスの内容を送信する必要があります。

-   デバイスで管理されたベクター サーフェイス

    描画サーフェイスは、デバイス内です。 プリンター グラフィックス DLL は、すべての描画機能をフック (を参照してください[画面ネゴシエーション](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation))、およびこれらの関数は、レンダリング操作中にプリンターに画像データを送信します。 縞模様のページは使用されません。

可能性のあるかかる場合グラフィックス DLL がありますを実行する 5 秒以上、プリンターによって提供されるグラフィックス DDI が機能するが予想される場合を呼び出すコードを含める必要があります[ **EngCheckAbort** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcheckabort)少なくとも印刷ジョブを終了する必要があるかどうかに表示する 5 秒ごとにします。

GDI の後に呼び出す[ **DrvEndDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)呼び出しでドキュメントが完全に表示されることを示す[ **DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)します。 場合[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)と呼ばれる[ **EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)、し**DrvDisableSurface**呼び出す必要があります[ **EngDeleteSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesurface)します。

GDI の呼び出しをプリンター グラフィックス DLL の[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)関数アプリケーションを呼び出す**とき**します。

アプリケーションを呼び出す場合**印刷**GDI、ドキュメントの印刷時に関数を新しいデバイス コンテキストを作成し、プリンター グラフィックス DLL の呼び出し[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)新しいコンテキストの関数。 GDI の呼び出し後、 [ **DrvResetPDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)関数は、グラフィックスの DLL は古いものからの情報で新しいコンテキストを更新できるようにします。 次に、 [ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)と[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)後に、古いコンテキストに対して呼び出される[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)新しいコンテキスト。 最後に、GDI が呼び出す[ **DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)し、新しいページにレンダリングが再開されます。

GDI 呼び出し[ **DrvDisableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)プリンター グラフィックス DLL をアンロードする前にします。

プリンターのハードウェアでは、GDI 描画関数でサポートされていない描画操作をサポートする場合、プリンター グラフィックス DLL を提供できます、 [ **DrvDrawEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)関数。

DLL が提供できるプリンター グラフィックス、 [ **DrvEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape) GDI 関数では実行できない描画または図面以外の操作をサポートする必要がある場合に機能します。 たとえば、 [Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) PostScript 挿入ポイントをサポートするために、エスケープを使用します。 または、アプリケーションは、ファックスの電話番号を取得する必要があります。 **DrvEscape**でサポートされる操作を示す関数を使用しても、 **DrvDrawEscape**関数。

**フォーマット**、**印刷**、および**とき**Microsoft Windows SDK ドキュメントに記載されています。

 

 




