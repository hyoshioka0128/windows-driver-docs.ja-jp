---
title: プロパティ ページの Windows メッセージの処理
description: プロパティ ページの Windows メッセージの処理
ms.assetid: 4920a003-59b5-41dc-a8ee-5e034087006a
keywords:
- デバイスのプロパティ ページの WDK デバイス インストールでは、Windows メッセージ
- プロパティ ページの WDK デバイス インストールでは、Windows メッセージ
- カスタム プロパティ ページの WDK デバイス インストールでは、Windows メッセージ
- WM_INITDIALOG
- Windows メッセージ WDK プロパティ ページ
- SendDlgItemMessage
- WDK のプロパティ ページのフレンドリ名
- WM_NOTIFY
- PSN_APPLY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7648e76a22ea1e88b9eb28caa73b0173d5e692c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531517"
---
# <a name="handling-windows-messages-for-property-pages"></a>プロパティ ページの Windows メッセージの処理





ときに、[デバイスのプロパティ ページのプロバイダー](types-of-device-property-page-providers.md)プロパティ ページ ダイアログ ボックス プロシージャのアドレスを返しますが、そのデバイスまたはデバイス クラスのプロパティ ページを作成する要求をハンドルします。 WM_INITDIALOG メッセージを取得し、その WM_NOTIFY メッセージを取得すると、デバイスのプロパティへの変更を処理する準備を整える必要があります、ダイアログ ボックス プロシージャはプロパティ ページを初期化する必要があります。 プロシージャは、Microsoft Windows SDK ドキュメントで説明されているようにも、このようなメッセージはすべて必要がありますに処理できます。

WM_INITDIALOG メッセージに応答してでは、ダイアログ ボックス プロシージャは、プロパティ ページの情報を初期化します。 このような情報は、デバイス、その PnP デバイスの説明と、デバイスのフレンドリ名を表すアイコンを含めることができます。

[**SetupDiLoadClassIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff552053)クラスを指定したデバイスのアイコンの読み込みし、アンロードの大きいアイコンを後続の呼び出しで使用できるハンドルを返します**SendDlgItemMessage**します。 次に、例を示します。

```cpp
if (SetupDiLoadClassIcon(
        &pTestPropPageData->DeviceInfoData->ClassGuid, &ClassIcon, 
        NULL)) {
    OldIcon = (HICON)SendDlgItemMessage(
                        hDlg, 
                        IDC_TEST_ICON,
                        STM_SETICON, (WPARAM)ClassIcon, 0);
    if (OldIcon) {
                DestroyIcon(OldIcon);
    }
}
```

ClassIcon で返されたハンドルは、SendDlgItemMessage 関数で必要とされる WPARAM にキャストすることができます。 例では、IDC_TEST_ICON は STM_SETICON メッセージを受信する ダイアログ ボックス コントロールを識別します。 IDC_TEST_ICON の値は、プロバイダーで定義する必要があります。 アイコンとビットマップを操作するその他の関数を参照してください[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)します。 詳細については**SendDlgItemMessage**、 **DestroyIcon**、およびアイコンを使用して、ダイアログ ボックスで、Windows SDK のドキュメントを参照してください。

だけでなく、デバイスを表すアイコン、一般的なデバイスのプロパティ ページは、説明またはデバイスの「表示名」が含まれています、デバイスのプロパティの現在の設定を示しています。 プラグ アンド プレイ (PnP) マネージャーでは、レジストリ内の各デバイスの PnP のプロパティを格納します。 プロパティ ページのプロバイダーを呼び出すことができます[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)このような任意のプロパティの値を取得します。 デバイスまたはクラス固有の構成情報が、インストール プロセスの一部として、レジストリに格納されているもの場合、プロパティ ページ プロバイダーを使用して他の**SetupDiXxx**表示用には、その情報を抽出する関数。 詳細については、次を参照してください。[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)します。

ページで特定の種類の変更が発生すると、プロパティ シートの送信、 [WM_NOTIFY](https://go.microsoft.com/fwlink/p/?linkid=181554)メッセージ、ダイアログ ボックス プロシージャをします。 メッセージ パラメーターから通知コードを抽出し、適切に応答するには、ダイアログ ボックス プロシージャを準備する必要があります。

ダイアログ ボックス プロシージャが発生する可能性がある通知について、PSN_APPLY または PSN_HELP 通知、および手順が処理する方法などの詳細については、次を参照してください[通知](https://go.microsoft.com/fwlink/p/?linkid=181555)Windows sdk。ドキュメントです。

### <a href="" id="psn-apply-notifications"></a>PSN_APPLY 通知

ユーザーがクリックしたときに、プロパティ シートが PSN_APPLY 通知メッセージを送信**OK**、**閉じる**、または**適用**します。 このメッセージに応答して、ダイアログ ボックス プロシージャが検証し、ユーザーによって行われた変更を適用する必要があります。

PSN_APPLY 通知を受信した場合、プロバイダー、次の操作する必要があります。

1.  これが既に実行していない場合は、デバイスのインストール パラメーターをポインターを取得 ([**SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)構造) デバイス。 呼び出してこの構造体が使用可能な[ **SetupDiGetDeviceInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff551104)を渡して、保存された*DeviceInfoSet*と*DeviceInfoData*によって参照される領域内で渡されたが、 **lParam** PROPSHEETPAGE 構造体のメンバー。

2.  ユーザーの変更が有効であることを確認します。

3.  プロバイダーが DI_FLAGSEX_PROPCHANGE_PENDING フラグを設定する必要があります、プロバイダーは、Windows を削除し、デバイスの再起動が必要なプロパティを設定するユーザーを許可している場合、 **FlagsEx**返された SP_DEVINSTALL_PARAMS のフィールド構造体。

    ただし場合、プロバイダーは、変更には、デバイスのドライバーを停止して再起動が必要としないことを確認できますがないこのフラグを設定します。

4.  呼び出す[ **SetupDiSetDeviceInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552141)で、変更された[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)構造に新しいパラメーターを設定します。

### <a href="" id="psn-reset-notifications"></a>PSN_RESET 通知

ユーザーがクリックしたときに、プロパティ シートが PSN_RESET 通知メッセージを送信**キャンセル**します。 このメッセージに応答して、ダイアログ ボックス プロシージャは、ユーザーによって行われた変更を破棄する必要があります。

 

 





