---
Description: USBStress とは、ユーザーモードアプリケーション (usbstress) とカーネルモードドライバーのドライバーインストールパッケージ (usbstress) の組み合わせです。
title: USBStress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb6c07c9e5ea4b366b783136f20b5126958fecaa
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995436"
---
# <a name="usbstress"></a>USBStress


USBStress とは、ユーザーモードアプリケーション (usbstress) とカーネルモードドライバーのドライバーインストールパッケージ (usbstress) の組み合わせです。

これらのファイルは、 [MUTT ソフトウェアパッケージ](https://docs.microsoft.com/windows-hardware/drivers/usbcon/mutt-software-package)に含まれています。

## <a name="usbstress"></a>USBStress


USBStress は、USB ドライバースタック全体と USB 汎用親ドライバー (Usbccgp)、およびコントローラーとそのアップストリームハブに焦点を合わせた一連のテストです。 USBStress は、ランダムにテストを選択し、接続されているテストデバイスを構成します。 テストにはランダムな性質があるため、より多くのテストの組み合わせを許可するには、Usb 負荷を24時間の期間にわたって実行することをお勧めします。

このツールでは、テストデバイスとの間でさまざまな転送長の制御、一括、アイソクロナス、データ転送が実行されます。 スーパー Mutt デバイスの場合、USBTCD は、一括エンドポイントでサポートされているストリームにデータを転送します。

USBStress ドライバーは主に自己駆動型です。つまり、ほとんどの i/o 要求は、アプリケーションではなくドライバーによって生成されます。 ドライバーは、タイマーと作業項目を使用して、i/o を生成し、その他の操作を実行します。 ドライバーは、テストを実行する必要があるかどうかを判断するために、レジストリを確認します。 外部プログラムによってそのレジストリキーが設定されます。 このドライバーの目的は、競合状態と同期の問題をフラッシュするために、さまざまな操作の間にできるだけ多くの同時実行を作成することです。

この一覧には、USBStress によって実行されるテストの概要が示されます。

-   リモートウェイクアップを使用したセレクティブサスペンド。
-   一括、割り込み、およびアイソクロナスのエンドポイントとキャンセルに対する同時読み取り/書き込み要求。
-   同時実行文字列の転送要求とキャンセル。
-   一括エンドポイントとキャンセルの同時実行中止パイプ。
-   ランダムリセットによる突然の削除と再列挙。
-   ランダムにリセットすると、再列挙が削除されて再列挙され、失敗します。
-   使用可能な代替インターフェイスをランダムに選択します。
-   N 番目のコントロール転送ごとに停止するようにデバイスにランダムに指示します。
-   MUTT パック (接続されている場合) をランダムに指示して、公開されたダウンストリームポートから VBUS を切断します。
-   MUTT パック (接続されている場合) をランダムに指示して、公開されている下流ポートでのオーバーオーバー状態をシミュレートします。
-   MUTT パック (接続されている場合) をランダムに指示して、ハブでハードウェアのリセットを実行します。

MUTT デバイス用の usbstress ドライバーをインストールするには、次のオプションを`-UpdateDriver `指定してを使用します。

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbstress.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBSTRESS
Return value: 1
```

## <a name="related-topics"></a>関連トピック
[USB テストツール](usb-test-tools.md)  
[MUTT ソフトウェアパッケージのツール](mutt-software-package.md)  
[Microsoft USB テストツール (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



