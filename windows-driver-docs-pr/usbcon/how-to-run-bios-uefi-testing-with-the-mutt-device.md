---
Description: BIOS および UEFI テストには、USB ブートとオペレーティング システムのコント ローラーのハンドオフが検証します。
title: MUTT デバイスを使用した BIOS/UEFI のテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624a3ab4d1873b409dad699d68b2ea4232e1408e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366066"
---
# <a name="biosuefi-testing-with-the-mutt-devices"></a>MUTT デバイスを使用した BIOS/UEFI のテスト


BIOS および UEFI テストには、USB ブートとオペレーティング システムのコント ローラーのハンドオフが検証します。

## <a name="usb-boot-configurations"></a>USB ブート構成


USB 2.0 (EHCI) と、プライマリ USB メディアの種類 (USB 2.0 ボット、USB 3.0 のボットと USB 3.0 UASP、および USB の DVD) の各に USB 3.0 (xHCI) コント ローラーの両方でこれらのテストを実行します。

シナリオごとに、予期される結果では、次のイベントの 1 つです。

-   接続されているキーボードで構成モードを開始するユーザーは、ユーザーには、適切なキー シーケンスが入ると、(BIOS または UEFI の構成)。
-   キーの組み合わせが押されていない場合は、USB デバイスから起動します。

BIOS/UEFI が構成されていることを想定して USB から起動します。 認識される Windows ファイル システムでは、接続されている USB ストレージ デバイスの各を書式設定されているがします。

-   USB ブート シナリオ 1-USB 3.0 ハブ

    ![usb 3.0 ハブ](images/fig16-usb-bootbehind30hub.png)

-   USB ブート シナリオ 2-USB 2.0 ハブ

    ![usb 2.0 ハブ](images/fig17-usb-bootbehind20hub.png)

-   USB ブート シナリオ 3: ルート ポート

    ![ブート ルート ポート](images/fig18-usb-bootrootport.png)

## <a name="non-usb-boot-configurations"></a>非 USB ブート構成


このシナリオでかない USB 起動可能なメディアがシステムに接続されている、または USB から起動しない BIOS および UEFI が構成されていると見なされます。 接続された USB キーボードを使用して、構成モードに入る/マウスは、予想されるシナリオは、ここに記載されていません。

![usb コント ローラーのハンドオフ](images/fig19-usb-controllerhandoff.png)

このシナリオで予想される結果は、SuperMUTT パック MUTT パックが存在する機能と運用オペレーティング システムで起動し、標準の MUTT を実行しているテストの後です。 テスト デバイスが検証されると、システムは (S3、S4、) は、サポートされているシステム電源の状態の各操作を実行、各システムの再開後に、MUTT テスト デバイスは機能を維持するかを検証する必要があります。 再開の各イベント後に、MUTT テストを実行します。

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  



