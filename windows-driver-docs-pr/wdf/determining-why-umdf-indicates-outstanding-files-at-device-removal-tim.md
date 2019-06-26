---
title: UMDF は、デバイス削除時に未処理のファイルを示します
description: Wudfext.dll を使用して、UMDF にある未処理のファイルがデバイスを削除したときに示す理由を判断する方法について説明します。
ms.assetid: 9a8b3b69-1192-40c1-895b-4abfc01c1ca7
keywords:
- WDK UMDF のシナリオをデバッグするには、UMDF 示します未処理のファイルがデバイスの削除時に
- UMDF WDK、デバッグ シナリオでは、UMDF にデバイスの削除時に未処理のファイルことを示します
- UMDF WDK、UMDF にデバイスの削除時に未処理のファイルことを示します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f514950f5076da63032dd47b30e3c3703981bec2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377428"
---
# <a name="determining-why-umdf-indicates-outstanding-files-at-device-removal-time"></a>デバイスの取り外し時に UMDF が未処理ファイルを示す理由の特定


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) のバージョン 1 または 2 ドライバーと組み合わせて Wudfext.dll デバッガー拡張機能を使用して UMDF がデバイスを削除したときに未処理のファイルが認識はことを示す理由を判断する方法について説明します。

UMDF バージョン 1、wudfext.dll で実装された拡張機能のコマンドを使用します。 UMDF バージョン 2 以降、wdfkd.dll で実装された拡張機能のコマンドを使用します。

UMDF が未処理のファイルを示す理由を確認するのには、次の手順を使用します。

1.  使用[ **! wudfext.umdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umdevstack) (UMDF 1) または[ **! wdfkd.wdfumdevstack** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)デバイス スタックをダンプする (UMDF 2)。 ダンプには、未処理の UMDF 内 stack ファイル (つまり、アプリケーションによって、または別のスタック内のドライバーによって作成されたファイル オブジェクトではなく、スタック内のドライバーが作成されたファイル オブジェクト) が含まれています。

2.  スタック内のファイルごとに、実行[ **! wudfext.umfile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umfile) (UMDF 1) または[ **! wdfkd.wdfumfile** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)ファイルに関する情報を取得する (UMDF 2).

    出力には、保留になっている Irp の一覧が含まれています。

3.  理由を判断各 IRP 未処理を使用して[ **! wudfext.umirp** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirp) (UMDF 1) または[ **! wdfkd.wdfumirp** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)情報を取得する (UMDF 2)IRP について。

    それぞれの出力から[ **! wudfext.umirp** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirp)または[ **! wdfkd.wdfumirp**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp):

    -   IRP が完了したかどうかを判断します。
    -   ドライバーで明示的または暗黙的にオブジェクト ツリーで、ドライバーが作成した要求が削除されないかどうかを決定します。

 

 





