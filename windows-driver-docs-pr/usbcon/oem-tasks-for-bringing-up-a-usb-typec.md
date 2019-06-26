---
Description: Windows は、USB 型-c コネクタおよびタスク C-USB 型システムを構築する Oem のサポートします。
title: USB Type-C コネクタに対する Windows サポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4cca50437de9aadbcd65be59bfbdf75042e1fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368831"
---
# <a name="windows-support-for-usb-type-c-connectors"></a>USB Type-C コネクタに対する Windows サポート

このトピックでは、USB 型-C# のコネクタの使用の Windows 10 システムを構築し、ビルボードのデバイスを充電高速化、電源の配信、デュアル ロール、代替モード、およびエラーの通知を許可する OS 機能を活用する Oem 向けです。

従来の USB 接続では、各端での USB A と B の USB コネクタの使用、ケーブルを使用します。 A の USB コネクタは常に、ホスト側に接続し、USB B コネクタが関数の側では、デバイス (電話) または (マウス、キーボード) の周辺機器を接続します。 これらのコネクタを使用するは、ホスト; 関数にのみ接続できます。別のホストまたは別の関数を関数にホストことはありません。 ホストは、電源のソース プロバイダーであり、関数が、ホストから電力を消費します。

従来の構成には、いくつかのシナリオが制限されます。 たとえば、周辺機器に接続しようとすると、モバイル デバイスの場合デバイスする必要がありますホストとして機能し、接続されたデバイスに電源を配信します。

USB で導入された、USB 型-c コネクタの場合、USB 3.1 仕様で定義されている、それらの制限事項に対処します。 Windows 10 には、これらの機能のネイティブ サポートが導入されています。

![usb コネクタの比較](images/typecccomp.jpg)


## <a name="feature-summary"></a>機能の概要

- 高速化充電まで台の 100 w 電源の配信を使用した USB 型-C. 経由では、します。
- USB ホストとの USB デバイスの両方の 1 つのコネクタ。
- USB ホストまたはデバイスをサポートする USB ロールを切り替えることができます。
- ソーシングと電源のシンクの間で電源のロールを切り替えることができます。
- USB タイプ-C. 経由でディスプレイ ポート等と雷などの他のプロトコルをサポートしています
- 別のモードのエラー通知を提供する USB ビルボード デバイス クラスについて説明します。

**公式の仕様**

[USB 3.1 と USB 型-C# の仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)

[USB 電源配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)

[ビルボード デバイス仕様](https://go.microsoft.com/fwlink/p/?linkid=620207)

[UCSI 仕様](https://go.microsoft.com/fwlink/p/?LinkId=703713)

## <a name="hardware-design"></a>ハードウェアの設計
USB タイプ-c コネクタは、元に戻すことと対称です。

![USB タイプ-c 対称ケーブル](images/usb-type-c.png)

主なコンポーネントが: USB 型-c コネクタ、そのポート、またはコネクタの [cc] ピン留めするロジックを管理する PD コント ローラー。 通常、このようなシステムには、ホストから関数への USB ロールを切り替えることができますをデュアル ロール コント ローラーがあります。 USB 経由で送信されるビデオ信号を可能にする表示出力モジュールがあります。 必要に応じて BC1.2 充電器の検出をサポートできます。

- [USB タイプ-c システムのハードウェアの設計](architecture--usb-type-c-in-a-windows-system.md)
- [埋め込みコント ローラーを備えた USB 型-c システムのハードウェアの設計](ucsi.md)

設計とハードウェアの最小要件、Windows ハードウェア互換性プログラムの要件およびそれらの要件に構築されたその他の推奨事項を含め、USB のコンポーネントの開発に関する推奨事項を検討してください。
[USB ハードウェア コンポーネントのガイドライン](https://docs.microsoft.com/windows-hardware/design/component-guidelines/universal-serial-bus--usb-)

## <a name="choose-a-driver-model"></a>ドライバー モデルを選択します。

このフロー チャートを使用すると、USB C 型システムのソリューションを判断できます。 
![ドライバー](images/drivers-c.png)

|場合、システム.| お勧めしています.|
|---|---|
|PD ステート マシンを実装していません |UcmTcpciCx クラスの拡張機能に、クライアント ドライバーを記述します。 <p>[USB タイプ-c ポート コント ローラー ドライバーを作成します。](write-a-usb-type-c-port-controller-driver.md)</p>|
|実装 PD ハードウェアまたはファームウェア内のマシンの状態にあり、ACPI 経由での USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) のサポート| インボックス ドライバー、UcmUcsiCx.sys と UcmUcsiAcpiClient.sys、Microsoft を読み込みます。 <p>参照してください[UCSI ドライバー](ucsi.md)します。</p>|
|ハードウェアまたはファームウェアが、いずれかの実装 PD ステート マシンは UCSI をサポートしていないか、サポート UCSI では、ACPI 以外のトランスポートが必要です。|UcmCx クラスの拡張機能用のクライアント ドライバーを記述します。<p>[USB タイプ-c コネクタのドライバーを作成します。](bring-up-a-usb-type-c-connector-on-a-windows-system.md)</p><p>[Write a USB Type-C Policy Manager client driver (USB Type-C ポリシー マネージャー クライアント ドライバーの作成)](policy-manager-client.md)</p>|
|実装 UCSI ACPI 以外のトランスポートが必要です。|UcmUcsiCx クラスの拡張機能に、クライアント ドライバーを記述します。<p>使用[こちらのサンプル テンプレート](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)ハードウェアを使用するトランスポートに基づいてに変更します。</P><p>[Write a UCSI client driver (UCSI クライアント ドライバーの作成)](write-a-ucsi-driver.md)</P>|


## <a name="bring-up-drivers"></a>ドライバーを起動します。

- USB 機能ドライバー bring アップは USB 機能モードをサポートするために必要な。 マイクロ B の USB コネクタ用に USB 機能ドライバーが既に実装されている場合について説明します、適切なコネクタ USB 型-C# で作業を続行する USB 機能ドライバーを ACPI テーブル。 

    詳細については、次を参照してください。 [USB 機能ドライバーの作成について](developing-windows-drivers-for-usb-function-controllers.md)します。

- USB の役割の交代 bring ドライバー - アップはのみホストと関数の両方の役割を想定するロールのデュアル コント ローラーを持つデバイスに必要です。 ロールの切り替えの USB ドライバーの表示時に、Microsoft のインボックス USB 役割の交代ドライバーを有効にする ACPI テーブルを変更する必要があります。 

    詳細については、次を参照してください。、[ロール切り替えの USB ドライバーを取り込むためのガイダンス](dual-role-controller-bringup-for-a-usb-type-c-system.md)します。

- USB コネクタ マネージャー ドライバーは、Windows システムの種類 C の USB ポートを管理する必要があります。 USB コネクタ マネージャー ドライバー用の bring アップ タスクは、型-C# の USB ポートの選択したドライバーによって異なります。Microsoft のインボックス UCSI (UcmUcsiCx.sys および UcmUcsiAcpiClient.sys) ドライバー、UcmCx クライアント ドライバーでは、または UcmTcpciCx クライアント ドライバー。 詳細については、C-USB 型システムに最適なソリューションを選択する方法を説明する前のセクションでリンクを参照してください。


## <a name="test"></a>テスト
さまざまな機能を実行し、システムと USB 型-C# のコネクタを公開しているデバイスでテストを強調します。

[USB タイプ C ConnEx で USB 型-c システムをテストする](test-usb-type-c-systems-with-mutt-connex-c.md)-Windows 10 用 Windows ハードウェア ラボ キット (HLK) に含まれる実行 USB テストします。
> C ~ A ケーブルでテストを実行 USB 関数 HLK (検索**Windows USB デバイス**HLK で 

認定とコンプライアンスへの参加 Power 配信および USB 型-C コンプライアンス ワーク ショップ標準化団体によってホストされています。
 
## <a name="see-also"></a>関連項目


-   [よく寄せられる質問:Windows システム上の C-USB 型コネクタ](faq--usb-type-c-connector-on-a-windows-system.md)
-   [UI でのメッセージをトラブルシューティングします。](https://go.microsoft.com/fwlink/?LinkId=526894) 

 




