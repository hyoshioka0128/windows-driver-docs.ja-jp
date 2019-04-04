---
Description: The driver for the function controller informs the operating system about the charging levels that its USB Type-C connector supports and notifies the battery subsystem when it can begin charging and the maximum amount of current the device can draw.
title: USB タイプ C Windows システム関数のコント ローラーの起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 488ea8a90b8d46564e7351c001267271f719f854
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559177"
---
# <a name="bring-up-the-function-controller-on-a-usb-type-c-windows-system"></a>USB タイプ C Windows システム関数のコント ローラーの起動します。


**要約**

-   OEM は、USB 型-c コネクタがある関数のコント ローラーのタスクを表示します。

**適用されます。**

-   Windows 10 Mobile

**最終更新日**

-   2015 年 11 月

**重要な API**

-   [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt188010)
-   [独自の充電器をサポートするための USB フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/mt188012)

関数コント ローラーのドライバーは、その型から C の USB コネクタがサポートし、課金を開始し、デバイスに描画できる現在の最大量ときにバッテリ サブシステムに通知充電中レベルの詳細について、オペレーティング システムを通知します。

ここでは、特定の時点で、関数のコント ローラーが 1 つのコネクタ (UFP) を管理します。

## <a name="1-load-the-usb-device-side-drivers"></a>1. デバイス側の USB ドライバーを読み込む


関数のコント ローラーの操作を管理する 2 つのドライバーがあります。 ペアは、Microsoft 提供の USB 関数クラスの拡張機能とそのクライアント ドライバーがします。 クラスの拡張機能は、クライアント ドライバーによって、オペレーティング システムに送信される情報を報告します。 クライアント ドライバーでは、ハードウェアのインターフェイスを使用して、ハードウェアと通信します。 参照してください、 [Windows での USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)します。

![usb 関数コント ローラーのドライバー](images/function-controller.png)

-   場合は、システムでは、ChipIdea および Synopsys コント ローラーを使用します。
    1.  ChipIdea および Synopsys コント ローラーの組み込みのクライアント ドライバーを提供する Microsoft を読み込みます。
    2.  下位のフィルター ドライバーを取得しますアタッチ/デタッチ充電が接続されているときにイベントを記述します。 ドライバーは、充電器と構成プロパティの種類を決定します。 USB BC1.2 仕様で定義されたポートを充電中も検出できます。 課金調停ドライバー (CAD.sys) ことを報告できるように、クラスの拡張機能に情報を充電渡されます。 詳細については、[独自の充電器をサポートするための USB フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/mt188012)を参照してください。
-   システムは、カスタムのコント ローラーを使用している場合は、クライアント ドライバーを記述します。 BC1.2 は検出ロジックは、クライアント ドライバーで実装されます。 詳しくは、次のトピックをご覧ください。

    [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt188010)

    [関数の USB コント ローラーの Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)

## <a name="2-modify-system-acpi-to-indicate-to-the-function-controller-driver-that-the-connector-is-a-usb-type-c-connector"></a>2. コネクタは、USB 型-C# のコネクタを関数のコント ローラー ドライバーに示すために、ACPI システムを変更します。


これは、ACPI 6.0 仕様で定義されている ACPI メソッドを通じて行われます

`_UPC (USB Port Capabilities)`

ACPI 6.0 で定義されている新しい値を使用して、適切な種類の"種類 C USB2"と「型 C USB2 とスイッチを使用して SS」などの C-USB 型コネクタを示します。 関数のドライバーは、適切な充電ソースを決定する USB 種類 C 固有調停ロジックを使用するよう CAD.sys、するには、この情報を通信します。

```cpp
Device (UFN0)
{
    ...

    Name (_UPC, Package()
    {
        0x1,    // Connectable
        0x9,    // Type-C USB2 and Type-C USB2 and SS with switch
        0x0,    // Reserved
        0x0     // Reserved
    })

    Name (_CRS, ResourceTemplate()
    {
        ...
    })

    ...
```

## <a name="related-topics"></a>関連トピック
[USB タイプ-c コネクタの Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)  



