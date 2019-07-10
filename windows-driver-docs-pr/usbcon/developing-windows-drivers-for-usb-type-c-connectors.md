---
Description: C-USB 型システムに埋め込みコント ローラーが含まれていない場合それ以外の場合は Microsoft 提供の UCSI ドライバーをロードするコネクタ用のドライバーを記述する必要があります。
title: USB タイプ-c コネクタ用の Windows ドライバーの開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bcee7d92a050eff44e096df6d79c341a369d9ba
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716984"
---
# <a name="overview-of-developing-windows-drivers-for-usb-type-c-connectors"></a>USB タイプ-c コネクタ用の Windows ドライバーの開発の概要

C-USB 型システムが PD ステート マシンを実装していないまたはステート マシンの実装が非 ACPI トランスポート経由で UCSI をサポートしていませんが、コネクタのドライバーを記述する必要があります。 その場合は、Microsoft から提供されたを読み込むことができます[UCSI ドライバー](ucsi.md)します。

**対象読者**

-   USB タイプ-c システムのドライバー開発ガイダンスでは、埋め込みコント ローラーは含まれません。

**最終更新日**

-   2018 の年 9 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

**重要な API**

-   [USB タイプ-c ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

![ドライバー](images/drivers-c.png)


|             ハードウェアまたはファームウェアの機能             |                                                                                                                                                    非切り離し可能                                                                                                                                                    |                                                                                                                              アドオンのカード                                                                                                                               |
|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| USB タイプ-c コネクタには、PD ステート マシンはありません。 |        [クライアント ドライバーを書き込む UcmTcpciCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)します。 <p>始まり[UcmTcpciCx ポート コント ローラーのクライアント ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample) </p>        | [クライアント ドライバーを書き込む UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)します。 <p>始まり、 [UcmCx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)します。</p> |
|         コネクタは、ACPI に UCSI-準拠。         |                                                          UcmUcsiCx.sys と UcmUcsiAcpiClient、インボックス ドライバーを読み込みます。 参照してください[USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)します。                                                           |                                                                                                                                  なし                                                                                                                                   |
|       コネクタは ACPI せず UCSI に準拠しています。        | クライアント ドライバーは UcmUcsiCx 書き込みます。 詳細については、次を参照してください。 [UCSI クライアント ドライバーを書く](write-a-ucsi-driver.md)します。 <p>始まり[こちらのサンプル テンプレート](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)ACPI 部分を必要なバスの実装に置き換えます。 |                                                           [クライアント ドライバーを書き込む UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)します。                                                            |
|    PD ステート マシンが UCSI 準拠ではありません。     |                          [クライアント ドライバーを書き込む UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)します。 <p>始まり、 [UcmCx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)します。                          | [クライアント ドライバーを書き込む UcmCx](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)<p>始まり、 [UcmCx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)します。 </p>  |

## <a name="in-this-section"></a>このセクションの内容
実装には、前の表では、提案されたソリューションは、これらのトピックを参照します。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="architecture--usb-type-c-in-a-windows-system.md" data-raw-source="[Architecture: USB Type-C design for a Windows system](architecture--usb-type-c-in-a-windows-system.md)">アーキテクチャ:Windows システムの USB 型-C# のデザイン</a></p></td>
<td><p>USB タイプ-c システムとハードウェア コンポーネントをサポートする Microsoft 提供のドライバーの一般的なハードウェア設計について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="function-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the function controller on a USB Type-C Windows system](function-controller-bringup-for-a-usb-type-c-system.md)">USB タイプ C Windows システム関数のコント ローラーの起動します。</a></p></td>
<td><p>関数コント ローラーのドライバーは、その型から C の USB コネクタがサポートし、課金を開始し、デバイスに描画できる現在の最大量ときにバッテリ サブシステムに通知充電中レベルの詳細について、オペレーティング システムを通知します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dual-role-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the dual-role controller for a USB Type-C Windows system](dual-role-controller-bringup-for-a-usb-type-c-system.md)">USB タイプ C Windows システムのデュアル ロール コント ローラーの起動します。</a></p></td>
<td><p>役割の交代の USB ドライバー (URS) は、WDF クラスの拡張機能とデュアル ロール コント ローラーの役割の交代機能を処理するクライアント ドライバーのセットです。 システムの役割のデュアル コント ローラーの場合は、システムの USB 型-c コネクタのパートナーのポートに接続されているデバイスによってシステムの役割を切り替えることができます。 これにより、ワイヤード (有線) のドッキングなど、興味深いシナリオができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">USB タイプ-c コネクタのドライバーを作成します。</a></p></td>
<td><p>USB タイプ-c コネクタとコネクタのドライバーの想定される動作を管理する USB コネクタ マネージャ (UCM) について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="write-a-usb-type-c-port-controller-driver.md" data-raw-source="[Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)">USB タイプ-c ポート コント ローラー ドライバーを作成します。</a></p></td>
<td><p>記述する方法について説明します、せず PD ステート マシン型-C# の USB コネクタと通信する型-C# の USB ポート コント ローラー ドライバー。 </p></td>

</tr>
<tr class="even">
<td><p><a href="write-a-ucsi-driver.md" data-raw-source="[Write a UCSI client driver](write-a-ucsi-driver.md)">Write a UCSI client driver (UCSI クライアント ドライバーの作成)</a></p></td>
<td><p>非 ACPI のトランスポートを使用する UCSI 準拠コント ローラー用ドライバーを記述する方法について説明します。 </p></td>

</tr>

<tr>
<tr class="odd">
<td><a href="policy-manager-client.md" data-raw-source="[Write a USB Type-C Policy Manager client driver](policy-manager-client.md)">Write a USB Type-C Policy Manager client driver (USB Type-C ポリシー マネージャー クライアント ドライバーの作成)</a></td>
<td>Microsoft から提供された USB 型 C ポリシー マネージャーは、USB 型-C# のコネクタのアクティビティを監視します。 Windows、バージョンは 1809 には、一連のポリシー マネージャーにクライアント ドライバーを記述するインターフェイスのプログラミングが導入されています。 クライアント ドライバーは、USB 型-C# のコネクタのポリシーの決定に参加できます。 この設定すると、エクスポート カーネル モード ドライバーまたはユーザー モード ドライバーを記述できます。 </td>
</tbody>
</table>



**関連項目**

[USB の役割の切り替え (URS) のクライアント ドライバーを記述します。 ](usb-dual-role-driver-stack-architecture.md)

[USB デュアルロール コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

[USB 関数のクライアント ドライバーを記述します。](developing-windows-drivers-for-usb-function-controllers.md)  

[USB 関数コントローラーのプログラミング参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

## <a name="related-topics"></a>関連トピック

[USB タイプ-c コネクタの Windows のサポート](oem-tasks-for-bringing-up-a-usb-typec.md)  





