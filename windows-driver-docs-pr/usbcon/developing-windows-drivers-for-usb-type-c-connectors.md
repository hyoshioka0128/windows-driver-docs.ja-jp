---
Description: USB タイプ C システムに埋め込みコントローラーが含まれていない場合は、コネクタ用のドライバーを作成する必要があります。それ以外の場合は、Microsoft 提供の UCSI ドライバーを読み込むことができます。
title: USB Type-C コネクタ用 Windows ドライバー開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94bcc13f4f6be2654dd57ea360280bc8a199a28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842389"
---
# <a name="overview-of-developing-windows-drivers-for-usb-type-c-connectors"></a>USB Type-C コネクタ用 Windows ドライバー開発の概要

USB タイプ C システムが PD ステートマシンを実装していない場合や、ステートマシンを実装していても、非 ACPI トランスポートをサポートしていない場合は、コネクタ用のドライバーを作成する必要があります。 含まれている場合は、Microsoft 提供の[Ucsi ドライバー](ucsi.md)を読み込むことができます。

**対象読者**

-   USB タイプ C システムのドライバー開発ガイダンスには、埋め込みコントローラーは含まれていません。

**最終更新日時**

-   2018年9月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

**重要な API**

-   [USB タイプ-C ドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

![ドライバー](images/drivers-c.png)


|             ハードウェア/ファームウェアの機能             |                                                                                                                                                    非切り離し                                                                                                                                                    |                                                                                                                              アドオンカード                                                                                                                               |
|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| USB タイプ-C コネクタには、PD ステートマシンがありません。 |        [クライアントドライバーを UcmTcpciCx に書き込み](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)ます。 <p>[Ucmtcpcicx ポートコントローラークライアントドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)を使用して開始する </p>        | [クライアントドライバーを UcmCx に書き込み](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)ます。 <p>[Ucmcx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)を使用して開始します。</p> |
|         コネクタは、ACPI に準拠しています。         |                                                          インボックスドライバー UcmUcsiCx と UcmUcsiAcpiClient を読み込みます。 「 [USB タイプ-C コネクタシステムソフトウェアインターフェイス (UCSI) ドライバー」を](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)参照してください。                                                           |                                                                                                                                  該当なし                                                                                                                                   |
|       コネクタは、ACPI を使用せずに、UCSI に準拠しています。        | クライアントドライバーを UcmUcsiCx に書き込みます。 詳細については、「 [UCSI クライアントドライバーの記述](write-a-ucsi-driver.md)」を参照してください。 <p>[このサンプルテンプレート](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)から開始し、ACPI 部分を必要なバスの実装に置き換えます。 |                                                           [クライアントドライバーを UcmCx に書き込み](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)ます。                                                            |
|    には PD ステートマシンがありますが、UCSI に準拠していません。     |                          [クライアントドライバーを UcmCx に書き込み](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)ます。 <p>[Ucmcx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)を使用して開始します。                          | [クライアントドライバーを UcmCx に書き込む](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)<p>[Ucmcx サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmCxUcsi)を使用して開始します。 </p>  |

## <a name="in-this-section"></a>このセクションの内容
前の表の提案されたソリューションを実装するには、次のトピックを参照してください。
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
<td><p><a href="architecture--usb-type-c-in-a-windows-system.md" data-raw-source="[Architecture: USB Type-C design for a Windows system](architecture--usb-type-c-in-a-windows-system.md)">アーキテクチャ: Windows システム向けの USB タイプ C 設計</a></p></td>
<td><p>USB タイプ C システムの一般的なハードウェア設計と、ハードウェアコンポーネントをサポートする Microsoft 提供のドライバーについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="function-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the function controller on a USB Type-C Windows system](function-controller-bringup-for-a-usb-type-c-system.md)">USB 型の関数コントローラーを表示する-C Windows システム</a></p></td>
<td><p>関数コントローラーのドライバーは、USB タイプ C コネクタがサポートしている充電レベルについてオペレーティングシステムに通知し、充電を開始できることと、デバイスが描画できる最大容量をバッテリサブシステムに通知します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="dual-role-controller-bringup-for-a-usb-type-c-system.md" data-raw-source="[Bring up the dual-role controller for a USB Type-C Windows system](dual-role-controller-bringup-for-a-usb-type-c-system.md)">USB タイプのデュアルロールコントローラーを起動する-C Windows システム</a></p></td>
<td><p>USB 役割スイッチドライバー (URS) は、一連の WDF クラス拡張機能とそのクライアントドライバーで、デュアルロールコントローラーの役割切り替え機能を処理します。 システムにデュアルロールコントローラーがある場合は、システムの USB タイプ C コネクタのパートナーポートに接続されているデバイスに応じて、システムの役割を切り替えることができます。 これにより、ワイヤード (有線) ドッキングなどの興味深いシナリオが可能になります。</p></td>
</tr>
<tr class="even">
<td><p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">USB タイプの C コネクタドライバーを作成する</a></p></td>
<td><p>USB タイプ C コネクタと、コネクタドライバーの予期される動作を管理する USB コネクタマネージャー (UCM) について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="write-a-usb-type-c-port-controller-driver.md" data-raw-source="[Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)">USB タイプの C ポートコントローラードライバーを作成する</a></p></td>
<td><p>PD ステートマシンなしで USB タイプ C コネクタと通信する USB タイプ C ポートコントローラードライバーを記述する方法について説明します。 </p></td>

</tr>
<tr class="even">
<td><p><a href="write-a-ucsi-driver.md" data-raw-source="[Write a UCSI client driver](write-a-ucsi-driver.md)">Write a UCSI client driver (UCSI クライアント ドライバーの作成)</a></p></td>
<td><p>非 ACPI トランスポートを使用する UCSI 準拠コントローラーのドライバーを記述する方法について説明します。 </p></td>

</tr>

<tr>
<tr class="odd">
<td><a href="policy-manager-client.md" data-raw-source="[Write a USB Type-C Policy Manager client driver](policy-manager-client.md)">Write a USB Type-C Policy Manager client driver (USB Type-C ポリシー マネージャー クライアント ドライバーの作成)</a></td>
<td>Microsoft 提供の USB タイプ C ポリシーマネージャーは、USB タイプ C コネクタのアクティビティを監視します。 Windows バージョン1809では、クライアントドライバーをポリシーマネージャーに書き込むために使用できる一連のプログラミングインターフェイスが導入されています。 クライアントドライバーは、USB タイプ C コネクタのポリシーの決定に参加できます。 このセットを使用して、カーネルモードのエクスポートドライバーまたはユーザーモードドライバーを作成できます。 </td>
</tbody>
</table>



**関連セクション**

[USB 役割スイッチ (URS) クライアントドライバーの作成](usb-dual-role-driver-stack-architecture.md)

[USB デュアルロール コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

[USB 関数のクライアントドライバーを作成する](developing-windows-drivers-for-usb-function-controllers.md)  

[USB 関数コントローラーのプログラミング参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

## <a name="related-topics"></a>関連トピック

[USB タイプ C コネクタの Windows サポート](oem-tasks-for-bringing-up-a-usb-typec.md)  





