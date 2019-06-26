---
title: WHEA ポリシー設定
description: WHEA ポリシー設定
ms.assetid: 65ef70b7-a517-4428-9e6d-09c6da84e798
keywords:
- 予測的な失敗の分析 (PFA) WDK WHEA、レジストリ設定
- WDK WHEA のレジストリ設定
- WDK WHEA、予測的な失敗の分析 (PFA) のレジストリ設定
- WDK WHEA のポリシー設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0787cb6dfe69d07b9a9f5d36a7079a3ce318de7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377381"
---
# <a name="whea-policy-settings"></a>WHEA ポリシー設定


予測的な障害の分析 (PFA) として Windows ハードウェア エラー アーキテクチャ (WHEA) での実行は、レジストリ設定を使用して構成されます。 WHEA は、コンピューター システムの起動時に、これらのレジストリ設定を読み取ります。 これらの設定を変更するを有効にするには、システムを再起動する必要があります。

Windows 8 以降、WHEA ポリシーがあることができますがどちらかで管理[ **WHEAPolicyManagementMethods** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)または WHEA Powershell モジュールを使用します。 これらのモードのいずれかで、ポリシーが更新され、ポリシーの値が直ちに有効にします。

**注**  このトピックで説明されているレジストリ設定が使用するため WHEA によってのみです。 場合、[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)PFA を実行し、その構成設定を格納する、レジストリを使用して、このトピックに記載されているものとは異なるレジストリ値を使用する必要があります。

 

WHEA PFA 構成設定は、次のレジストリ キーに配置されます。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WHEA\Policy
```

**注**  WHEA は、その値が 存在しない場合、PFA レジストリ値の既定の設定を想定しています**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\WHEA\\ポリシー**します。

 

次の表では、PFA 構成に使用されるさまざまなレジストリ値について説明します。 次の表のレジストリ値は REG\_DWORD の値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ値の名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<p><strong>DisableOffline</strong></p></td>
<td><p>WHEA が PFA を使用してオフラインのハードウェア コンポーネントを取得できるかどうかを指定するブール値。 WHEA は、PFA (WHEA またはプラグイン PSHED によって実行される) の判断、モジュールがエラーのしきい値を超えたときに、ECC メモリ ページなどのハードウェア コンポーネントとオフラインします。</p>
<div class="alert">
<strong>注</strong>  、 <strong>DisableOffline</strong>値 WHEA またはプラグイン PSHED でいずれかを実行する PFA のために失敗すると予測されます。 ハードウェア コンポーネントに適用されます。
</div>
<div>
 
</div>
<p>値 0 は、ハードウェアのオフライン サポートを有効します。 その他の値は、ハードウェアのオフライン サポートを無効にします。</p>
<p>この設定の既定値は 0 です。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPersistOffline</strong></p></td>
<td><p>WHEA かかったオフライン ECC メモリ ページがでブート構成データ (BCD) を保持するかどうかを指定するブール値を格納します。 BCD ストア内に保存場合、ECC メモリ ページはオフライン システムが再起動された後すぐに。</p>
<div class="alert">
<strong>注</strong>  、 <strong>MemPersistOffline</strong>値 WHEA またはプラグイン PSHED でいずれかを実行する PFA のためオフラインになった ECC メモリ ページに適用されます。
</div>
<div>
 
</div>
<p>1 の値には、BCD の永続化が有効になります。 値 0 は、BCD の永続化を無効にします。</p>
<p>この設定の既定値は、Windows Server プラットフォーム 1 および Windows クライアント プラットフォームの場合は 0。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaDisable</strong></p></td>
<td><p>WHEA の PFA ECC メモリ ページが無効になっているかどうかを指定するブール値。</p>
<p>値が 0 のでは、ECC メモリ ページの PFA ができるようにします。 その他の値には、ECC メモリ ページの PFA が無効にします。</p>
<p>この設定の既定値は 0 です。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaPageCount</strong></p></td>
<td><p>WHEA が PFA を監視する ECC メモリ ページの最大数を指定する値。</p>
<p>この値は、1 ~ 65536 で指定できます。 既定値は、64 です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外にある数に設定されている場合、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaThreshold</strong></p></td>
<td><p>エラーの最大数を指定する値は、WHEA が監視されて ECC メモリ ページの使用。</p>
<p>エラーの数がこのしきい値を超える WHEA メモリ ページの監視を停止し、メモリ ページをオフラインにしようとしています。</p>
<p>この値は、1 ~ 65536 で指定できます。 既定値は、16 です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外にある数に設定されている場合、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaTimeout</strong></p></td>
<td><p>ECC のメモリ ページはどのくらいですかを示す値を秒単位で PFA for WHEA によって監視します。</p>
<p>WHEA では、そのメモリ ページの最初のエラーが検出されたときに、ECC メモリ ページの監視を開始します。</p>
<p>WHEA では、次のいずれかが発生したときに、ECC メモリ ページの監視を停止します。</p>
<ul>
<li><p>監視間隔を超えた、 <strong>MemPfaTimeout</strong>値。</p></li>
<li><p>検出されたエラーの数を超えています、 <strong>MemPfaThreshold</strong>値。</p></li>
</ul>
<p>この値は、0 から 604800 (7 日間) まで指定できます。 値 0 は、監視対象のメモリ ページがタイムアウトしないことを指定します。既定値は、86400 (24 時間) です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外にある数に設定されている場合、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

アプリケーション互換性の理由からは、次の 2 つの従来のレジストリ値がサポートされています。

<a href="" id="singlebiteccerrorthreshold"></a>**SingleBitEccErrorThreshold**  
この値に対応、 **MemPfaThreshold**レジストリ値。

<a href="" id="maxcorrectedmceoutstanding"></a>**MaxCorrectedMCEOutstanding**  
この値に対応、 **MemPfaPageCount**レジストリ値。

**注**  可能であれば、これらの従来のレジストリ値ではなく、このトピックの前に説明したレジストリ値を使用する必要があります。

 

 

 




