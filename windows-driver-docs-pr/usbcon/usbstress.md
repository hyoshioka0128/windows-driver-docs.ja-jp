---
Description: USBStress がユーザー モード アプリケーション (usbstress.exe) と、カーネル モード ドライバーのドライバーのインストール パッケージの組み合わせ usbstress.sys します。
title: USBStress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a321240256a9550d82e9b72ef96eaf8d0cd33cfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342135"
---
# <a name="usbstress"></a>USBStress


USBStress がユーザー モード アプリケーション (usbstress.exe) と、カーネル モード ドライバーのドライバーのインストール パッケージの組み合わせ usbstress.sys します。

これらのファイルに含まれる、 [MUTT ソフトウェア パッケージ](https://msdn.microsoft.com/windows/hardware/jj590752)します。

## <a name="usbstress"></a>USBStress


USBStress には、全体の USB ドライバー スタックと USB の一般的な親ドライバー (Usbccgp.sys) とコント ローラーとそのアップ ストリーム ハブに重点を置いてテストのセットです。 USBStress はランダムにテストを選択し、接続されているテスト デバイスを構成します。 テストのランダムな性質 USBStress テストの組み合わせを許可する 24 時間以内に実行する必要がありますをお勧めします。

ツールは、コントロール、さまざまな転送の長さにし、テスト デバイスからの一括、アイソクロナス、データ転送を実行します。 SuperMUTT デバイスの場合は、USBTCD は、一括エンドポイントでサポートされているストリームにデータを転送します。

USBStress ドライバーが大きく自己駆動型には、ドライバーとアプリケーションではなく、ほとんどの I/O 要求の生成は、します。 ドライバーは、タイマーおよび作業項目を使用して、I/O を生成し、その他の操作を実行します。 ドライバーは、そのテストを実行する必要があるかどうかを確認するレジストリを確認します。 外部プログラムは、そのレジストリ キーを設定します。 このドライバーの目標に競合状態と同期の問題を除去するためのさまざまな操作の間でできるだけ多くの同時実行を作成します。

この一覧は、USBStress を実行するテストをまとめたものです。

-   選択的にリモート ウェイク アップを中断します。
-   一括、割り込み、アイソクロナス エンドポイントとキャンセルの同時読み取り/書き込み要求。
-   同時実行の文字列は、要求とキャンセルを転送します。
-   同時実行一括エンドポイントおよびキャンセルのパイプを中止します。
-   突然削除と再列挙にランダムなリセットします。
-   突然削除と再列挙再列挙が失敗するランダムなリセットします。
-   使用可能な代替インターフェイスをランダムに選択します。
-   すべての n 番目の制御の移動を停止するデバイスにランダムに指示します。
-   MUTT をランダムに指示する VBUS をダウン ストリームの公開ポートから切断する (接続されている) 場合をパックします。
-   MUTT をランダムに指示するダウン ストリームの公開ポートで、過電流の状態をシミュレートするために (場合接続) をパックします。
-   MUTT をランダムに指示する、ハードウェアのハブのリセットを実行する (接続されている) 場合をパックします。

MUTT デバイスの usbstress.sys ドライバーをインストールすると MuttUtil を使用して、`-UpdateDriver `オプション。

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbstress.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBSTRESS
Return value: 1
```

## <a name="related-topics"></a>関連トピック
[USB テスト ツール](usb-test-tools.md)  
[MUTT ソフトウェア パッケージのツール](mutt-software-package.md)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



