---
Description: USB の役割の切り替えドライバーとそのクライアント ドライバー デュアル ロール コント ローラーの役割の交代機能を処理します。
title: USB Type-C Windows システムにおけるデュアルロール コントローラーの起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f71dd96b1c325a0f8427b34ec930b0d9267831e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383038"
---
# <a name="bring-up-the-dual-role-controller-for-a-usb-type-c-windows-system"></a>USB Type-C Windows システムにおけるデュアルロール コントローラーの起動


**要約**

-   OEM は、USB 型-c コネクタがあるデュアル ロール コント ローラーのタスクを表示します。

**適用対象**

-   Windows 10 Mobile

**最終更新日**

-   2016 年 12 月

**重要な API**

-   [USB デュアルロール コントローラー ドライバーのプログラミング参照](https://msdn.microsoft.com/library/windows/hardware/mt628026)

役割の交代の USB ドライバー (URS) は、WDF クラスの拡張機能とそのデュアル ロール コント ローラーの役割の交代機能を処理できるクライアント ドライバーのセットです。 システムの役割のデュアル コント ローラーの場合は、システムの USB 型-c コネクタのパートナーのポートに接続されているデバイスによってシステムの役割を切り替えることができます。 これにより、ワイヤード (有線) のドッキングなど、興味深いシナリオができます。

デュアル ロール USB コント ローラーが Windows ホストまたは関数のいずれかのモードに構成する必要があるように、システムを設計できます。 これらの設計では、USB ロール スイッチのスタックを使用します。 システムが Synopsys または ChipIdea のロールのデュアル コント ローラーを使用しない場合は、システムの役割のデュアル コント ローラー用の USB ロール切り替えのクライアント ドライバーを記述する必要があります。

**注**  デュアル ロールの USB ポートが Windows ホストまたは関数のいずれかのモードに構成する必要があるようには、システムを設計することができます。 これらの設計では、USB ロール スイッチのスタックを使用します。 システムが Synopsys ロール デュアル コント ローラーを使用しない場合は、システムの役割のデュアル コント ローラー用の USB ロール切り替えのクライアント ドライバーを記述する必要があります。

 

クライアント ドライバーでは、ハードウェアのイベントを処理し、クラスの拡張機能に報告します。 役割の交代ハードウェアのイベントが発生した場合は、URS は、ロールを決定し、したがってそのロール用のドライバーを読み込みます。 コント ローラーがホストの役割の場合、[ホスト側の USB ドライバー](usb-3-0-driver-stack-architecture.md)が読み込まれるは、関数の役割、[デバイス側ドライバー](usb-device-side-drivers-in-windows.md)が読み込まれます。

システム USB マイクロ AB コネクタでは、デュアル ロール コント ローラーのクライアント ドライバーに割り当てられている割り込みリソースを使用して、コネクタの ID のピンに基づく決定を使用します。 システム型-C# の USB コネクタでは、この決定は、コネクタのクライアント ドライバーによって実現されます。 CC に基づくロールのピンし、役割の交代のドライバーに結果を送信する USB コネクタ マネージャ (UCM) に結果を報告するドライバーを決定します。

![ロール切り替えの usb ドライバー](images/urs.png)

## <a name="1-enable-the-urs-driver-in-system-acpi"></a>1. ACPI システムで URS ドライバーを有効にします。


URS を使用するには、ACPI の変更を行う必要があります。 これでデバイスを交換して、[デバイス側の USB ドライバー](usb-device-side-drivers-in-windows.md) urs においての読み込む必要があります、デバイスを使用して読み込みます。 ACPI の定義を変更する方法の詳細についてで指定された例を参照してください。 [USB デュアル ロール ドライバー スタック アーキテクチャ](usb-dual-role-driver-stack-architecture.md)します。 割り込みのリソースを削除することを確認します。 USB タイプ-C. の必須ではありません。

## <a name="2-load-the-usb-role-switch-drivers-for-the-dual-role-controller-driver"></a>2. デュアル ロール コント ローラーのドライバーの役割の交代の USB ドライバーを読み込む


![usb ロール スイッチのスタック](images/urs.png)

-   システム ChipIdea および Synopsys コント ローラーを使用する場合は、ChipIdea および Synopsys コント ローラーの組み込みのクライアント ドライバーを提供する Microsoft を読み込みます。

    ドライバーを読み込むには、ドライバーのインストール パッケージを作成する必要があります。 INF ファイルが必要**Include ニーズ**ディレクティブのサポートされているコント ローラーのインボックス INF を参照します。 インボックス INF には、既に他のコント ローラーのハードウェア Id が含まれています。 デュアル ロール コント ローラーのハードウェア ID がないボックスの INF にハードウェア Id のいずれかの場合、この手順が必要です。 SoC ベンダーに確認します。

    詳細については、「URS ドライバー パッケージ」を参照してください。[ドライバー インストール パッケージ](usb-dual-role-driver-stack-architecture.md#inf)します。

-   システムは、カスタムのコント ローラーを使用している場合は、役割の交代クライアント ドライバーを作成します。 詳しくは、次のトピックをご覧ください。

    [USB デュアルロール コントローラー ドライバーのプログラミング参照](https://msdn.microsoft.com/library/windows/hardware/mt628026)

## <a name="related-topics"></a>関連トピック
[USB デュアル ロール ドライバー スタック アーキテクチャ](usb-dual-role-driver-stack-architecture.md)  



