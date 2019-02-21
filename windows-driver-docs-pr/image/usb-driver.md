---
title: USB ドライバー
description: USB ドライバー
ms.assetid: c20bd393-98d0-498e-a3e8-bbd1958ed774
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91bc1d7c28c3927ed2e0c683b340d4bda57d61a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529375"
---
# <a name="usb-driver"></a>USB ドライバー





USB バス静止画像カーネル モード ドライバーには、複数の割り込み、一括 IN、および一括エンドポイントと共に、1 つのコントロール エンドポイントがサポートしています。 コントロールおよび割り込みのエンドポイントは I/O 制御コードを使用してアクセスおよび[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)します。 一括エンドポイントを使用してアクセス**ReadFile**と**WriteFile**します。

呼び出しの前に[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、 **ReadFile**、または**WriteFile**、呼び出す必要があります[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) (すべて、Microsoft Windows SDK ドキュメントで説明されている) にデバイス ハンドルを取得します。 各エンドポイントの種類の 1 つをサポートするデバイスの (制御、中断、一括を一括)、1 回の呼び出し**CreateFile**が開きますがパイプを各エンドポイントに転送します。

1 つの呼び出し、複数の中断や一括エンドポイントをサポートするデバイス用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)が開きますがパイプを各型の最も高い数字のエンドポイントに転送します。 別のエンドポイントを使用する場合は、次の操作を行う必要があります。

1.  呼び出す[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)の I/O 制御コードを指定する[ **IOCTL\_取得\_パイプ\_構成** ](https://msdn.microsoft.com/library/windows/hardware/ff542859)、ポートのエンドポイントのインデックス番号を確認する (つまり、返されたにインデックスを作成[ **USBSCAN\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff548547)構造体配列の場合)。 これらのインデックス番号は*いない*で説明されているエンドポイントの番号、*ユニバーサル シリアル バス仕様*します。

2.  によって返されるポート名に円記号と、エンドポイントのインデックス番号を追加[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944) CreateFile の呼び出し時にします。

たとえば、("usbscan0"のポートの名前) でのデバイスが各型の 2 つのエンドポイント (中断、一括を一括) 次のようにインデックス番号します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インデックス</th>
<th>種類</th>
<th>エンドポイント数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>割り込み</p></td>
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
<td><p>一括します。</p></td>
<td><p>0x04</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>一括します。</p></td>
<td><p>0x05</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>割り込み</p></td>
<td><p>0x06</p></td>
</tr>
</tbody>
</table>

 

呼び出す場合[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) "usbscan0"のポート名、関数は、2、4、および 5 のインデックス値を持つエンドポイントに加えて、コントロール エンドポイントに転送パイプが開きます。

呼び出す場合[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)ポート名を持つ"usbscan0\\1"、関数は、1、4、および 5 のインデックス値を持つエンドポイントに加えて、コントロール エンドポイントに転送パイプを開きます。

このデバイスに対する割り込みエンドポイント 0、一括でエンドポイント 1、および外部エンドポイント 3 一括を使用する場合を呼び出す[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) 3 回のポートの名前を指定する"usbscan0\\0"、"usbscan0\\1"と"usbscan0\\3"。 これには、次の 3 つのデバイス ハンドルが作成されます。 後続の呼び出しのたびに[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、 **ReadFile**、または**WriteFile**が行われた、デバイスのハンドルに関連付けられている、必要なパイプを指定する必要があります。

1 つのコントロール エンドポイントがサポートされているためを指定したコントロールのパイプを使用する I/O 制御コードが原因 (ある場合)、エンドポイントに関係なく、適切なエンドポイントを使用するドライバーを指定する[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858).

すべての I/O 制御コードの説明については、次を参照してください。 [USB まだイメージ I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff548569)します。

カーネル モードの USB ドライバーは、パッケージまたはメッセージのプロトコルを実装していません。 読み取り操作では、特定のパケットの配置は必要ありませんが、読み取り要求は最大パケット サイズの境界に揃えて配置した場合、パフォーマンスの向上を実現できます。 使用してパケットの最大サイズを取得することができます、 [ **IOCTL\_取得\_チャネル\_ALIGN\_RQST** ](https://msdn.microsoft.com/library/windows/hardware/ff542849) I/O 制御コード。

 

 




