---
Description: Here are some example designs for USB Type-C system.
title: USB タイプ-c システムのハードウェアの設計
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a2677550b5c56a958b77a9af31ec3844a8263d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571548"
---
# <a name="hardware-design-usb-type-c-systems"></a>ハードウェアのデザイン:USB Type-C システム


**最終更新日**

-   2016 年 12 月

\[いくつかの情報は、リリース版の発売までに著しく変更される可能性がありますが、リリース前の製品に関連します。 Microsoft では、一切の保証、明示または黙示にかかわらず、ここで提供される情報はありません。\]

ここでは、C-USB 型システムの一部の例のデザインです。

一般的な USB C 型システムでは、これらのコンポーネントがあります。

-   **ロール-USB デュアル コント ローラー**ことができるか、または周辺機器デバイス/関数/ロールでホストの役割で動作します。 このコンポーネントは SoC. に統合されています。
-   **バッテリの充電 1.2 検出**特定 Soc に統合されている可能性があります。 ソフトウェアで他のユーザーを実装、SoC ベンダーによっては検出ロジックを実装する PMIC モジュールを提供します。 Windows 10 Mobile には、すべてのオプションがサポートしています。 このコンポーネントに関する情報を取得、SoC ベンダーに問い合わせてください。
-   **型 C PD ポート コント ローラー**種類 C の USB コネクタの [cc] ピンを管理します。 BMC のエンコードとデコードの電力配信メッセージをサポートしています。 このコンポーネントは通常、ほとんどの Soc に統合されていません。
-   **Mux**種類 C ポート コント ローラーによって検出された印刷の向きに応じてコント ローラー上のポートの SuperSpeed USB ペア。 Mux SuperSpeed ペアと、場合によっては SBU 行 (表示モジュールでは、通常は) 別の場所と代替のモードを開始します。
-   **VBus/VConn**ソースが必要です。 ほとんどの PMICs VBus/VConn コントロールを実装します。 詳細については、SoC PMIC/ベンダーにお問い合わせください。

## <a href="" id="emb"></a>埋め込みコント ローラーと USB 型-c システムの設計


USB タイプ-c システムのコンポーネントに加えて、上記の一覧で、埋め込みコント ローラーことができます。 このインテリジェントなマイクロ コント ローラー システムの種類 C および配信の電源ポリシー マネージャーとして機能します。

USB タイプを押しながら C システム埋め込みコント ローラーの例を次に示します。

![埋め込みコント ローラー デバイスの usb 型 c ハードウェア設計の例](images/type-c-hw1.png)

別のビューを次に示します。

![埋め込みコント ローラー デバイスの usb 型 c ハードウェア設計の例](images/type-c-hw1-1.png)

システム埋め込みコント ローラーでは、Microsoft によって提供されるインボックス ドライバーを USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様を実装するには、UcmUcsi.sys を読み込みます。

[UCSI ドライバー](ucsi.md)します。 ドライバーの読み込まれたデバイス スタックの詳細については、[ドライバーとシステムの USB 型-C# のコンポーネントをサポートするためにコント ローラーが埋め込まれた](architecture--usb-type-c-in-a-windows-system.md#drivers)を参照してください。


埋め込みコント ローラーを搭載したシステム非 ACPI のトランスポートを使用しています。 

[Write a UCSI client driver (UCSI クライアント ドライバーの作成)](write-a-ucsi-driver.md)

[USB タイプ-c ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

## <a href="" id="hardware"></a>USB タイプ-c システムの設計


埋め込みコント ローラーがないモバイル デバイスを USB C 型システムの例を次に示します。

![モバイル デバイスの usb 型 c ハードウェア設計の例](images/type-c-hw2.png)

別のビューを次に示します。

![埋め込みコント ローラーがない、型 c ハードウェアの設計例 usb デバイス](images/type-c-hw2-1.png)

上記の設計では、コネクタと通信し、コネクタで USB 型-C# のイベントに関する情報を通知するオペレーティング システムを保持するドライバーを実装します。

[USB タイプ-c コネクタのドライバーを作成します。](bring-up-a-usb-type-c-connector-on-a-windows-system.md)

[USB タイプ-c ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

## <a name="related-topics"></a>関連トピック
[USB タイプ-c コネクタの Windows のサポート](oem-tasks-for-bringing-up-a-usb-typec.md)  



