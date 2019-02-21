---
Description: USB interface association descriptor (IAD) allows the device to group interfaces that belong to a function.
title: USB インターフェイスの関連付けの記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1972b9b5a47db4d38c6feb0032bcfa8dab087af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535651"
---
# <a name="usb-interface-association-descriptor"></a>USB インターフェイスの関連付けの記述子


USB インターフェイスの関連付け記述子 (IAD) では、関数に属しているグループのインターフェイスにデバイスを許可します。 このトピックでは、クライアント ドライバーを調べる方法、デバイスに、IAD 関数が含まれているかどうかについて説明します。

ユニバーサル シリアル バス仕様、バージョン 2.0 では、1 つ以上のインターフェイスの 1 つの関数内で複合デバイスをグループ化はサポートされていません。 ただし、USB デバイス Working Group (DWG) の複数のインターフェイスを持つ関数を許可する USB デバイス クラスを作成して、USB 実行者のフォーラムの発行、エンジニア リングの変更通知 (ECN) インターフェイスのグループ化するためのメカニズムを定義します。

ECN には、インターフェイスの関連付け記述子 (IAD) インターフェイスのグループを定義するハードウェアの製造元を許可すると呼ばれる、USB 記述子を指定します。 Iad を使用する最も可能性のあるデバイスのクラスは次のとおりです。

-   USB ビデオ クラス仕様 (クラス コード - 0x0E)

-   USB オーディオ クラスの指定 (クラス コード - 0x01)

-   USB Bluetooth クラスの指定 (クラス コード - 0xE0)

Windows 7、Windows Server 2008、Windows Vista、Microsoft Windows Server 2003 Service Pack 1 (SP1)、および Microsoft Windows XP Service Pack 2 (SP2) は、Iad をサポートします。

次のサブセクションでは、Iad を使用する方法についての情報について説明します。

### <a href="" id="how-should-a-composite-device-alert-the-operating-system-that-it-has-i"></a>どのようにする必要があります複合デバイス アラートを使用するオペレーティング システムのファームウェアで Iad があります。

複合デバイスの製造元が通常デバイス クラスにゼロの値を割り当てる (*bDeviceClass*)、サブクラス (*bDeviceSubClass*)、およびプロトコル (*bDeviceProtocol*)、ユニバーサル シリアル バス仕様で指定したとおり、デバイス記述子フィールド。 これにより、製造元別のデバイス クラスとプロトコルを関連付ける個々 の各インターフェイスになります。

USB のコア チームを作成した特殊なクラスとプロトコル コード セットをそのいずれかのオペレーティング システムに通知するか、Iad の詳細については、デバイスのファームウェアに存在します。 デバイスのデバイスの記述子は、次の表に表示される値をいる必要があります。 そう、オペレーティング システムが、デバイスの Iad を認識されないか、デバイスのインターフェイスを適切にグループ化します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイス記述子フィールド</th>
<th>必要な値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>bDeviceClass</em></p></td>
<td><p>0xEF</p></td>
</tr>
<tr class="even">
<td><p><em>bDeviceSubClass</em></p></td>
<td><p>0x02</p></td>
</tr>
<tr class="odd">
<td><p><em>bDeviceProtocol</em></p></td>
<td><p>0x01</p></td>
</tr>
</tbody>
</table>

 

これらのコード値では、正しく、デバイスを列挙する特殊な用途のバス ドライバーをインストールする Iad をサポートしていない Windows のバージョンも警告されます。 デバイス記述子でこれらのコードがない、デバイスを列挙するために、システムが失敗または、デバイスが正常に動作しない可能性があります。

デバイスには、1 つ以上の IAD をことができます。 各 IAD、IAD を表すインターフェイス グループのインターフェイスの直前にある必要があります。

関数クラス (*bFunctionClass*)、サブクラス (*bFunctionSubclassClass*)、およびプロトコル (*bFunctionProtocol*)、IAD のフィールドがある値を含める必要がありますUSB デバイス クラスで指定された関数のインターフェイスを記述します。

IAD のクラスとサブクラスのフィールドは、IAD を記述するインターフェイスのコレクションのインターフェイスのクラスとサブクラスのフィールドに一致する必要はありません。 ただし、コレクションの最初のインターフェイスに、IAD のクラスとサブクラスのフィールドに一致するクラスとサブクラスのフィールドがあることをお勧めします。 次の表では、どのフィールドが一致する必要がありますを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IAD フィールド</th>
<th>対応するインターフェイスのフィールド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>bFunctionClass</em></p></td>
<td><p><em>bInterfaceClass</em></p></td>
</tr>
<tr class="even">
<td><p><em>bFunctionSubclassClass</em></p></td>
<td><p><em>bInterfaceSubClass</em></p></td>
</tr>
</tbody>
</table>

 

*BFirstInterface* IAD のフィールドは、関数の先頭のインターフェイスの数を示します。 *BInterfaceCount* IAD のフィールドでは、インターフェイスのコレクションがインターフェイスの数を示します。 インターフェイス、IAD インターフェイスのコレクションでは、連続するである必要があります (ありますインターフェイス番号の一覧のギャップ)、最初のインターフェイスの数がカウントは、コレクション内のすべてのインターフェイスを指定するだけで十分です。

### <a name="accessing-the-contents-of-an-iad"></a>IAD の内容にアクセスします。

クライアント ドライバーでは、IAD 記述子を直接アクセスできません。 IAD エンジニア リングの変更通知 (ECN) では、デバイスを返す構成記述子 (いる出力の構成) のソフトウェアをホストから要求を受信したときに構成情報で Iad を含める必要があることを指定します。 ホスト ソフトウェアは、いる出力要求を直接 Iad を取得することはできません。

ただし、クライアント ドライバーは、デバイスのハードウェア識別子 (Id) の USB デバイスの親のドライバーにクエリを実行し、デバイスのハードウェア Id、IAD のフィールドの詳細についての埋め込まれた情報を含めることをがします。

### <a name="usb-interface-association-descriptor-example"></a>USB インターフェイスの関連付けの記述子の例

複合 USB デバイスの記述子のレイアウトを次に示します。 例のデバイスでは、2 つの関数があります。

<a href="" id="function-1--video-class"></a>**関数 1:ビデオ クラス**  
この関数は、インターフェイスの関連付け記述子 (IAD) によって定義され、2 つのインターフェイスが含まれています。 ゼロ (0) とインターフェイス 1 つのインターフェイス。

」の説明に従ってハードウェアと関数の場合、互換性のある識別子 (Id) をシステムが生成[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。 適切な INF ファイルを照合した後、ビデオ クラス ドライバー スタックが読み込まれます。

<a href="" id="function-2--human-input-device"></a>**関数 2:人間の入力デバイス**  
この関数には、1 つだけのインターフェイスが含まれています。 インターフェイスの 2 つ (2)。

」の説明に従ってハードウェアと関数の場合、互換性 Id をシステムが生成[複合デバイスを USB でインターフェイス コレクションの列挙体](support-for-interface-collections.md)します。 適切な INF ファイルを照合した後は、システムは、人間の入力デバイス (HID) のクラス ドライバーを読み込みます。

記述子は次のとおりです。

### <a name="device-descriptor"></a>デバイス記述子:

```cpp
    BYTE  bLength      0x12
    BYTE  bDescriptorType    0x01
    WORD  bcdUSB      0x0200
    BYTE  bDeviceClass     0xEF
    BYTE  bDeviceSubClass   0x02
    BYTE  bDeviceProtocol    0x01
    BYTE  bMaxPacketSize0   0x40
    WORD  idVendor      0x045E
    WORD  idProduct      0xFFFF
    WORD  bcdDevice     0x0100
    BYTE  iManufacturer     0x01
    WORD  iProduct      0x02
    WORD  iSerialNumber    0x02
    BYTE  bNumConfigurations  0x01
```

### <a name="configuration-descriptor"></a>構成記述子:

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x02
    WORD  wTotalLength    0x....
    BYTE  bNumInterfaces    0x03
    BYTE  bConfigurationValue  0x01
    BYTE  iConfiguration     0x01
    BYTE  bmAttributes     0x80 (BUS Powered)
    BYTE  bMaxPower     0x19 (50 mA)
```

### <a name="interface-association-descriptor"></a>インターフェイスの関連付けの記述子。

```cpp
    BYTE  bLength      0x08
    BYTE  bDescriptorType    0x0B
    BYTE  bFirstInterface    0x00
    BYTE  bInterfaceCount    0x02
    BYTE  bFunctionClass    0x0E
    BYTE  bFunctionSubClass   0x03
    BYTE  bFunctionProtocol   0x00
    BYTE  iFunction      0x04
```

### <a name="interface-descriptor-video-control"></a>インターフェイスの記述子 (ビデオのコントロール):

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x00
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x0E
    BYTE  bInterfaceSubClass   0x01
    BYTE  bInterfaceProtocol   0x00
    BYTE  iInterface      0x05
```

### <a name="class-specific-descriptors"></a>クラスの特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="endpoint-descriptors"></a>エンドポイント Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-video-streaming"></a>インターフェイスの記述子 (ビデオ ストリーミング)。

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x01
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x0E
    BYTE  bInterfaceSubClass   0x02
    BYTE  bInterfaceProtocol   0x00
    BYTE  iInterface      0x06
```

### <a href="" id="class-specific-descriptor-s--video"></a>クラスの特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a href="" id="endpoint-descriptor-s--video"></a>エンドポイント Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-human-input-devices"></a>インターフェイスの記述子 (人間の入力デバイス):

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x02
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x03
    BYTE  bInterfaceSubClass   0x01
    BYTE  bInterfaceProtocol   0x01
    BYTE  iInterface      0x07
```

### <a href="" id="class-specific-descriptor-s--hid"></a>クラスの特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a href="" id="endpoint-descriptor-s--hid"></a>エンドポイント Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

## <a name="related-topics"></a>関連トピック
[USB ディスクリプター](usb-descriptors.md)  



