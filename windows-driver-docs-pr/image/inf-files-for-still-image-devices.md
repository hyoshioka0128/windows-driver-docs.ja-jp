---
title: 静止画像デバイスの INF ファイル
description: 静止画像デバイスの INF ファイル
ms.assetid: f68ba904-9049-4f7e-9903-fdf6f413a1a5
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: bc4aec4498ba796cd832a592772f7a05a7b863fa
ms.sourcegitcommit: c4dc4a78ea33537bd47fc7fb666cfd0718d302e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58349263"
---
# <a name="inf-files-for-still-image-devices"></a>静止画像デバイスの INF ファイル

既定クラスのインストーラーを静止画像デバイス、 *sti\_ci.dll*、INF ファイルのエントリの特殊なセットを認識します。 内でのデバイスの INF ファイル内でこれらのエントリを配置する必要があります[ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)します。 エントリは、次の表で説明します。

| INF ファイルのエントリ | 値 | コメント |
| --- | --- | --- |
| サブクラス | StillImage | 必須 |
| DeviceType | スキャナー、カメラ、ビデオ デバイスの 3 2 の場合は 1 | 必須 |
| DeviceSubType | ベンダー定義の値 | 省略可能 |
| 接続 | 非 PnP デバイスのシリアル ポートまたはパラレル ポートに接続されている場合は、インストール時にポートのユーザーの選択を制限するには、シリアルまたは並列このできます。 | 任意。<br>指定しない場合、ユーザーは、任意のシリアル ポートまたはパラレル ポートを選択できます。 |
| 機能 | デバイスの機能を示すフラグをビットに変換される数を指定します。 これらのフラグは、レジストリに格納し、して Microsoft STI コンポーネントで使用できますが、 [STI_DEV_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/ns-sti-_sti_dev_caps)構造体。<br><br>0 − セット/クリア STI_GENCAP_NOTIFICATIONS STI_DEV_CAPS ビットします。<br>1 − セット/クリア STI_GENCAP_POLLING_NEEDED STI_DEV_CAPS ビットします。<br>2 − セット/クリア STI_GENCAP_GENERATE_ARRIVALEVENT STI_DEV_CAPS ビットします。<br>3 − セット/クリア STI_GENCAP_AUTO_PORTSELECT STI_DEV_CAPS ビットします。 | 省略可能 |
| プロパティ ページ | カスタマイズを作成する DLL の名前とエントリ ポイントを識別する[静止画像デバイスのプロパティ シート ページ](property-sheet-pages-for-still-image-devices.md)します。<br>次の例は、DLL を識別*estp2cpl.dll*、だけでなく**EnumStiPropPages**この DLL 内のエントリ ポイント。 エントリ ポイント名は省略可能です。エントリ ポイントの既定値を省略した場合、 **EnumStiPropPages**します。<br><br>`PropertyPages = estp2cpl.dll, EnumStiPropPages`<br><br> | 省略可能 |
| DeviceData | 下のレジストリに格納される情報を格納しているベンダーから提供されたデータのセクションを識別、 **DeviceData**キー。 TWAIN でサポートされているデバイスでは、[データ] セクションを含める必要があります、 **TwainDS**エントリ。 詳細については、次を参照してください[仕入先が変更可能なレジストリ値。](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si) | 任意。<br>ただし、このエントリに必要な[プッシュ モデルの対応アプリケーションを作成する](creating-push-model-aware-applications.md)します。 |
| イベント | 静止画像デバイス イベントの一覧を表示するベンダーから提供されたデータのセクションを識別します。 このセクションでは、各エントリには、次の形式が必要です。<br><br>`EventName="String",{GUID},App`<br><br>*EventName*イベントの内部名は、*文字列*は、イベントの表示文字列、 *GUID*イベントの guid を参照してください[イメージ デバイス イベントではまだ](still-image-device-events.md)、および*アプリ*イベントの発生時に起動されるようにイメージング アプリケーションを指定します。 現在登録されているアプリケーションを起動するのにアスタリスク (*) を使用して、*アプリ*します。 | 任意。<br>ただし、このエントリに必要な[プッシュ モデルの対応アプリケーションを作成する](creating-push-model-aware-applications.md)します。 |
| UninstallSection | 通常を格納している INF セクションを指す[INF DelFiles ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)と[INF してディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)します。 このセクション内のエントリでは、次の形式があります。<br><br>`UninstallSection=UninstallSectionName`<br><br>*UninstallSectionName*含んでいるセクションの名前を指定します**Delfiles**または**して**ディレクティブ。 なお**Windows ファイル保護**可能性がありますを使用して指定されている場合でも、いくつかのファイルを削除してからユーザーを禁止**DelFiles**ディレクティブ。 | 任意。<br>このエントリは、Windows 2000 でのみ有効です。 |

既定クラスのインストーラーを静止画像デバイス標準をサポートする[INF CopyFiles ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)します。 インストーラーは、アンインストール操作中にいくつかのデバイスで共有されるファイルが途中で削除されないようにコンポーネントのファイルの内部参照カウンターを使用します。

まだのイメージのデバイスの既定の INF ファイル*sti.inf*デバイスの種類ごとに 2 つのインストール セクションを次のように定義します。

- [INF DDInstall セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)、内で参照されている必要があります、 *DDInstall*のベンダーから提供された INF ファイルの次の表に示すようにします。

| USB デバイス | SCSI デバイス | シリアル デバイス |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection` |

- [INF DDInstall.Services セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)、内で参照されている必要があります、 *DDInstall*.**サービス**のベンダーから提供された INF ファイルの次の表に示すようにします。

| USB デバイス | SCSI デバイス | シリアル デバイス |
| --- | --- | --- |
| `Include=sti.inf`<br><br>`Needs=STI.USBSection.Services` | `Include=sti.inf`<br><br>`Needs=STI.SCSISection.Services`  | `Include=sti.inf`<br><br>`Needs=STI.SerialSection.Services` |

また場合[イメージの取得 Api のデバイスに固有のコンポーネントを作成する](creating-device-specific-components-for-image-acquisition-apis.md)、INF ファイルでこれらのコンポーネントのファイル名を含めるは通常。

静止画像デバイスの INF ファイルを作成する追加のガイダンスについては、エントリが含まれている Windows で提供される任意の INF ファイルを表示できる"サブクラス StillImage ="。

## <a name="remarks"></a>コメント

スキャナー、INF ファイルを開発するときに使用できます[Microsoft OS ディスクリプター](https://msdn.microsoft.com/library/windows/hardware/gg463179.aspx)互換性 ID 機能を有効にします。 これを行う場合は、複数のスキャナー モデルと互換性がある 1 つのスキャナー ドライバーを許可します。
