---
Description: This paper provides information about USB ContainerIDs for the Windows operating system. It includes guidelines for device manufacturers to program their multifunction USB devices so that they can be correctly detected by Windows.
title: Windows における USB ContainerID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8214980cf6f42494b66141d8791922955aee635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578401"
---
# <a name="usb-containerids-in-windows"></a>Windows における USB ContainerID


このホワイト ペーパーは、USB に関する情報を提供します。 **ContainerID**の Windows オペレーティング システム。 これには、Windows によって正しく検出されるように、多機能の USB デバイスをプログラミングするデバイスの製造元向けガイドラインが含まれます。

Windows 7 以降、ユーザーを利用できますの自分のコンピューターに接続されているデバイスのすべての機能。 これには、組み合わせのプリンター、スキャナー、およびコピー機のデバイスなどの多機能デバイスが含まれます。 Windows 7 には、デバイスのコンテナーに 1 つの物理デバイスのすべての機能を統合するためのサポートが含まれています。 デバイス コンテナーは、物理デバイスの仮想表現です。 この統合を割り当てることで実現を**ContainerID**プロパティを物理デバイスの列挙は各デバイス関数。 同じを割り当てることで**ContainerID** Windows 7 の各デバイス関数に値が同じ物理デバイスにデバイスのすべての関数が属していることを認識します。

すべての種類の異なるバスの種類を使用して、コンピューターに接続するデバイスのデバイスのコンテナーをサポートできます。 ただし、すべてのバスの種類が同じメカニズムを使用を生成するため、 **ContainerID**します。 USB デバイス、デバイスのベンダーを使用できます、 **ContainerID**を記述する記述子、 **ContainerID**物理デバイス。 A **ContainerID**記述子は、USB デバイスのファームウェアに格納できる Microsoft OS 機能記述子。 USB デバイス製造元で正しく実装これらする必要があります**ContainerID** Windows 7 で利用できる新しいデバイス機能を活用するために自分のデバイス内の記述子。 USB デバイス製造元が 1 つだけを実装する必要があります**ContainerID**デバイスがサポートする数のデバイス関数に関係なく、物理デバイスごとにします。

デバイス コンテナーに 1 つのデバイスのすべての機能の統合についての詳細については、[どのコンテナー Id が生成される](https://msdn.microsoft.com/library/windows/hardware/ff546193)を参照してください。

USB デバイスの Microsoft OS ディスクリプターの詳細については、[USB デバイスの Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)を参照してください。

## <a name="how-a-usb-containerid-is-generated"></a>USB ContainerID を生成する方法


生成する 2 つの方法を次に、 **ContainerID** USB デバイス。

-   USB デバイスの製造元を指定します、 **ContainerID** Microsoft OS を使用して、デバイスのファームウェアで**ContainerID**記述子。
-   Microsoft USB ハブのドライバーが自動的に作成、 **ContainerID**デバイスから、デバイスの製品 ID (PID) の組み合わせ、仕入先 ID (VID)、リビジョン番号、およびシリアル番号。 このような状況で Microsoft USB ハブのドライバーを作成、 **ContainerID**を最小限の機能です。 このメソッドは、一意のシリアル番号を持つデバイスにのみ適用されます。

## <a name="usb-containerid-contents"></a>USB ContainerID 内容


USB **ContainerID**汎用一意識別子 (UUID) 文字列の形式で、オペレーティング システムが表示されます。 **ContainerID** UUID が内に含まれる、 **ContainerID**記述子。 A **ContainerID**記述子は、デバイス レベルの Microsoft OS 機能記述子。 オペレーティング システムが USB を要求したときにそのため、 **ContainerID**記述子の要求の wValue フィールドは、0 に常に設定する必要があります。 Microsoft OS 機能ディスクリプターと記述子の要求の詳細については、[Microsoft OS 1.0 記述子仕様](https://go.microsoft.com/fwlink/p/?linkid=617519)を参照してください。

A **ContainerID**記述子は、ヘッダーのセクションで構成されています。

| Offset | フィールド          | サイズ | 型           | 説明                                                                                                                                                                                                                                                                                                                                                                                         |
|--------|----------------|------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0      | **dwLength**   | 4    | 符号なしの DWord | 全体の長さをバイト単位で**ContainerID**記述子。 このフィールドは、常に、0x18 の値に設定する必要があります。                                                                                                                                                                                                                                                                                   |
| 4      | **bcdVersion** | 2    | BCD            | バージョン番号、 **ContainerID**記述子、バイナリ コード化された 10 進数 (BCD) が各ニブルが 1 桁の数字に対応します。 最上位バイト (MSB) は、小数点の前に 2 桁の数字を含み、最下位バイト (LSB) には、小数点より後の 2 桁の数字が含まれています。 たとえば、1.00 のバージョンは 0x0100 として表されます。 このフィールドは、0x0100 に常に設定する必要があります。 |
| 6      | **wIndex**     | 2    | Word           | このフィールドが USB を 6 に設定されて常に**ContainerID**記述子。                                                                                                                                                                                                                                                                                                                                  |

 

A **ContainerID** ContainerID セクションの記述子で構成されます。

| Offset | フィールド            | サイズ | 型           | 説明           |
|--------|------------------|------|----------------|-----------------------|
| 0      | **bContainerID** | 16   | 符号なしの DWord | **ContainerID**データ。 |

 

デバイスの製造元は、デバイスの各インスタンスでの汎用一意識別 16 バイト値を持つことを確保するため、 **ContainerID**します。 また、デバイスを報告する必要があります、同じ**ContainerID**の電源を入れ、毎回の値します。
重複する 0 に近くなる可能性が Uuid を生成するためのいくつか確立されているアルゴリズムはあります。 デバイスの製造元は、ニーズに最も合った UUID 生成アルゴリズムを選択できます。 結果が一意な UUID 生成アルゴリズムを使用する必要はありません。

## <a name="usb-containerid-syntax"></a>USB ContainerID 構文


A **ContainerID** {xxxxxxxx xxxx-xxxx-。} の標準の UUID 文字列の形式で報告されます。 次に表現の例では、0 C B4 A7 のファームウェア 2c D1 7B 25 4F B5 73 A1 3A 97 5D DC 07 USB **ContainerID**、{2CA7B40C-7BD1-4F25-B573-A13A975DDC07} UUID 文字列として書式設定されています。

```cpp
UCHAR Example<mark type="member">ContainerID</mark>Descriptor[24] =
{
    0x18, 0x00, 0x00, 0x00,     // dwLength - 24 bytes
    0x00, 0x01,                 // bcdVersion - 1.00
    0x06, 0x00,                 // wIndex – 6 for a <mark type="member">ContainerID</mark>

    0x0C, 0xB4, 0xA7, 0x2C,     // b<mark type="member">ContainerID</mark> -
    0xD1, 0x7B, 0x25, 0x4F,     // {2CA7B40C-7BD1-4F25-B573-A13A975DDC07}
    0xB5, 0x73, 0xA1, 0x3A,     // 0C B4 A7 2C D1 7B 25 4F B5 73 A1 3A 97 5D DC 07
    0x97, 0x5D, 0xDC, 0x07      //
}
```

UUID 文字列として書式設定するには、最初の 8 バイトのバイト順の変更に注意してください。

## <a name="microsoft-os-descriptor-changes"></a>Microsoft OS 記述子の変更


レガシを保持する**ContainerID**機能のサポートを示すために使用できる Microsoft OS 文字列記述子フィールドが追加されている新しいフラグ、 **ContainerID**記述子。

Microsoft OS 文字列記述子の現在の定義に、1 バイトのパッド フィールドが含まれています**bPad**0 に設定されている通常の記述子の最後にします。 USB デバイスは、新しいをサポートする**ContainerID**、 **bPad**フィールドは、フラグ フィールドとして再定義**bFlags**します。 このフィールドの 1 のビットを使用して、指定のサポート、 **ContainerID**記述子。 表 3 には、USB デバイスの Microsoft OS 文字列記述子フィールドについて説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>長さ (バイト)</th>
<th>[値]</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>bLength</strong></td>
<td>1</td>
<td>0x12</td>
<td>記述子の長さ。</td>
</tr>
<tr class="even">
<td><strong>bDescriptorType</strong></td>
<td>1</td>
<td>0x03</td>
<td>記述子の型。 0x03 の値では、Microsoft OS 文字列記述子を示します。</td>
</tr>
<tr class="odd">
<td><strong>qwSignature</strong></td>
<td>14</td>
<td>' MSFT100'</td>
<td>署名のフィールドです。</td>
</tr>
<tr class="even">
<td><strong>bMS_VendorCode</strong></td>
<td>1</td>
<td>仕入先のコード</td>
<td>ベンダー コード。</td>
</tr>
<tr class="odd">
<td><strong>bFlags</strong></td>
<td>1</td>
<td>0x02</td>
<td><p>ビット 0:予約済み</p>
<p>ビット 1:<strong>ContainerID</strong>サポート</p>
<ul>
<li>0:サポートしていません<strong>ContainerID</strong></li>
<li>1:サポート<strong>ContainerID</strong></li>
</ul>
<p>ビット 2 ~ 7:予約済み</p></td>
</tr>
</tbody>
</table>

 

現在 Microsoft OS ディスクリプターをサポートがサポートしている USB デバイスを出荷、 **ContainerID**記述子が、 **bPad**フィールド 0x00 に設定します。 USB ハブのドライバーが、USB のようなデバイスを照会できません**ContainerID**記述子。
## <a name="container-view-of-a-usb-multifunction-device"></a>USB 多機能デバイスのコンテナー ビュー


**ContainerID**多機能の USB デバイスのデバイスを統合する情報を提供します。 図 1 は、方法の例を示しています。 製品内のすべての個々 のデバイスを使用して同じときに、多機能プリンターのすべてのデバイスが 1 つのデバイスのコンテナーに統合されます**ContainerID**します。

![多機能プリンターのすべてのデバイスの統合](images/containerid-multifunction.png)

USB 多機能デバイスのすべてのデバイスを統合することで、デバイスと Windows 7 でのプリンターで 1 つのデバイスとして、物理製品を表示できます。 図 2 では、USB 多機能キーボードとマウス デバイスでデバイスとプリンターの 1 つのデバイスとして表示されることを示す例です。

![デバイスとプリンターの多機能デバイス](images/containerid-multifunction1.png)

## <a name="usb-containerid-hck-requirements"></a>USB ContainerID HCK の要件


デバイスの製造元が生成されるデバイスの各インスタンスのグローバル一意識別を確保する必要があります**ContainerID**値 Windows が各 USB 多機能デバイスの機能を正常に統合できます。 Windows ハードウェア証明書のハードウェア認定キットには、要件が含まれています、USB の DEVFUND 0034 **ContainerID**デバイスに実装されている場合。 デバイスが USB を実装している場合**ContainerID**、Windows ハードウェア認定テスト、 **ContainerID** Microsoft OS ディスクリプターの一部としてテストし、チェックするかどうか、 **ContainerID**値はグローバルに一意です。 これらの Windows ハードウェア認定要件の詳細については、Windows ハードウェア認定の Web サイトを参照してください。

USB を実装するための推奨事項**ContainerID**デバイス ベンダーの設計、製造、および USB デバイスを出荷するための推奨事項を次に示します。

-   Windows 7 が多機能とを使用すると、複数のトランスポート USB デバイスのサポートを向上する方法について説明します、 **ContainerID**します。 「多機能デバイスのサポートと Windows 7 でデバイスのコンテナーのグループ化します。」の読み取りで開始することをお勧めします。
-   各 USB デバイスのシリアル番号が一意であることを確認します。 Windows ハードウェア認定要件の状態は、デバイスには、シリアル番号が含まれているシリアル番号が、デバイスの各インスタンスに対して一意である必要があります。
-   指定しない、 **ContainerID**システムに埋め込まれている USB デバイスです。 統合の USB デバイスは、ACPI BIOS 設定、または USB ハブ既述子に依存する必要があります**DeviceRemovable**ポートのビットします。
-   システムにアタッチされているすべての USB デバイスが一意であることを確認**ContainerID**値。 共有していない**ContainerID**値や、製品ライン全体での USB シリアル番号。
-   お使いのデバイスに正しくリムーバブル デバイスの機能を設定してください。
    **注**  追加 USB デバイス ベンダー **ContainerID** USB デバイスを以前に出荷する記述子は、デバイスのリリース番号を増やす必要があります (**bcdDevice**) で、デバイスのデバイス記述子。 USB ハブ ドライバー キャッシュ Microsoft OS 文字列に基づいて、デバイスのベンダー ID、製品 ID、およびデバイスのリリース番号、記述子 (またはのいずれかが不足している) ために必要です。 デバイスのリリース番号をインクリメントしない場合、ハブのドライバーで USB は照会されません**ContainerID**同じベンダーの ID、製品 ID、デバイスのリリース番号とデバイスのインスタンスを以前列挙されている場合、新しいデバイスのUSB をサポートしていなかった**ContainerID**記述子。

     

## <a name="related-topics"></a>関連トピック
[Windows 用の USB デバイスの構築](building-usb-devices-for-windows.md)  
[USB デバイス用のコンテナー Id](https://msdn.microsoft.com/library/windows/hardware/ff540084)  



