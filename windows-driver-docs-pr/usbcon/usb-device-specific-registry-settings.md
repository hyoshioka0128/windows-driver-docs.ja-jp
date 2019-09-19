---
Description: このトピックでは、デバイス固有のレジストリエントリについて説明します。
title: USB デバイス レジストリ エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c32d3c6b425b11ca9ffbc027611798cb51f071
ms.sourcegitcommit: 4943143e8395db70beda5a98ad734fe1bb7068dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71080186"
---
# <a name="usb-device-registry-entries"></a>USB デバイス レジストリ エントリ


このトピックでは、デバイス固有のレジストリエントリについて説明します。

## <a name="find-device-information-after-it-enumerates-on-windows"></a>Windows での列挙後にデバイス情報を検索する


**デバイスに関するデバイスインターフェイス GUID、ハードウェア Id、デバイスクラスの情報を表示します**

1.  このレジストリキーを見つけて、 **Deviceinstance**の値をメモします。

    **HKEY\_LOCAL\_MACHINESYSTEM\\\\CurrentControlSet Control deviceclasses 制御\\\\\\**

    ![usb ハードウェア id](images/deviceinstance.png)

2.  デバイスインスタンスのレジストリキーを検索し、デバイスインターフェイスの GUID を取得します。

    **HKEY\_LOCAL\_MACHINESYSTEM\\CurrentControlSet\\EnumUSB\\ hardware id&gt; \\\\\\&lt;&lt;インスタンス id&gt;デバイスパラメーター\\**

    ![usb デバイスインターフェイス guid](images/device-interface-guid2.png)

3.  デバイスインスタンスキーの下で、デバイスクラス、サブクラス、およびプロトコルコードに注意してください。

    **HKEY\_LOCAL\_MACHINESYSTEM\\CurrentControlSet\\EnumUSB\\\\**

    ![usb デバイスクラスサブクラスプロトコルコード](images/deviceclass.png)

## <a name="registry-settings-for-configuring-usb-driver-stack-behavior"></a>USB ドライバースタック動作を構成するためのレジストリ設定


このトピックで説明するレジストリエントリは、次のキーの下にあります。

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         Control
            usbflags
               <VVVVPPPPRRRR>
                  <Device-specific registry entry>
```

***Vvvvpppprrrrr***キーで、

-   *vvvv*は、ベンダーを識別する4桁の16進数です。
-   *pppp*は、製品を識別する4桁の16進数です。
-   *rrrr*は、デバイスのリビジョン番号を含む4桁の16進数です。

ベンダー ID、製品 ID、リビジョン番号の値は、 [USB デバイス記述子](usb-device-descriptors.md)から取得されます。
次の表では、 ***vvvvpppprrrrr***キーに使用できるレジストリエントリについて説明します。 USB ドライバースタックは、これらのエントリを読み取り専用の値と見なします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ エントリ</th>
<th>説明</th>
<th>設定可能な値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>osvc</strong></p>
<p>REG_BINARY</p>
<p>Windows XP 以降のバージョンでサポートされています。</p></td>
<td><p>オペレーティングシステムが<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft-Defined USB Descriptors](microsoft-defined-usb-descriptors.md)">Microsoft 定義の USB 記述子</a>用にデバイスを照会したかどうかを示します。 以前に試行された OS 記述子クエリが成功した場合、値には、OS 文字列記述子のベンダーコードが含まれます。</p></td>
<td><ul>
<li><p>0x0000デバイスは、Microsoft OS 文字列記述子要求に対して有効な応答を提供しませんでした。</p></li>
<li><p>0x01xx:デバイスは、Microsoft OS 文字列記述子要求に対して有効な応答を提供しました。 xx は応答に含まれる<strong>bVendorCode</strong>です。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>IgnoreHWSerNum</strong></p>
<p>REG_BINARY</p>
<p>Windows Vista 以降のバージョンでサポートされています。</p></td>
<td><p>USB ドライバースタックがデバイスのシリアル番号を無視する必要があるかどうかを示します。</p></td>
<td><ul>
<li><p>0x00この設定は無効になっています。</p></li>
<li><p>0x01USB ドライバースタックがデバイスのシリアル番号を無視するように強制します。 そのため、デバイスインスタンスは、デバイスが接続されているポートに関連付けられています。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>ResetOnResume</strong></p>
<p>REG_BINARY</p>
<p>Windows Vista 以降のバージョンでサポートされています。</p></td>
<td><p>ポートがスリープ状態から再開されたときに、USB ドライバースタックがデバイスをリセットする必要があるかどうかを示します。</p></td>
<td><ul>
<li><p>0x0000この設定は無効になっています。</p></li>
<li><p>0x0001ポートの再開時にデバイスをリセットするように、USB ドライバースタックを強制します。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



