---
title: WHEA ポリシー設定
description: WHEA ポリシー設定
ms.assetid: 65ef70b7-a517-4428-9e6d-09c6da84e798
keywords:
- 予測エラー分析 (PFA) WDK WHEA、レジストリ設定
- レジストリ設定 WDK WHEA
- レジストリ設定 WDK WHEA、予測エラー分析 (PFA)
- ポリシー設定 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c01cf7c897b949cf64556de9c6d5650edbbbbc9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828930"
---
# <a name="whea-policy-settings"></a>WHEA ポリシー設定


Windows ハードウェアエラーアーキテクチャ (WHEA) によって実行される予測エラー分析 (PFA) は、レジストリ設定を使用して構成されます。 WHEA は、コンピューターシステムの起動時にこれらのレジストリ設定を読み取ります。 これらの設定に変更を加えた場合は、システムを再起動して有効にする必要があります。

Windows 8 以降では、 [**WHEAPolicyManagementMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)または whea Powershell モジュールを使用して、whea ポリシーを管理できます。 これらのモードのいずれかを使用してポリシーを更新した場合、ポリシーの値は直ちに有効になります。

このトピックに記載されているレジストリ設定は、WHEA のみで使用することを想定し**て   ます**。 [プラットフォーム固有のハードウェアエラードライバー (pshed) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)が pshed を実行し、レジストリを使用して構成設定を格納している場合、このトピックで説明されているものとは異なるレジストリ値を使用する必要があります。

 

WHEA PFA 構成設定は、次のレジストリキーにあります。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WHEA\Policy
```

  WHEA では、値が**HKEY\_ローカル\_コンピューター\\システム\\CurrentControlSet\\コントロール\\WHEA\\ポリシー**に存在しない場合、pfa レジストリ値の既定の設定が使用されていることに**注意**してください。

 

次の表では、PFA 構成に使用されるさまざまなレジストリ値について説明します。 次の表のレジストリ値は、REG\_DWORD 値です。

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
<td><p>WHEA が PFA を使用してハードウェアコンポーネントをオフラインにするかどうかを指定するブール値です。 WHEA は、(WHEA または自己のプラグインによって実行される) PFA によってモジュールがエラーのしきい値を超えたと判断したときに、"ECC メモリ" ページなどのハードウェアコンポーネントをオフラインにします。</p>
<div class="alert"><strong>Disableoffline</strong>値は、WHEA または自己のプラグインによって実行された pfa が原因で失敗すると予測されるハードウェアコンポーネントに適用さ  
<strong>ことに注意</strong>してください。
</div>
<div>
 
</div>
<p>値を0にすると、ハードウェアのオフラインサポートが有効になります。 その他の値は、ハードウェアのオフラインサポートを無効にします。</p>
<p>この設定の既定値は0です。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPersistOffline</strong></p></td>
<td><p>WHEA がオフラインになった ECC メモリページがブート構成データ (BCD) ストアに保持されるかどうかを指定するブール値です。 BCD ストア内で永続化された場合、システムが再起動された直後に、ECC メモリページがオフラインになります。</p>
<div class="alert">Mempersistoffline 値は、WHEA または<strong>Ppersistプラグイン</strong>によって実行される pfa によってオフラインになった ECC メモリページに適用される  に
<strong>注意</strong>してください。
</div>
<div>
 
</div>
<p>値を1にすると、BCD の永続化が有効になります。 値0は BCD の永続化を無効にします。</p>
<p>この設定の既定値は、Windows Server プラットフォームの場合は1、Windows クライアントプラットフォームの場合は0です。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaDisable</strong></p></td>
<td><p>ECC メモリページの WHEA の PFA を無効にするかどうかを指定するブール値です。</p>
<p>値を0にすると、ECC メモリページの PFA が有効になります。 その他の値は、ECC メモリページの PFA を無効にします。</p>
<p>この設定の既定値は0です。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaPageCount</strong></p></td>
<td><p>WHEA が PFA を監視する ECC メモリページの最大数を指定する値。</p>
<p>この値は 1 ~ 65536 の範囲で指定できます。 既定値は64です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外の数値に設定されている場合は、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaThreshold</strong></p></td>
<td><p>WHEA が監視している ECC メモリページで許容されるエラーの最大数を指定する値。</p>
<p>エラーの数がこのしきい値を超えると、WHEA はメモリページの監視を停止し、メモリページをオフラインにしようとします。</p>
<p>この値は 1 ~ 65536 の範囲で指定できます。 既定値は16です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外の数値に設定されている場合は、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaTimeout</strong></p></td>
<td><p>PFA の WHEA によって ECC メモリページが監視される期間を指定する値 (秒単位)。</p>
<p>WHEA は、そのメモリページの最初のエラーが検出されたときに、[ECC メモリ] ページの監視を開始します。</p>
<p>WHEA は、次のいずれかが発生したときに、[ECC メモリ] ページの監視を停止します。</p>
<ul>
<li><p>監視間隔が<strong>MemPfaTimeout</strong>値を超えました。</p></li>
<li><p>検出されたエラーの数が<strong>Mempfathreshold</strong>の値を超えました。</p></li>
</ul>
<p>この値は 0 ~ 604800 (7 日) の範囲で指定できます。 値が0の場合は、監視対象のメモリページがタイムアウトにならないことを指定します。既定値は 86400 (24 時間) です。</p>
<div class="alert">
<strong>注</strong>  この値が許容範囲外の数値に設定されている場合は、既定値が使用されます。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

アプリケーションの互換性の理由で、次の2つのレガシレジストリ値がサポートされています。

<a href="" id="singlebiteccerrorthreshold"></a>**SingleBitEccErrorThreshold**  
この値は**Mempfathreshold**レジストリ値に対応します。

<a href="" id="maxcorrectedmceoutstanding"></a>**Max正しく Tedmce未処理**  
この値は、 **Mempfapagecount**レジストリ値に対応します。

**注意**  これらのレガシレジストリ値の代わりに、このトピックで既に説明したレジストリ値を使用する必要があります。

 

 

 




