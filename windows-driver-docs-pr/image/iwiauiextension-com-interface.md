---
title: IWiaUIExtension COM インターフェイス
description: IWiaUIExtension COM インターフェイス
ms.assetid: 10a8e981-889a-46f0-8bf5-da75632d4d94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08c18fd7f14918db2bc6d9735deb75c88d7f413f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378868"
---
# <a name="iwiauiextension-com-interface"></a>IWiaUIExtension COM インターフェイス





実装する場合、 [IWiaUIExtension インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545078(v=vs.85))、none、一部またはすべてを実装することができます、 **IWiaUIExtension**メソッド。 場合、特定のメソッドは、電子メールを返します。\_NOTIMPL、システム指定の代替、およびその 1 つには、代わりに使用されます。

**IWiaUIExtension**インターフェイスは、次のメソッドを提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::DeviceDialog&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))"><strong>IWiaUIExtension::DeviceDialog</strong></a></p></td>
<td><p>既定のシステムのユーザー インターフェイスを置換するカスタム ユーザー インターフェイスを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceBitmapLogo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85))"><strong>IWiaUIExtension::GetDeviceBitmapLogo</strong></a></p></td>
<td><p>デバイスのカスタム ビットマップのロゴを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceIcon&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))"><strong>IWiaUIExtension::GetDeviceIcon</strong></a></p></td>
<td><p>カスタム デバイス アイコンを取得します。</p></td>
</tr>
</tbody>
</table>

 

[**IWiaUIExtension::DeviceDialog** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))へのポインターを受け取る、 [ **DEVICEDIALOGDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/ns-wiadevd-tagdevicedialogdata)構造 (で宣言されている*wiadevd.h*)、デバイスのダイアログ ボックスを実装するために必要なすべてのデータが含まれています。

デバイス ダイアログは、次の 4 つの制約を受けますモーダル Win32 ダイアログ ボックスとして実装する必要があります。

1.  返される項目の配列*pDeviceDialogData*--&gt;**ppWiaItems**を使用して割り当てる必要がある**CoTaskMemAlloc**、によって解放されると、アプリケーションを使用して**CoTaskMemFree** (どちらの関数の Microsoft Windows SDK のドキュメントを参照してください)。

2.  破棄する必要がありますまたはに格納されているリリース ルート項目*pDeviceDialogData* --&gt;**pIWiaItemRoot**します。 する必要がありますいないが発生する、ルート項目が無効になります。 たとえば、呼び出す必要はありません、WIA\_CMD\_デバイスの同期コマンド。

3.  戻り値の S\_データ転送、および秒に、ユーザーが要求したことを示すには、[ok]\_ユーザーに、転送がキャンセルされたことを示す場合は FALSE。

4.  そのメモリ容量を確認するように注意またはインプロセスで実行されるため、リソースのリークは、このコンポーネントに導入されています、アプリケーションでします。

[**IWiaUIExtension::GetDeviceIcon** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))ドライバーが指定したアイコンを使用するアプリケーションを使用します。 リークのリソースを回避するために、このアイコンで読み込む必要があります**LoadImage**、LR を使用して\_共有のフラグ (Windows SDK のドキュメントを参照してください)。

[**IWiaUIExtension::GetDeviceBitmapLogo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85))により、アプリケーションに適切なデバイスと仕入先のロゴを表示できます。 現時点では、システム コンポーネントには、このメソッドは使用しません。 DIB に割り当てられたビットマップがありますを使用してビットマップ**CreateDIBSection**、またはを使用して読み込まれた**LoadImage** 、lr\_CREATEDIBSECTION フラグが (詳細については、Windows SDK のマニュアルを参照してください情報)。 これにより、アプリケーションをパレットの情報を抽出し、現在または表示の色深度を変更します。

カスタム スキャン ダイアログ ボックスを実装すると、WIA スキャナー ドライバーでは、使用、 **IWiaUIExtension::DeviceDialog**メソッド (上記 4 つの制約) と Win32 のモーダル ダイアログ ボックスを作成して DEVICEDIALOGDATA 構造体を渡す*dwInitParam* LPARAM として DialogBoxParam 関数のパラメーター。

これは、自体デバイス ダイアログ ボックスがデータ転送を管理していないことに注意してください。 ダイアログ ボックスの単なる配列へのポインターを返します**IWiaItem**ドライバーからアプリケーションへのポインター (プロパティ セット) を含むインターフェイスします。 転送メカニズムと形式をネゴシエートするアプリケーションの役目です。

 

 




