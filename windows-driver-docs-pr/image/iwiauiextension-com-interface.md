---
title: IWiaUIExtension COM インターフェイス
description: IWiaUIExtension COM インターフェイス
ms.assetid: 10a8e981-889a-46f0-8bf5-da75632d4d94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bfad4503557953eda9acaf66088cb05d0200026
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840792"
---
# <a name="iwiauiextension-com-interface"></a>IWiaUIExtension COM インターフェイス





[Iwiを](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545078(v=vs.85))実装する場合は、none、some、またはすべての**iwiの拡張**メソッドを実装できます。 特定のメソッドから E\_NOTIMPL が返される場合、システム指定の代替手段と使用可能なものが使用されます。代わりに、そのメソッドが使用されます。

**Iwi/Iextension**インターフェイスには、次のメソッドが用意されています。

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
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::DeviceDialog&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))"><strong>Iwievicedialog Iextension::D</strong></a></p></td>
<td><p>既定のシステムユーザーインターフェイスを置き換えるカスタムユーザーインターフェイスを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceBitmapLogo&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85))"><strong>Iwi/Iextension:: Getdevicebitma/ゴー</strong></a></p></td>
<td><p>デバイスのカスタムビットマップロゴを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)" data-raw-source="[&lt;strong&gt;IWiaUIExtension::GetDeviceIcon&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))"><strong>Iwi/Iextension:: GetDeviceIcon</strong></a></p></td>
<td><p>カスタムデバイスアイコンを取得します。</p></td>
</tr>
</tbody>
</table>

 

[**Iwievicedialog Iextension::D**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))は、デバイスダイアログボックスを実装するために必要なすべてのデータを含む[**Devicedialogdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/ns-wiadevd-tagdevicedialogdata)構造体へのポインター ( *wiadevd .h*で宣言) を受け入れます。

デバイスダイアログは、次の4つの制約に従って、モーダル Win32 ダイアログボックスとして実装する必要があります。

1.  *Pdevicedialogdata*--&gt;**ppwiaitems**に返される項目の配列は、 **CoTaskMemAlloc**を使用して割り当てる必要があり、アプリケーションによって**CoTaskMemFree**を使用して解放されます (Microsoft Windows SDK のドキュメントを参照してください)。2つの関数の場合)。

2.  *Pdevicedialogdata* --&gt;**Piwiaitemroot**に格納されているルート項目を破棄または解放することはできません。 また、ルート項目が無効になることもありません。 たとえば、WIA\_CMD\_SYNCHRONIZE device コマンドを呼び出すことはできません。

3.  S\_OK を返して、ユーザーがデータ転送を要求したことを示し、S\_FALSE を返して、ユーザーが転送を取り消したことを示します。

4.  メモリまたはリソースのリークは、アプリケーションでインプロセスで実行されるため、このコンポーネントでは導入されないように注意してください。

[**Iwi/Iextension:: GetDeviceIcon**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))を使用すると、アプリケーションはドライバーによって指定されたアイコンを使用できます。 リソースリークを回避するには、LR\_SHARED フラグを使用して、このアイコンを**LoadImage**で読み込む必要があります (Windows SDK のドキュメントを参照してください)。

[**Iwi/Iextension:: Getdevicebitma/ゴー**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545073(v=vs.85))を使用すると、アプリケーションは必要に応じてデバイスとベンダーのロゴを提示できます。 現在、このメソッドを使用するシステムコンポーネントはありません。 ビットマップは、 **Createdibsection**を使用して DIB で割り当てられたビットマップであるか、または**LoadImage**を使用して LR\_createdibsection フラグと共に読み込まれている必要があります (詳細については、Windows SDK のドキュメントを参照してください)。 これにより、アプリケーションは任意のパレット情報を抽出し、現在または変化している表示色の深度に適合させることができます。

カスタムスキャンダイアログボックスを WIA スキャナードライバーに実装するには、 **Iwievicedialog Iextension::D**メソッド (上記の4つの制約を含む) を使用して、Win32 モーダルダイアログボックスを作成し、DEVICEDIALOGDATA 構造を*Dwinitparam に渡します。* LPARAM としてのパラメーター関数のパラメーター。

デバイスのダイアログボックス自体はデータ転送を管理しないことに注意してください。 このダイアログボックスは、ドライバーからアプリケーションに**Iwiaitem**インターフェイスポインターの配列へのポインターを返すだけです (プロパティが設定されています)。 次に、転送メカニズムと形式をネゴシエートするアプリケーションが作成されます。

 

 




