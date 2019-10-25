---
title: ファイル システムからの検証チェック要求への応答
description: ファイル システムからの検証チェック要求への応答
ms.assetid: 227e65d6-d746-4b16-978d-4d42be9aeb2c
keywords:
- リムーバブルメディアの WDK カーネル、確認-確認要求
- 確認-確認要求 WDK リムーバブルメディア
- メディア変更要求 WDK リムーバブルメディア
- リムーバブルメディアの変更の確認
- リムーバブルメディアの変更の確認
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf2df0db0d517079ab1c5254dbda682522ec949
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838445"
---
# <a name="responding-to-check-verify-requests-from-the-file-system"></a>ファイル システムからの検証チェック要求への応答





また、ファイルシステムは、irp [ **\_MJ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)に対して、デバイスドライバーのディスパッチエントリポイントに irp を送信することができます。これにより、i/o スタックの場所に**DeviceIoControl コード**が設定されています。示し

<a href="" id="ioctl-xxx-check-verify"></a>IOCTL\_*XXX*\_チェック\_確認  
ここで、 *XXX*は、DISK、TAPE、または CDROM などのデバイスの種類です。

このタイプのディスクには、パーティション分割解除された (フロッピー) デバイスとパーティション分割されたリムーバブルメディアデバイスの両方が含まれています。

基になるデバイスドライバーによってメディアが変更されていないと判断された場合、ドライバーは IRP を完了し、 **Iostatus**ブロックを次の値で返します。

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
<td><p><strong>参照</strong></p></td>
<td><p>0に設定</p></td>
</tr>
</tbody>
</table>

 

さらに、デバイスの種類が DISK または CDROM で、呼び出し元によって出力バッファーが指定されている場合、ドライバーは**irp-&gt;AssociatedIrp**のバッファーにあるメディア変更数を返し、 **Irp&gt;iostatus**を設定します。**sizeof**(ULONG)。 このカウントを返すことにより、ドライバーは、メディアがパースペクティブから変更されたかどうかを判断する機会を呼び出し元に提供します。

基になるデバイスドライバーによってメディアが変更されたと判断された場合、ボリュームがマウントされているかどうかによって異なる操作が行われます。 ボリュームがマウントされている (VPB\_マウントされたフラグが VPB で設定されている) 場合、ドライバーは次の操作を実行する必要があります。

1.  **DeviceObject**でフラグを設定するには **、\_** ボリュームを確認\_で**フラグ**を設定します。

2.  IRP の**Iostatus**ブロックを次のように設定します。
    -   **状態を状態に設定\_** 確認\_必要
    -   0に設定される**情報**

3.  入力 IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

ボリュームがマウントされていない場合、ドライバーは DO\_VERIFY\_ボリュームビットを設定しないようにする必要があります。 ドライバーは**Iostatus. status**を STATUS\_IO\_デバイス\_エラーに設定し、 **Iostatus. 情報**を0に設定し、IRP で**IoCompleteRequest**を呼び出します。

 

 




