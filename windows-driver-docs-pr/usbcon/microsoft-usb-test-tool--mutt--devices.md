---
Description: Microsoft USB Test Tool (MUTT) には、USB のハードウェアは Microsoft USB ドライバー スタックとの相互運用性をテストするためのデバイスのコレクションです。
title: Microsoft USB Test Tool (MUTT) デバイスの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce3a2d372588aa0682e79e0e20fd0ed1fe93459
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717005"
---
# <a name="overview-of-microsoft-usb-test-tool-mutt-devices"></a>Microsoft USB Test Tool (MUTT) デバイスの概要


**概要**

-   MUTT デバイスの説明
-   このセクションに記載の製造元は販売 MUTT ハードウェアのボードの相互運用性のテストを実行するために必要です。
-   [![mutt ソフトウェア パッケージをダウンロード](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)MUTT ソフトウェア パッケージ、テスト ツールの最新バージョンを取得します。

Microsoft USB Test Tool (MUTT) には、USB のハードウェアは Microsoft USB ドライバー スタックとの相互運用性をテストするためのデバイスのコレクションです。 このセクションでは、MUTT デバイス、テスト、デバイスを使用して実行でき、コント ローラー、ハブ、デバイス、トポロジの提案し、BIOS および UEFI テストのさまざまな種類の概要を提供します。

MUTT デバイスと通信、MUTT ソフトウェア パッケージが必要です。 このパッケージには、いくつかのテスト ツールとハードウェア テスト エンジニア テスト、USB コント ローラーや Microsoft USB ドライバー スタックとハブの相互運用性のためのドライバーが含まれています。 テスト ツールは、USB ホスト コント ローラーのソフトウェア、ハードウェア (ファームウェアを含む) およびホスト コント ローラーとデバイスの間にインストールされているいずれかの USB ハブを検証します。

## <a name="how-to-get-mutt-devices"></a>MUTT デバイスを取得する方法


<a href="" id="mutt"></a>MUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-pack"></a>MUTT パック  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="supermutt"></a>SuperMUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

[Pactron](http://pactronstore.com/products/supermutt.mdl)

<a href="" id="supermutt-pack"></a>SuperMUTT パック  
[ラボを使用して](https://go.microsoft.com/fwlink/p/?linkid=618285)

<a href="" id="dr-mutt"></a>DR の MUTT  
[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

<a href="" id="mutt-connex-c"></a>USB タイプ C ConnEx [MCCI](https://go.microsoft.com/fwlink/p/?LinkId=733488)

[JJG テクノロジ]( https://go.microsoft.com/fwlink/p/?linkid=618287)

## <a name="mutt"></a>MUTT


-   CY3681 EZ USB FX2 Development Kit (キプロス FX2) のデザインに基づいています。
-   互換性のある**FX2**高速一括、アイソクロナスのコントロールへのフル スピード転送などの機能は、エンドポイントを中断します。
-   USB 2.0 デバイスからのトラフィックをシミュレートします。

    ![mutt デバイス](images/fig1-mutt-device.png)

## <a name="mutt-pack"></a>MUTT パック


MUTT パックは、USB 2.0 ハブおよびハブを制御し、ダウン ストリーム デバイスとして動作 FX2 デバイスの組み合わせです。

-   キプロス ハブとキプロス FX2 のデザインに基づいています。
-   ハブの機能です。 これは、マルチ TT またはシングル TT 高速ハブ; として動作できます。過電流をシミュレートします。
-   オンまたはオフになっていることができますをダウン ストリームのポートを公開します。
-   USB 2.0 ハブの動作をシミュレートします。
-   自己供給またはバス供給のモードで動作できます。

    ![mutt パック デバイス](images/fig2-muttpackdevice.png)

MUTT パックには、2 つの USB コネクタがあります。 標準の B コネクタは、ホスト システムに MUTT パック接続に使用されます。 Standard コネクタは、MUTT パックに埋め込みのハブのダウン ストリームとその他のデバイスは、(このドキュメントで後述します) をテストするために使用できます。

![mutt パックのコネクタ](images/fig3-muttpackconnectors.png)

### <a name="how-to-power-the-mutt-pack"></a>MUTT パックを強化する方法について

MUTT パックが小規模のジャンパー線を使用して (図 3 参照) 自己給電とバス供給のモードを切り替えます。 バス供給のモードで、ホスト システムの USB バスは、MUTT パックで強化できます。 自己供給型のモードで MUTT パックは、外部の 5 v の電源アダプターを使用した電源します。

![mutt パックの電源のフローチャート](images/fig4-muttpackpoweringflowchart.png)

MUTT パックを強化するのに方法について確認するのにには、次のフロー チャートを使用します。

**注**  power ジャンパーせず、MUTT パックを使用しないでください。

 

![不適切な使用方法](images/fig5-muttpackincorrectusage.png)

このイメージは、MUTT パックのホスト システムの USB バスで電源のジャンパーを使用する方法を示します。

![mutt パック バスの電源](images/fig6-muttpackbuspowered.png)

このイメージは、外部電源アダプターを使用した、MUTT パックの電源のジャンパーを使用する方法を示します。

![電源セルフ mutt パック](images/fig7-muttpackselfpowered.png)

**注**  ジャンパー MUTT パックに変更している場合、既存の電源アダプターとホスト システムにケーブルを切断します。

 

## <a name="supermutt"></a>SuperMUTT


-   FX3 EZ USB FX3 のデザインに基づいています。
-   一括ストリーム機能などの SuperSpeed 機能を実装します。
-   USB 3.0 デバイスのトラフィックをシミュレートします。
-   注: このデバイスは、低速度での操作をサポートしません。

    ![supermutt](images/fig8-supermutt.png)

## <a name="supermutt-pack"></a>SuperMUTT パック


SuperMUTT パックは、いずれかで 2 つのデバイスです。 USB 3.0 ハブ キプロス FX2 デバイス ダウン ストリームにすることをお勧めします。 デバイスは、ハブを制御し、ダウン ストリーム デバイスとしても機能します。 SuperMUTT パックは、USB 3.0 ハブの動作をシミュレートします。

**注**  ダウン ストリーム デバイスは、2.0 デバイス、USB 3.0 デバイスではありません。

 

![supermutt パック](images/supermuttpack.png)

## <a name="dr-mutt"></a>DR の MUTT


テスト対象のデバイスのモードのホストをテストするときに、DR MUTT が SuperMutt のように機能しますも、テスト対象のデバイスの機能モードをテストするホスト モードに切り替えることができます。

## <a name="usb-type-c-connex"></a>USB タイプ C ConnEx


USB タイプ C 接続 Exerciser (USB 型 C ConnEx) では、USB 型-C# の相互運用性シナリオを自動化する 4 対 1 のスイッチのあるカスタム シールドです。 Arduino マイクロ コント ローラーとして使用するシールドは設計されています。 詳細については、次を参照してください。 [USB 型 C ConnEx でシステムをテスト USB 型-c](test-usb-type-c-systems-with-mutt-connex-c.md)します。

![USB タイプ C ConnEx](images/connexc-side.jpg)

## <a name="related-topics"></a>関連トピック
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Windows での USB ハードウェア、ドライバー、およびアプリのテスト](usb-driver-testing-guide.md)  




