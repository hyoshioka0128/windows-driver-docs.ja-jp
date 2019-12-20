---
Description: Microsoft USB テストツール (MUTT) は、Microsoft USB ドライバースタックと USB ハードウェアの相互運用性をテストするためのデバイスのコレクションです。
title: Microsoft USB テスト ツール (MUTT) デバイスの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7fe0f408bcb495299b43ece8b53999b1750e36
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210638"
---
# <a name="overview-of-microsoft-usb-test-tool-mutt-devices"></a>Microsoft USB テスト ツール (MUTT) デバイスの概要


**要約**

-   MUTT デバイスの説明
-   このセクションに記載されている製造元は、相互運用性テストの実行に必要な MUTT ハードウェアボードを販売しています。
-   mutt ソフトウェアパッケージをダウンロードして、最新バージョンのテストツールを入手[![](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)ます。

Microsoft USB テストツール (MUTT) は、Microsoft USB ドライバースタックと USB ハードウェアの相互運用性をテストするためのデバイスのコレクションです。 このセクションでは、さまざまな種類の MUTT デバイスの概要、デバイスを使用して実行できるテスト、コントローラー、ハブ、デバイス、BIOS/UEFI テストのトポロジを提案します。

MUTT デバイスと通信するには、MUTT ソフトウェアパッケージが必要です。 このパッケージには、ハードウェアテストエンジニアが Microsoft USB ドライバースタックと USB コントローラーまたはハブの相互運用性をテストできるようにするテストツールとドライバーがいくつか含まれています。 テストツールは、USB ホストコントローラーソフトウェア、ハードウェア (ファームウェアを含む)、およびホストコントローラーとデバイスの間にインストールされているすべての USB ハブを検証します。

## <a name="how-to-get-mutt-devices"></a>MUTT デバイスを入手する方法


<a href="" id="mutt"></a>MUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-pack"></a>MUTT パック  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="supermutt"></a>SuperMUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

[Pactron](https://pactronstore.com/products/supermutt.mdl)

<a href="" id="supermutt-pack"></a>SuperMUTT パック  
[ラボ経由](https://go.microsoft.com/fwlink/p/?linkid=618285)

<a href="" id="dr-mutt"></a>DR MUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-connex-c"></a>USB タイプ-C ConnEx [Mcci](https://go.microsoft.com/fwlink/p/?LinkId=733488)

[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

## <a name="mutt"></a>MUTT


-   CY3681 EZ-USB FX2 Development Kit (キプロス FX2) の設計に基づいています。
-   高速で、一括、アイソクロナス、制御、割り込みエンドポイントへの高速転送などの**FX2**機能と互換性があります。
-   USB 2.0 デバイスからのトラフィックをシミュレートします。

    ![mutt デバイス](images/fig1-mutt-device.png)

## <a name="mutt-pack"></a>MUTT パック


MUTT パックは、USB 2.0 ハブと FX2 デバイスを組み合わせたもので、ハブを制御し、ダウンストリームデバイスとして機能します。

-   キプロス Hub とキプロス FX2 の設計に基づいています。
-   ハブの機能。 これは、マルチ TT または単一 TT の高速ハブとして動作します。過電流をシミュレートします。
-   オンまたはオフにできるダウンストリームポートを公開します。
-   USB 2.0 hub の動作をシミュレートします。
-   は、自己給電モードまたはバス電源モードで動作できます。

    ![mutt パックデバイス](images/fig2-muttpackdevice.png)

MUTT パックには、2つの USB コネクタがあります。 標準 B コネクタは、の MUTT パックをホストシステムに接続するために使用されます。 標準コネクタは、MUTT パックの埋め込みハブの下流にあり、追加のデバイステストに使用できます (このドキュメントで後述します)。

![mutt パックコネクタ](images/fig3-muttpackconnectors.png)

### <a name="how-to-power-the-mutt-pack"></a>MUTT パックの電源をオンにする方法

MUTT パックは、小さなジャンパー (図3を参照) を使用して、自己給電モードとバス電源モードを切り替えます。 バス電源モードでは、ホストシステムの USB バスによって MUTT パックが作動します。 自己電源モードでは、MUTT パックに外部の5V 電源アダプターが搭載されています。

![mutt パックの電源フローチャート](images/fig4-muttpackpoweringflowchart.png)

次のフローチャートを使用して、MUTT パックの電源を入れます。

電源ジャンパーを使用せずに MUTT パックを使用しない  に**注意**してください。

 

![不適切な使用法](images/fig5-muttpackincorrectusage.png)

このイメージは、ジャンパーを使用して、ホストシステムの USB バスで MUTT パックを電源に入れる方法を示しています。

![mutt pack バス電源](images/fig6-muttpackbuspowered.png)

このイメージは、ジャンパーを使用して、外付け電源アダプターで MUTT パックを電源に入れる方法を示しています。

![mutt パックのセルフパワー](images/fig7-muttpackselfpowered.png)

MUTT パックのジャンパーを変更するときは、既存の電源アダプターとケーブルをホストシステムに**接続  ます**。

 

## <a name="supermutt"></a>SuperMUTT


-   FX3 EZ-USB FX3 の設計に基づいています。
-   一括ストリーム機能などの SuperSpeed 機能を実装します。
-   USB 3.0 デバイストラフィックをシミュレートします。
-   注: このデバイスは、低速での操作をサポートしていません。

    ![supermutt](images/fig8-supermutt.png)

## <a name="supermutt-pack"></a>SuperMUTT パック


SuperMUTT パックは1つのデバイスです。 これは、キプロス FX2 device 下流の USB 3.0 ハブです。 デバイスはハブを制御し、ダウンストリームデバイスとしても機能します。 SuperMUTT パックは、USB 3.0 hub の動作をシミュレートします。

ダウンストリームデバイスは2.0 デバイスであり、USB 3.0 デバイスではない  に**注意**してください。

 

![supermutt パック](images/supermuttpack.png)

## <a name="dr-mutt"></a>DR MUTT


DR MUTT は、テスト対象のデバイスのホストモードをテストするときにスーパー MUTT のように動作しますが、ホストモードに切り替えて、テスト対象のデバイスの関数モードをテストすることもできます。

## <a name="usb-type-c-connex"></a>USB タイプ-C ConnEx


Usb タイプ c 接続 Exerciser (USB タイプ-C 接続 Ex) は、USB タイプ C の相互運用性のシナリオを自動化するための4対1のスイッチを備えたカスタムシールドです。 シールドは、マイクロコントローラーとして Arduino と連携するように設計されています。 詳細については、「 [Usb タイプを使用して c システムをテストする-c ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)」を参照してください。

![USB タイプ-C ConnEx](images/connexc-side.jpg)

## <a name="related-topics"></a>関連トピック
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Windows での USB ハードウェア、ドライバー、およびアプリのテスト](usb-driver-testing-guide.md)  




