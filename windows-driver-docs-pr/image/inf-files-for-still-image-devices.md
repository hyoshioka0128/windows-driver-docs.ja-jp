---
title: 静止イメージデバイス用の INF ファイル
description: 静止イメージデバイス用の INF ファイル
ms.assetid: f68ba904-9049-4f7e-9903-fdf6f413a1a5
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 770b88bcce17e4f8003bf512e4dc19707f1126bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840824"
---
# <a name="inf-files-for-still-image-devices"></a>静止イメージデバイス用の INF ファイル

静止イメージデバイスの既定のクラスインストーラーである*sti\_、ci .dll*は、特殊な一連の INF ファイルエントリを認識します。 INF ファイル内では、これらのエントリはデバイスの[**Inf DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)内に配置する必要があります。 次の表で、エントリについて説明します。

| INF ファイルのエントリ | 値 | 説明 |
| --- | --- | --- |
| サブクラス | StillImage | 必須 |
| DeviceType | スキャナーの場合は1、カメラの場合は2、ビデオデバイスの場合は3 | 必須 |
| DeviceSubType | ベンダー定義の値 | 省略可能 |
| 接続 | シリアルポートまたはパラレルポートに接続されている非 PnP デバイスの場合、これは、インストール時にユーザーが選択するポートを制限するために、シリアルまたは並列にすることができます。 | 省略可能。<br>指定しない場合、ユーザーは任意のシリアルポートまたはパラレルポートを選択できます。 |
| 機能 | デバイスの機能を識別するビットフラグに変換される数値を指定します。 これらのフラグはレジストリに格納され、 [STI_DEV_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_dev_caps)構造体を使用して Microsoft STI コンポーネントで使用できます。<br><br>ビット 0: STI_DEV_CAPS の STI_GENCAP_NOTIFICATIONS を設定/クリアします。<br>ビット 1: STI_DEV_CAPS で STI_GENCAP_POLLING_NEEDED を設定/クリアします。<br>ビット2− STI_DEV_CAPS で STI_GENCAP_GENERATE_ARRIVALEVENT を設定/クリアする<br>ビット 3: STI_DEV_CAPS で STI_GENCAP_AUTO_PORTSELECT を設定/クリアする | 省略可能 |
| PropertyPages | [静止画像デバイス用に](property-sheet-pages-for-still-image-devices.md)カスタマイズされたプロパティシートページを作成する DLL の名前とエントリポイントを識別します。<br>次の例では、dll、 *estp2cpl*、およびこの Dll の**enum**エントリポイントを識別します。 エントリポイント名は省略可能です。省略した場合、エントリポイントは既定で**enum/Proppages**に設定されます。<br><br>`PropertyPages = estp2cpl.dll, EnumStiPropPages`<br><br> | 省略可能 |
| DeviceData | **Devicedata**キーの下にある、レジストリに格納される情報を含む、ベンダーが提供するデータセクションを識別します。 TWAIN でサポートされているデバイスの場合、data セクションには**twの**エントリが含まれている必要があります。 詳細については、「[ベンダーが変更可能なレジストリ値](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si)」を参照してください。 | 省略可能。<br>ただし、[プッシュモデルに対応](creating-push-model-aware-applications.md)したアプリケーションを作成するには、このエントリが必要です。 |
| イベント | まだイメージデバイスイベントの一覧を示す、ベンダーから提供されたデータセクションを識別します。 このセクションの各エントリは、次の形式である必要があります。<br><br>`EventName="String",{GUID},App`<br><br>*EventName*はイベントの内部名、*文字列*はイベントの表示文字列、 *guid*はイベントの Guid、「[イメージデバイスのイベント](still-image-device-events.md)」を参照してください。さらに、*アプリ*は、イベントが発生したときに起動するイメージングアプリケーションを指定します。 現在登録されているアプリケーションを起動するには、*アプリ*にアスタリスク (*) を使用します。 | 省略可能。<br>ただし、[プッシュモデルに対応](creating-push-model-aware-applications.md)したアプリケーションを作成するには、このエントリが必要です。 |
| UninstallSection | 通常は inf [DelFiles ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)と[inf delfiles ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)を含む inf セクションを指します。 このセクションのエントリの形式は次のとおりです。<br><br>`UninstallSection=UninstallSectionName`<br><br>*Uninstallsectionname*は、 **delfiles**または**delfiles**ディレクティブを含むセクションの名前です。 **Windows ファイル保護**では、 **delfiles**ディレクティブを使用して指定されている場合でも、ユーザーが一部のファイルを削除できない可能性があることに注意してください。 | 省略可能。<br>このエントリは、Windows 2000 でのみ有効です。 |

静止イメージデバイスの既定のクラスインストーラーでは、標準の[INF CopyFiles ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)がサポートされています。 インストーラーはコンポーネントファイルに対して内部参照カウンターを使用するので、複数のデバイスで共有されているファイルは、アンインストール操作の途中で削除されません。

引き続きイメージデバイス (sti) の既定の INF ファイルでは、デバイスの種類ごとに次の2つのインストールセクションが定義されて*います*。

- 次の表に示すように、ベンダが提供する INF ファイルの*Ddinstall*セクション内で参照する必要がある[Inf ddinstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。

| USB デバイス | SCSI デバイス | シリアルデバイス |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection` |

- [INF ddinstall. Services セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)。 *ddinstall*内で参照する必要があります。次の表に示すように、ベンダーが提供する INF ファイルの**Services**セクション。

| USB デバイス | SCSI デバイス | シリアルデバイス |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection.Services` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection.Services`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection.Services` |

[イメージ取得 api 用のデバイス固有のコンポーネントも作成](creating-device-specific-components-for-image-acquisition-apis.md)する場合は、通常、これらのコンポーネントのファイル名を INF ファイルに含めます。

静止イメージデバイス用の INF ファイルの作成に関するその他のガイダンスについては、Windows で提供されている、"サブクラス = StillImage" というエントリを含む任意の INF ファイルを参照してください。

## <a name="remarks"></a>解説

スキャナー用の INF ファイルを開発している場合は、 [MICROSOFT OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))を使用して互換性 ID 機能を有効にすることができます。 これを行うと、1つのスキャナードライバーに複数のスキャナーモデルとの互換性を持たせることができます。
