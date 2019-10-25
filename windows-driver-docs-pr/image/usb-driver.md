---
title: USB ドライバー
description: USB ドライバー
ms.assetid: c20bd393-98d0-498e-a3e8-bbd1958ed774
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8d4421e0dbaace2a3f3e101a85b0540d974185b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840732"
---
# <a name="usb-driver"></a>USB ドライバー





カーネルモードの USB バス用イメージドライバーでは、1つのコントロールエンドポイントと、複数の割り込み、一括イン、および一括送信エンドポイントがサポートされています。 制御と割り込みのエンドポイントには、i/o 制御コードと[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を使用してアクセスできます。 この一括エンドポイントには、 **ReadFile**と**WriteFile**を使用してアクセスできます。

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)、 **ReadFile**、または**WriteFile**を呼び出す前に、デバイスハンドルを取得するために[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) (Microsoft Windows SDK のドキュメントで説明されているすべて) を呼び出す必要があります。 各エンドポイントの種類 (コントロール、割り込み、一括入力、一括出力) のいずれかをサポートしていないデバイスの場合、 **CreateFile**を1回呼び出すと、各エンドポイントへの転送パイプが開かれます。

複数の割り込みまたは一括エンドポイントをサポートするデバイスでは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を1回呼び出すと、各型の最上位のエンドポイントにパイプ転送が開かれます。 別のエンドポイントを使用する場合は、次の操作を行う必要があります。

1.  [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出し、IOCTL の i/o 制御コードを指定し[ **\_パイプ\_構成を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_pipe_configuration)して、ポートのエンドポイントインデックス番号 (つまり、返された[**usbscan\_パイプへのインデックス) を決定し\_\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ns-usbscan-_usbscan_pipe_information)構造体配列)。 これらのインデックス番号は、*ユニバーサルシリアルバス仕様*で説明されているエンドポイント番号では*ない*ことに注意してください。

2.  CreateFile を呼び出すときに、 [**Istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)によって返されたポート名に、円記号とエンドポイントのインデックス番号を追加します。

たとえば、ポート名が "usbscan0" のデバイスには、各種類 (割り込み、一括入力、一括出力) の2つのエンドポイントがあり、次のようにインデックス番号が付けられているとします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インデックス</th>
<th>タスクバーの検索ボックスに</th>
<th>終点#</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>妨害</p></td>
<td><p>0x01</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>一括で</p></td>
<td><p>0x82</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>一括で</p></td>
<td><p>0x83</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>一括送信</p></td>
<td><p>0x04</p></td>
</tr>
<tr class="odd">
<td><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td><p>一括送信</p></td>
<td><p>0x05</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>妨害</p></td>
<td><p>0x06</p></td>
</tr>
</tbody>
</table>

 

ポート名が "usbscan0" の[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出すと、関数は、インデックス値が2、4、および5のエンドポイントと、コントロールエンドポイントへの転送パイプを開きます。

ポート名が "usbscan0\\1" の[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出すと、関数は、インデックス値が1、4、および5のエンドポイントと、コントロールエンドポイントへの転送パイプを開きます。

このデバイスでは、割り込みエンドポイント0、バルクエンドポイント1、および一括送信エンドポイント3を使用する場合は、"usbscan0\\0"、"usbscan0\\1"、および "usbscan0\\3" のポート名を指定して、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を3回呼び出します。 これにより、3つのデバイスハンドルが作成されます。 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)、 **ReadFile**、または**WriteFile**の後続の呼び出しが行われるたびに、目的のパイプに関連付けられているデバイスハンドルを指定する必要があります。

サポートされているコントロールエンドポイントは1つだけであるため、コントロールパイプを使用する i/o 制御コードを指定すると、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)に指定されたエンドポイント (存在する場合) に関係なく、ドライバーは適切なエンドポイントを使用します。

すべての i/o 制御コードの説明については、「 [USB 静止イメージ I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)」を参照してください。

カーネルモードの USB ドライバーは、パッケージまたはメッセージプロトコルを実装していません。 読み取り操作では、特定のパケットアラインメントは必要ありませんが、読み取り要求が最大パケットサイズの境界に合わせて調整されると、パフォーマンスが向上する可能性があります。 最大パケットサイズを取得するには、 [**IOCTL\_GET\_CHANNEL\_\_RQST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_get_channel_align_rqst) i/o 制御コードを配置します。

 

 




