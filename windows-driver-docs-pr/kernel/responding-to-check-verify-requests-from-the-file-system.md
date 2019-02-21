---
title: ファイル システムからのチェック-確認要求に応答
description: ファイル システムからのチェック-確認要求に応答
ms.assetid: 227e65d6-d746-4b16-978d-4d42be9aeb2c
keywords:
- リムーバブル メディア、WDK のカーネルは、要求をチェック-検証します。
- WDK のリムーバブル メディアの要求をチェックことを確認します。
- 変更要求 WDK リムーバブル メディアをメディア
- リムーバブル メディアへの変更の確認
- リムーバブル メディアへの変更を確認しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc426505fbccbd5d3fb650e44c61b51f2f5692e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551081"
---
# <a name="responding-to-check-verify-requests-from-the-file-system"></a>ファイル システムからのチェック-確認要求に応答





独自の裁量では、ファイル システムは、デバイス ドライバーのディスパッチ エントリ ポイントに IRP を送信できる[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744) による要求**Parameters.DeviceIoControl.IoControlCode** I/O スタックを次の設定の場所。

<a href="" id="ioctl-xxx-check-verify"></a>IOCTL\_*XXX*\_CHECK\_VERIFY  
場所*XXX*ディスク、テープ、または cd-rom ドライブなどのデバイスの種類です。

ディスクの種類には、両方 unpartitionable (フロッピー) が含まれていると分割可能なリムーバブル メディア デバイス。

基になるデバイス ドライバーが、メディアが変更されていないと判断した場合、ドライバーを返す、IRP を完了する必要があります、 **IoStatus**次の値をブロックします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>状態</strong></p></td>
<td><p>STATUS_SUCCESS に設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>情報</strong></p></td>
<td><p>0 に設定します。</p></td>
</tr>
</tbody>
</table>

 

さらに、デバイスの種類がディスク、cd-rom ドライブと、呼び出し元は、出力バッファーを指定しますまたは、ドライバーを返します、メディア、バッファー内の数を変更する**Irp -&gt;AssociatedIrp.SystemBuffer**設定と**Irp。&gt;IoStatus.Information**に**sizeof**(ULONG)。 この数を返すことによって、ドライバーはその観点から、メディアが変更されたかどうかを判断する機会に、呼び出し元を示します。

基になるデバイス ドライバーは、メディアが変更されたことを判断した場合、ボリュームがマウントされているかどうかに応じて、別のアクションがかかります。 ボリュームがマウントされている場合 (、VPB\_VPB にマウント済みフラグが設定)、ドライバーは、次を行う必要があります。

1.  設定、**フラグ**で、**デバイス オブジェクト**Or で**フラグ**か\_確認\_ボリューム。

2.  設定、 **IoStatus** IRP が、次のブロックします。
    -   **ステータス**状態に設定\_確認\_必要な作業
    -   **情報**を 0 に設定

3.  呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP の入力を使用します。

ドライバーは設定しないで、ボリュームがマウントされていない場合\_確認\_ボリューム ビット。 ドライバーを設定する必要があります**IoStatus.Status**ステータス\_IO\_デバイス\_セットのエラー、 **IoStatus.Information**をゼロにして呼び出す**IoCompleteRequest** IRP にします。

 

 




