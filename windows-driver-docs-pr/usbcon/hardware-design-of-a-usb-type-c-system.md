---
Description: ここでは、USB タイプ C システムの設計例をいくつか紹介します。
title: USB タイプ C システムのハードウェア設計
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1612bc64e8d0741183f850788c96b505e98a0e9e
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242999"
---
# <a name="hardware-design-usb-type-c-systems"></a>ハードウェア設計: USB タイプ-C システム


**最終更新日時**

-   2016 年 12 月

\[一部の情報はリリース前の製品に関する事項であり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。\]

ここでは、USB タイプ C システムの設計例をいくつか紹介します。

一般的な USB タイプ C システムには、次のコンポーネントがあります。

-   **USB デュアルロールコントローラー**は、ホストロールでも、機能/デバイス/周辺機器ロールでも動作できます。 このコンポーネントは、SoC に統合されています。
-   **バッテリ充電1.2 の検出**は、特定のソケットに統合されている可能性があります。 一部の SoC ベンダは、検出ロジックを実装する PMIC モジュールを提供し、他の開発者はソフトウェアに実装します。 Windows 10 Mobile では、これらすべてのオプションがサポートされています。 このコンポーネントの詳細については、SoC ベンダにお問い合わせください。
-   **「-C-PD Port controller** 」と入力すると、USB タイプ c コネクタの CC ピンが管理されます。 では、BMC エンコード/電力配信メッセージのデコードがサポートされています。 このコンポーネントは、通常、ほとんどのソケットに統合されていません。
-   **Mux**タイプ C ポートコントローラーによって検出された向きに応じて、コントローラー上のポートに USB ペアを SuperSpeed します。 Mux SuperSpeed のペアと、場合によっては、代替モードに入るときに他の場所 (通常は表示モジュール) の行を SBU します。
-   **Vbus/Vbus** source が必要です。 ほとんどの PMICs は VBus/Vbus コントロールを実装します。 詳細については、SoC/PMIC ベンダにお問い合わせください。

## <a href="" id="emb"></a>USB タイプ-C システム設計と埋め込みコントローラー


前の一覧のコンポーネントに加えて、USB タイプ C システムは、埋め込みコントローラーを持つことができます。 このインテリジェントなマイクロコントローラーは、システムのタイプ C および電力配信ポリシーマネージャーとして機能します。

次に、埋め込みコントローラーを備えた USB タイプ C システムの例を示します。

![usb タイプ-c 組み込みコントローラーデバイス用のハードウェア設計の例](images/type-c-hw1.png)

もう1つのビューを次に示します。

![usb タイプ-c 組み込みコントローラーデバイス用のハードウェア設計の例](images/type-c-hw1-1.png)

コントローラーが埋め込まれているシステムの場合は、USB タイプの C コネクタシステムソフトウェアインターフェイス (UCSI) 仕様を実装する、Microsoft が提供する組み込みのドライバー UcmUcsi を読み込みます。

[Ucsi ドライバー](ucsi.md)。 ドライバー用に読み込まれたデバイススタックの詳細については、「 [embedded コントローラーを備えたシステムの USB タイプをサポートする C コンポーネント](architecture--usb-type-c-in-a-windows-system.md#drivers)」を参照してください。


非 ACPI トランスポートを使用するコントローラーが埋め込まれているシステムの場合。 

[Write a UCSI client driver (UCSI クライアント ドライバーの作成)](write-a-ucsi-driver.md)

[USB タイプ-C ドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

## <a href="" id="hardware"></a>USB タイプ-C システム設計


次に、埋め込みコントローラーのないモバイルデバイスの USB タイプ C システムの例を示します。

![モバイルデバイス向けの usb タイプ-c ハードウェア設計の例](images/type-c-hw2.png)

もう1つのビューを次に示します。

![usb タイプ-c ハードウェア設計サンプルデバイス (埋め込みコントローラーなし)](images/type-c-hw2-1.png)

上記の設計では、コネクタと通信するドライバーを実装し、コネクタで USB タイプ C イベントについてオペレーティングシステムに通知するようにします。

[USB タイプの C コネクタドライバーを作成する](bring-up-a-usb-type-c-connector-on-a-windows-system.md)

[USB タイプ-C ドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

## <a name="related-topics"></a>関連トピック
[USB タイプ C コネクタの Windows サポート](oem-tasks-for-bringing-up-a-usb-typec.md)  



