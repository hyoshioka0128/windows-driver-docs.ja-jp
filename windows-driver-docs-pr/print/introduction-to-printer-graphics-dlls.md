---
title: プリンター グラフィックス Dll の概要
description: プリンター グラフィックス Dll の概要
ms.assetid: 3f7ce476-6bef-4a80-ae2a-2a63e891dda1
keywords:
- プリンター グラフィックス DLL の WDK プリンター グラフィックス DLL について
- プリンター グラフィックス DLL についての DLL の WDK プリンターのグラフィック
- グラフィックス DLL WDK プリンター
- プリンター グラフィックス DLL WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 846d52929fa96f14d74b882d816c454a97f4fef7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558428"
---
# <a name="introduction-to-printer-graphics-dlls"></a>プリンター グラフィックス Dll の概要


プリンター グラフィックス Dll Drv プレフィックス付きのグラフィックスに記載されている DDI 関数を実装する[グラフィックス DDI を使用して](https://msdn.microsoft.com/library/windows/hardware/ff570139)します。 これらの Dll では、次の 2 つの役割があります。

-   印刷ジョブを表示するのには、GDI を支援します。

    プリンター グラフィックス DLL できるグラフィックス DDI 描画関数を提供描画操作であり、デバイスに固有の方法で実行する必要があります、ため、GDI のレンダリング エンジンによって排他的処理することはできません。

-   スプーラーに表示されたデータ ストリームを配信します。

    プリンター グラフィックス Dll は、通常、生のデータ型の出力ストリームを生成します。

プリンター グラフィックス DLL を指定する必要がありますレンダリング アシスタンス量プリンターによっては、ハードウェアの描画の機能の種類に固有であり、次のシナリオが含まれています。

-   GDI レンダリング エンジンは GDI 管理画面を使用して表示する、すべてです。 グラフィックス DLL では、すべて DDI 描画機能は提供されません。

-   グラフィックス DLL 関数を提供一部のグラフィックス DDI 描画 GDI のレンダリング エンジンと連携して動作する GDI 管理画面を使用します。 グラフィックス DDI グラフィックス DLL によって提供される関数を描画できます必要に応じてコールバック、GDI レンダリング エンジンの[GDI サポート サービス](https://msdn.microsoft.com/library/windows/hardware/ff566714)します。

-   グラフィックスの DLL では、すべてのレンダリングはグラフィックス DDI を提供することで描画関数と、デバイス管理の画面を使用します。

たとえば、 [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) は GDI 管理画面を使用したり、一部のグラフィックス DDI を提供中に関数を描画するには、 [Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md)を使用して、画面のデバイスが管理します。

グラフィック ドライバーのレンダリングについての支援を提供する詳細については、次を参照してください。[画面型](https://msdn.microsoft.com/library/windows/hardware/ff569900)と[グラフィックス DDI を使用して](https://msdn.microsoft.com/library/windows/hardware/ff570139)します。

次の 2 つの図は、アプリケーションは、GDI を使用して印刷ジョブを作成するときに発生するデータ フローを示しています。 EMF の記録と再生は、これらの図に結合されます。

最初の図は、ユーザー モードのプリンター グラフィックス DLL を示します。

**注**   Windows Vista でプリンター グラフィックス Dll は、ユーザー モードでのみ実行できます。 詳細については、次を参照してください。[選択ユーザー モードまたはカーネル モード](choosing-user-mode-or-kernel-mode.md)します。

 

![ユーザー モードのプリンター グラフィックス dll を示す図](images/usrmdprt.png)

2 番目の図は、カーネル モード プリンター グラフィックス DLL を示しています。

![カーネル モード プリンター グラフィックス dll を使用して、印刷ジョブのデータ フロー](images/gdiprint.png)

出力形式 GDI からがの場合のこれらの注意事項ダイアグラムを*拡張メタファイル (EMF)*、EMF プリント プロセッサが再生 EMF レコードまでプリンター グラフィックス DLL がジョブを受信しません。 EMF のプリント プロセッサが非 EMF を出力形式を変更にも注意してください。

図では、完全ローカルの環境について説明します。 場合は、プリンターがサーバーに接続されて、EMF レコードは GDI レンダリング エンジン (GRE) のクライアントのコピーによって通常生成され、サーバーに送信されるローカル ファイルにスプールされ、します。 スプーラーのサーバーのコピーがファイルを読み取り、レコード、サーバーの EMF のプリント プロセッサに送信し、GRE のサーバーのコピーが、サーバーのプリンター グラフィックス DLL を呼び出します。

 

 




